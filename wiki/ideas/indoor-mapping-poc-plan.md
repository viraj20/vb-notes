---
type: concept
domain: ideas
status: draft
created: 2026-05-10
updated: 2026-05-10
sources: []
---

# Indoor Mapping POC — Step-by-Step Plan

A concrete, follow-along build plan for a home-scale indoor positioning POC using **3 old Android phones as fixed BLE beacons**, a **laptop as the backend**, and a **browser-based dashboard** for visualization. Two phases:

- **Phase 1 — Live dot:** real-time x/y position rendered on a 2D floor plan, ≤2 m median error.
- **Phase 2 — Navigation:** A* pathfinding + turn-by-turn directions to a named destination room.

Parent concept: [[indoor-location-tracking-system|Indoor Location Tracking & Navigation System]]
MOC: [[index|Ideas MOC]]

---

## Architecture

```
[ Phone-A ]  [ Phone-B ]  [ Phone-C ]     ← 3 Android phones, plugged in, BLE advertising
     \           |           /
      \          |          /     RSSI broadcasts (iBeacon, ~100 ms ad interval)
       \         |         /
       [ Tracker device ]                  ← laptop (phase 1a) → daily phone (phase 1b)
              |
              | RSSI samples (HTTP POST or WebSocket)
              v
       [ Laptop: FastAPI + SQLite ]        ← trilateration, position store, REST API
              |
              v
       [ Browser: floor plan + dot ]       ← simple HTML/JS dashboard, polls /position
```

Three Android phones replace the 3–5 dedicated hardware beacons in the original plan. The laptop runs FastAPI and serves the dashboard. A fourth device — initially the laptop itself, later the user's daily phone — acts as the "person being tracked" by scanning BLE advertisements and posting RSSI samples to the backend.

---

## Bill of materials

| Item | Quantity | Notes |
|---|---|---|
| Old Android phones | 3 | Each acts as a fixed BLE beacon. Android 5.0+ ideal; older may lack BLE peripheral mode. |
| USB chargers + cables | 3 | Beacons must run continuously. Plan around outlet availability. |
| Wall mounts / shelves / hooks | 3 | Phones must sit at consistent height (~1.5–2 m), stable across sessions. |
| Laptop | 1 | Backend + initial scanner. Built-in BT 4.0+ is enough. |
| Tracker device | 1 | Laptop in phase 1a, your daily Android phone in phase 1b. |
| Tape measure / laser distance meter | 1 | For floor plan + calibration distances. |
| Floor plan source | — | Builder PDF, hand-measured sketch, or LiDAR scan if you have an iPhone Pro. |

Optional but recommended:
- **A 4th beacon** (used Android phone or a hardware iBeacon, ~₹500). Three beacons is the bare minimum for trilateration; a 4th dramatically improves robustness, especially when one beacon is occluded.
- **External USB BLE dongle** if your laptop's built-in radio is flaky.

---

## Project layout

```
indoor-poc/
  backend/
    main.py            # FastAPI app
    trilateration.py   # nonlinear least squares solver
    calibration.py     # path-loss model fit
    config.yaml        # beacon positions, RSSI model params, floor plan metadata
    floorplan.png
    db.sqlite
  scanner/
    scan_laptop.py     # phase 1a: bleak-based scanner
    scan_web.html      # phase 1b: Web Bluetooth scanner running on the daily phone
  dashboard/
    index.html
    app.js
  README.md
```

---

## Phase 0 — Prep (one evening)

### 0.1 Digitize the floor plan

Goal: a top-down image of the apartment with a known scale and a coordinate origin.

Two paths:
1. **Builder PDF** — the cleanest source if you have it. Open in any image editor, crop to your unit, export as PNG.
2. **Manual measurement** — measure each room with tape; sketch in Figma, draw.io, or even paper → photograph. Keep walls axis-aligned where possible.

Standardize:
- Origin at one corner of the floor plan (e.g. top-left).
- Scale: **1 px = 1 cm** is convenient (so a 5 m wall = 500 px, a 10 m × 8 m apartment = 1000 × 800 px).
- Save as `backend/floorplan.png` and metadata in `config.yaml`:

```yaml
floorplan:
  image: floorplan.png
  width_m: 10.0
  height_m: 8.0
  scale_px_per_m: 100
```

### 0.2 Choose 3 beacon positions

Place phones to **maximize coverage and minimize collinearity**. Three beacons in a straight line create a trilateration ambiguity — every position has a mirror solution across the line, and the solver flickers between them.

