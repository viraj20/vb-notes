---
type: concept
domain: ideas
status: draft
created: 2026-04-24
updated: 2026-04-24
sources: []
---

# Indoor Location Tracking & Navigation System

A BLE-based indoor positioning system for tracking people and assets, with turn-by-turn navigation. POC starts at home, targets office scale (7 floors, 1000–25,000 people).

---

## Goals

- **Real-time lookup** — find where a specific person or asset is right now
- **Movement analytics** — space utilization, historical patterns
- **Security/access** — know who is where for compliance and safety
- **Indoor navigation** — guide users from point A to point B with turn-by-turn directions

---

## POC Strategy

Start with a **single home environment** to validate the hard parts:
- BLE beacon placement and signal stability
- Floor plan digitization and graph construction
- Pathfinding accuracy
- Phone app BLE scanning and position estimation

Then expand to **one office floor** before going full 7-floor rollout. This avoids building for scale before the fundamentals are validated.

---

## Hardware

### POC (Home)

| Component | Purpose | Quantity | Notes |
|---|---|---|---|
| BLE Beacons | Fixed signal sources for positioning | 3–5 | Estimote or Kontakt.io recommended |
| Smartphones (iOS/Android) | People tracking via BLE scan | Existing devices | Acts as the mobile tag for people |
| Raspberry Pi 4 | Local backend server during POC | 1 | Runs FastAPI + SQLite |
| iPhone 12 Pro+ or iPad Pro | LiDAR floor plan scan | 1 | For Polycam/Canvas digitization |

### Office Scale (Single Floor)

| Component | Purpose | Quantity | Notes |
|---|---|---|---|
| BLE Beacons | Fixed zone anchors | 50+ per floor | ~1 every 5–10m for navigation accuracy |
| BLE Asset Tags | Attached to equipment/assets | 1 per tracked asset | Battery-powered, 6–12 month life |
| Cloud Server / On-prem | Backend at scale | — | Postgres + message queue |
| Network switches | PoE for any powered readers | Per floor | If using powered readers instead of battery beacons |

### At 25,000 People (Full Scale)

Additional infrastructure:
- **Message queue** (Kafka or Pulsar) for ingesting location updates at scale
- **Time-series database** (InfluxDB or TimescaleDB) for movement analytics
- **Aggregation layer** — heatmap rendering instead of 25k individual dots on dashboard

---

## Technology Choices

### Positioning Technology: BLE (Bluetooth Low Energy)

- GPS is unreliable indoors — BLE is the right call
- Beacons are fixed, cheap, and stateless hardware
- Phones scan nearby beacons and report signal strengths (RSSI)
- Position estimated via **trilateration** (3+ beacons → one position)
- Zone-level accuracy sufficient for v1; higher beacon density enables navigation

### Map Representation

**Occupancy grid** for pathfinding:
- Floor plan image divided into a grid of cells
- Each cell marked walkable or blocked (wall)
- Simple to implement, easy to visualize
- A* runs directly on the grid

**Semantic graph** for UI:
- Rooms and corridors as nodes, doorways as edges
- Metadata per node (restricted zone, elevator, exit)
- Used for human-readable directions ("turn left at the kitchen")

Both layers coexist — grid for computation, graph for presentation.

### Floor Plan Digitization

1. **LiDAR scan** (fastest, most accurate) — use Polycam or Canvas on an iPhone 12 Pro+/iPad Pro. Exports dimensionally accurate 2D floor plan in minutes.
2. **Manual draw** (fallback) — measure rooms with a tape measure, draw in Floorplanner or Figma. More work but full control.

After digitization: overlay a grid on the floor plan image, mark walls using OpenCV, extract the traversable graph.

---

## Software Stack

### Backend — Python

| Library | Role |
|---|---|
| `FastAPI` | REST API for location updates and queries |
| `numpy` | Occupancy grid representation and operations |
| `networkx` | Semantic graph for rooms/corridors |
| `opencv` | Process floor plan image into walkable grid |
| `SQLite` → `Postgres` | Location store (SQLite for POC, Postgres at scale) |

### Mobile App — React Native

| Library | Role |
|---|---|
| `react-native-ble-plx` | BLE scanning — reads nearby beacon signal strengths |
| Custom trilateration module | Converts RSSI from 3+ beacons to x/y position |
| Map rendering (SVG/Canvas) | Displays floor plan with user position overlay |

### Dashboard — Web

- Simple web canvas or React frontend
- Real-time lookup: show current position of person/asset
- Heatmap view for analytics (aggregated, not 25k dots)
- Floor selector for multi-floor view

---

## Pathfinding

Algorithm: **A\*** on the occupancy grid.

Steps:
1. User requests navigation from current position → destination
2. Current position resolved from BLE trilateration
3. Destination looked up in semantic graph (room name → grid coordinates)
4. A* finds shortest walkable path on the grid
5. Path converted to human-readable waypoints via semantic graph
6. Directions pushed to mobile app

---

## Scaling Path

| Stage | People | Infra |
|---|---|---|
| Home POC | ~5 | Raspberry Pi, SQLite, 3–5 beacons |
| One office floor | ~100–200 | Cloud VM, Postgres, 50+ beacons |
| Full office (7 floors) | 1,000 | Multi-instance FastAPI, Postgres, per-floor beacon grid |
| Full scale | 25,000 | Kafka ingestion pipeline, TimescaleDB, aggregated dashboard |

The BLE beacon hardware scales linearly and cheaply. The bottleneck at 25k is the ingestion pipeline and dashboard rendering — both solvable without changing the core architecture.

---

## Open Questions

- Badge/wristband as fallback for people who don't carry phones?
- Privacy/consent policy for employee tracking
- Asset tag battery replacement cadence at office scale
- Restricted zone logic (who can see whom on the dashboard)

---

## Links

- [[wiki/ideas/index|Ideas MOC]]