Heuristics for a typical 2BHK:
- One near the front door / entry corridor.
- One in the living-room / kitchen overlap.
- One at the bedroom corridor junction.
- Each within ~1 m of a power outlet.
- Mounted at ~1.5–2 m height (above most furniture, below most ceiling clutter).
- Line-of-sight to as much of the home as possible. BLE attenuates ~10 dB per drywall, more through brick or concrete.

Record each beacon's `(x_m, y_m)` in floor-plan coordinates:

```yaml
beacons:
  - id: 1
    name: phone-A
    x_m: 0.5
    y_m: 7.5
  - id: 2
    name: phone-B
    x_m: 6.2
    y_m: 4.0
  - id: 3
    name: phone-C
    x_m: 9.5
    y_m: 0.8
```

### 0.3 Set up the project skeleton

Create the directory tree above. Initialize a Python venv with:

```
fastapi uvicorn bleak numpy scipy pyyaml requests pydantic sqlalchemy
```

Add a minimal `main.py` and confirm `uvicorn backend.main:app --reload` boots a 200 OK on `/`.

---

## Phase 1 — Live dot

### 1.1 Configure the 3 phones as BLE beacons

For each Android phone:

1. Install **nRF Connect for Mobile** (Nordic Semiconductor, Play Store).
2. Open the **Advertiser** tab → "+" to create a new advertisement.
3. Configure as iBeacon:
   - **UUID:** generate one with `uuidgen` and use the same UUID across all 3 phones (e.g. `e2c56db5-dffb-48d2-b060-d0f5a71096e0`).
   - **Major:** `1` for all three.
   - **Minor:** `1` on phone A, `2` on phone B, `3` on phone C. The minor is how the scanner distinguishes them.
   - **TX power:** the highest the phone allows.
   - **Advertising interval:** 100 ms.
4. Disable battery optimization for nRF Connect: Settings → Apps → nRF Connect → Battery → Unrestricted.
5. Plug the phone into power, lock the screen, and verify the advertisement persists for 30 minutes by scanning from a second device.

**Done when:** all three phones are visible in your laptop's `bleak` scan with stable RSSI readings, even with screens locked, for 30 minutes continuously.

If a phone stops advertising on screen-off (Xiaomi/MIUI is the worst offender):
- Try **Beacon Simulator** (Play Store) as a fallback.
- Or write a 50-line Android foreground-service app that calls `BluetoothLeAdvertiser.startAdvertising`. Foreground services are exempt from background BLE throttling.

### 1.2 Scanner — laptop first

`scanner/scan_laptop.py`:

```python
import asyncio, time, struct, requests
from bleak import BleakScanner

BEACON_UUID = bytes.fromhex("e2c56db5dffb48d2b060d0f5a71096e0")
APPLE_MFG_ID = 0x004C
BACKEND = "http://localhost:8000/rssi"

def parse_ibeacon(adv_data):
    mfg = adv_data.manufacturer_data.get(APPLE_MFG_ID)
    if not mfg or len(mfg) < 23 or mfg[0:2] != b"\x02\x15":
        return None
    uuid_bytes = mfg[2:18]
    if uuid_bytes != BEACON_UUID:
        return None
    major = struct.unpack(">H", mfg[18:20])[0]
    minor = struct.unpack(">H", mfg[20:22])[0]
    tx_power = struct.unpack(">b", mfg[22:23])[0]
    return major, minor, tx_power

def handle(device, adv):
    parsed = parse_ibeacon(adv)
    if not parsed:
        return
    _, minor, _ = parsed
    try:
        requests.post(BACKEND, json={
            "minor": minor,
            "rssi": adv.rssi,
            "ts": time.time(),
        }, timeout=0.5)
    except requests.RequestException:
        pass

async def main():
    scanner = BleakScanner(handle)
    await scanner.start()
    try:
        await asyncio.sleep(86400)
    finally:
        await scanner.stop()

asyncio.run(main())
```

Run on the laptop. Walk it around the apartment slowly and confirm RSSI samples for all three minor IDs reach the backend.

### 1.3 Backend (FastAPI)

`backend/main.py` — endpoints:

| Method | Path | Purpose |
|---|---|---|
| `POST` | `/rssi` | Accept `{minor, rssi, ts}`, append to ring buffer per beacon. |
| `GET` | `/position` | Return current `{x, y, ts, confidence}` computed from latest RSSI window. |
| `GET` | `/floorplan.png` | Serve the floor plan image. |
| `GET` | `/config` | Serve beacon positions and floor plan metadata for the dashboard. |
| `GET` | `/raw` | (Debug) Serve recent RSSI samples as JSON for inspection. |

Storage: SQLite `samples(beacon_minor INT, rssi INT, ts REAL)`. On `/position`, query the last 60 s of samples per beacon, compute median RSSI per beacon over the last 1 s window, run trilateration. Cache the last computed position with a 200 ms TTL to avoid recomputing on every dashboard poll.

### 1.4 Calibration ritual

This is the step everyone underestimates. Without it, every beacon reports a different distance for the same physical point because phone radios vary by ±6 dB at the same TX power.

For **each** of the 3 beacons:

1. Stand at known distances from the beacon: **1 m, 2 m, 3 m, 5 m, 8 m** with line-of-sight.
2. At each distance, hold the tracker still and collect ~30 s of RSSI samples (≈300 samples at 100 ms ad rate).
3. Compute the median RSSI per distance.
4. Fit the **log-distance path-loss model**:

   ```
   RSSI(d) = A − 10·n·log₁₀(d)
   ```

   where `A` is the RSSI at 1 m and `n` is the environmental path-loss exponent (typically 2.0–4.0 indoors). Use `scipy.optimize.curve_fit`.

5. Store `(A_i, n_i)` per beacon in `config.yaml`:

   ```yaml
   beacons:
     - id: 1
       name: phone-A
       x_m: 0.5
       y_m: 7.5
       rssi_at_1m: -59
       path_loss_n: 2.4
   ```

6. Inverted at runtime to estimate distance:

   ```
   d = 10 ^ ((A − RSSI) / (10·n))
   ```

`backend/calibration.py` should be a standalone script: it reads a CSV `(beacon_minor, distance_m, rssi)`, fits per beacon, and writes the parameters back into `config.yaml`.

**Done when:** for each beacon, the fitted curve passes within ±2 dB of all 5 calibration points, and the residual standard deviation is under 4 dB.

### 1.5 Trilateration + smoothing

`backend/trilateration.py`:

```python
import numpy as np
from scipy.optimize import least_squares

def estimate_distance(rssi, A, n):
    return 10 ** ((A - rssi) / (10 * n))

def trilaterate(beacons, distances):
    """
    beacons:   list of (x, y) tuples
    distances: list of estimated distances (same order)
    returns:   (x, y, residual)
    """
    def residuals(p):
        x, y = p
        return [
            np.hypot(x - bx, y - by) - d
            for (bx, by), d in zip(beacons, distances)
        ]

    weights = [1.0 / max(d, 0.5)**2 for d in distances]

    def weighted_residuals(p):
        return np.array(residuals(p)) * np.array(weights)

    centroid = np.mean(beacons, axis=0)
    result = least_squares(weighted_residuals, x0=centroid, method="lm")
    return result.x[0], result.x[1], float(np.linalg.norm(result.fun))
```

Smoothing pipeline (in this order):
1. **RSSI median over last 1 s** per beacon (kills single-sample spikes).
2. **Distance estimate** via the path-loss inverse.
3. **Trilateration** (weighted least squares).
4. **Position EMA** with α = 0.3 over last position. Skip a Kalman filter for v1 — EMA is 5 lines and covers 90% of the smoothing benefit.

The least-squares **residual** doubles as a confidence metric: residual < 1.5 m → green dot, 1.5–3 m → yellow, > 3 m → red.

### 1.6 Web dashboard

`dashboard/index.html` + `dashboard/app.js`:

- Renders `floorplan.png` on a `<canvas>`.
- Polls `GET /position` every 500 ms.
- Draws a dot at `(x, y)` converted to pixels via `scale_px_per_m`. Color by confidence.
- Draws the 3 beacon positions as small green squares with their minor IDs labelled. Useful for debugging.
- Draws a translucent "uncertainty circle" sized by the residual.
- "Recenter" button: re-fit the canvas to the floor plan dimensions on demand.

### 1.7 Validate

Mark **5 ground-truth points** in the apartment with painter's tape — pick varied locations: front door, living-room center, kitchen, bedroom, bathroom doorway. Stand at each for 30 s, log the reported position, compute Euclidean error from the tape mark.

**Phase 1 success bar:**
- Median error ≤ 2 m across the 5 points.
- Room classification correct ≥ 90% of the time over a 5-minute walk.
- No flicker: dot moves smoothly when standing still.

If you're at 4–5 m error, the fix is almost always one of:
- **Recalibrate `n`** per beacon — environment matters more than people expect, and small furniture shifts can change `n` by 0.3–0.5.
- **Move beacons** to break collinearity — re-check the triangle they form.
- **Add a 4th beacon** — two more bearings cut typical error in half. A used phone or a hardware iBeacon both work.

### 1.8 Swap tracker laptop → daily phone (optional)

Phase 1a uses the laptop as the tracker because its BLE stack is mature and `bleak` is straightforward. Once the live dot is solid, move the tracker to your daily phone:

1. Open `scanner/scan_web.html` on Chrome on your daily Android phone.
2. Use the **Web Bluetooth API**:

   ```js
   const scan = await navigator.bluetooth.requestLEScan({
     acceptAllAdvertisements: true,
     keepRepeatedDevices: true,
   });
   navigator.bluetooth.addEventListener('advertisementreceived', (e) => {
     // parse iBeacon manufacturer data, POST to backend
   });
   ```

3. Enable `chrome://flags/#enable-experimental-web-platform-features` if `requestLEScan` isn't available.
4. POST samples to your laptop's IP on the same Wi-Fi (e.g. `http://192.168.1.42:8000/rssi`).

Web Bluetooth requires HTTPS or localhost — for a LAN-only POC, run the backend with `mkcert`-issued local certs, or wrap in a local tunnel.

---

## Phase 2 — Navigation

Begin only after Phase 1 has been validated.

### 2.1 Build the occupancy grid

- Cell size: **10 cm**. A 10 m × 8 m apartment becomes a 100 × 80 grid (8000 cells) — trivial to A* over.
- From `floorplan.png`, mark walls in black, traversable space in white. Two paths:
  1. Hand-paint walls in any image editor.
  2. OpenCV thresholding if your floor plan is high-contrast and clean:
     ```python
     img = cv2.imread('floorplan.png', cv2.IMREAD_GRAYSCALE)
     _, walls = cv2.threshold(img, 128, 1, cv2.THRESH_BINARY_INV)
     grid = walls  # 0 = walkable, 1 = blocked
     ```
- Inflate walls by 30 cm (3 cells) so paths don't hug corners:
  ```python
  from scipy.ndimage import binary_dilation
  grid = binary_dilation(grid, iterations=3).astype(int)
  ```
- Save as `backend/grid.npy`.

### 2.2 A* pathfinding

`networkx` works but is slow on dense grids. Hand-roll A* with `heapq` — about 50 lines:

```python
import heapq
import numpy as np

def astar(grid, start, goal):
    H, W = grid.shape
    def h(p): return np.hypot(p[0]-goal[0], p[1]-goal[1])
    open_set = [(h(start), 0, start, None)]
    came_from = {}
    g_score = {start: 0}
    while open_set:
        _, g, current, parent = heapq.heappop(open_set)
        if current in came_from:
            continue
        came_from[current] = parent
        if current == goal:
            path = []
            while current is not None:
                path.append(current)
                current = came_from[current]
            return list(reversed(path))
        for dx, dy in [(-1,0),(1,0),(0,-1),(0,1),(-1,-1),(-1,1),(1,-1),(1,1)]:
            nx, ny = current[0]+dx, current[1]+dy
            if not (0 <= nx < H and 0 <= ny < W) or grid[nx, ny]:
                continue
            step = np.hypot(dx, dy)
            ng = g + step
            if ng < g_score.get((nx, ny), float('inf')):
                g_score[(nx, ny)] = ng
                heapq.heappush(open_set, (ng + h((nx, ny)), ng, (nx, ny), current))
    return None
```

Endpoint: `GET /path?to=bedroom`. Resolve "bedroom" → grid coords via the semantic graph, run A*, return waypoints as a JSON list of `(x_m, y_m)`.

**Path simplification:** the raw A* output is a chain of single-cell steps. Run **Ramer-Douglas-Peucker** with epsilon = 30 cm to collapse to long line segments before sending to the dashboard.

### 2.3 Semantic graph

Hand-build in `config.yaml`:

```yaml
rooms:
  - name: bedroom
    bbox_m: [6.0, 0.0, 10.0, 4.0]   # x_min, y_min, x_max, y_max
    center_m: [8.0, 2.0]
  - name: kitchen
    bbox_m: [0.0, 0.0, 4.0, 3.5]
    center_m: [2.0, 1.7]
  - name: living_room
    bbox_m: [0.0, 3.5, 6.0, 8.0]
    center_m: [3.0, 5.7]
  ...
doorways:
  - between: [bedroom, living_room]
    at_m: [6.0, 3.0]
  ...
```

Used for: (a) destination lookup by name, (b) "turn left at the kitchen" descriptions, (c) labelling the current room on the dashboard regardless of position-estimate noise.

### 2.4 Turn-by-turn UI

- Draw the path on the floor plan as a polyline.
- Compute the **next-waypoint instruction** by comparing path heading at the user's position vs. the path heading after the next waypoint:
  - Heading delta < 30° → "Continue forward 3 m"
  - 30°–135° turn → "Turn left/right at the kitchen"
  - > 135° → "Turn around"
- Recompute the path when the user drifts > 1.5 m off the polyline for more than 3 s.

**Phase 2 success bar:** ask the dashboard to "navigate to bedroom," walk the suggested path, arrive without the path getting confused or oscillating.

---

## Risks & gotchas

1. **Android OEM BLE advertising throttling.** MIUI, ColorOS, and EMUI throttle background BLE aggressively. Mitigation in priority order:
   - Disable battery optimization for nRF Connect.
   - Keep the screen on (set timeout to "Never" while plugged in; a black-screen webpage with `wakeLock` works too).
   - Write a 50-line foreground-service Android app that calls `BluetoothLeAdvertiser.startAdvertising`. Foreground services are exempt from background BLE throttling — this is the durable fix.
2. **RSSI is noisy.** ±5 dB swings at fixed distance are normal. Hence: median filter, EMA smoothing, generous calibration samples. Don't try to fight noise with cleverness in the trilateration solver — fix it upstream in the RSSI pipeline.
3. **Multipath in small rooms.** BLE reflects off walls and metal surfaces. Calibrate at the actual heights/positions you'll deploy at — not on a desk in the middle of a room. Re-calibrate if you move furniture significantly.
4. **Body absorption.** A phone in your pocket reads 6–10 dB lower than the same phone in your hand. For phase 1, keep the tracker out and visible. Revisit for phase 2 with calibration data taken pocket-mounted.
5. **3 beacons is the bare minimum.** If accuracy is bad, the cheapest fix isn't more software — it's a 4th beacon. A used 4th Android off OLX or one hardware iBeacon (~₹500) will outperform a week of algorithm tuning.
6. **Trilateration ambiguity with collinear beacons.** Two solutions reflected across the line connecting them. The least-squares solver picks one arbitrarily and can flicker. Place the 3rd beacon clearly off-axis from the other two.
7. **Time-of-flight is not your friend.** BLE RSSI is an indirect distance proxy through power, not time. Don't expect sub-meter accuracy without UWB hardware. For UWB, look at the Apple AirTag / Estimote UWB line — but that's a different POC.
8. **Daylight savings / clock skew.** All RSSI timestamps come from the scanner. If you ever distribute scanners (multi-floor scale-up), drift becomes a real problem — sync via NTP. Not a phase-1 concern.

---

## Milestones

| Milestone | Deliverable | Effort |
|---|---|---|
| M0 | Floor plan PNG + beacon positions in `config.yaml` | 1 evening |
| M1 | 3 phones advertising stably for 24 hr | 1 evening |
| M2 | Laptop scanner posting RSSI to FastAPI | 1 evening |
| M3 | Calibration data collected, model fit per beacon | 2 hours |
| M4 | Trilateration returns a position | half day |
| M5 | **Phase 1 demo** — live dot on floor plan, 5-point validation | half day |
| M6 | Occupancy grid + A* | 1 day |
| M7 | Semantic graph + turn-by-turn UI | 1 day |
| M8 | **Phase 2 demo** — navigate to a named room | half day |

Phase 1 fits in a long weekend if no OEM throttling issues arise. Phase 2 fits in another.

---

## Decisions log

| Date | Decision | Rationale |
|---|---|---|
| 2026-05-10 | Phones-as-beacons (not phones-as-trackers) | Avoids buying hardware beacons; 3 phones cover the apartment adequately. |
| 2026-05-10 | Laptop + web dashboard, skip Pi and React Native | Fastest path to a working demo. Pi/React Native can come at scale-up. |
| 2026-05-10 | Phase 1 = live dot, Phase 2 = navigation | De-risks fundamentals (positioning) before layering pathfinding on top. |

---

## Open questions

- Privacy considerations once family members are tracked — solo POC for now, but worth thinking about before any scale-up.
- Whether to invest in a 4th beacon proactively or wait to see if 3 is sufficient.
- How to handle the tracker being offline (laptop sleeping, phone Bluetooth toggled) — graceful degradation in the dashboard.
- Eventual swap of nRF Connect → custom Android app for beacon role, to control TX power and advertising interval programmatically.

---

## Links

- [[indoor-location-tracking-system|Parent: Indoor Location Tracking & Navigation System]]
- [[index|Ideas MOC]]
