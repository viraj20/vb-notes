---
type: source-summary
domain: learning
status: draft
created: 2026-04-19
updated: 2026-04-19
sources:
  - sources/learning/books/System Performance by Brendon Gregg.md
  - sources/learning/books/Kindle Highlights/Gregg-Systems Performance.md
---

# Systems Performance (Gregg)

- Author: Brendan Gregg
- ASIN: B08J5QZPNC
- Sources: personal notes (partial, CPU section only) + Kindle highlights (59 annotations)

Parent: [[../index|Learning MOC]] · Related: [[designing-data-intensive-applications|DDIA]] · [[site-reliability-engineering|SRE book]]

## Core argument

Tune closest to where work is performed. Measure utilization, saturation, and errors on every resource. Beware averages — they hide bursts and tail outliers.

> "Then there was the man who drowned crossing a stream with an average depth of six inches." (loc 2455)

## Key ideas extracted

- **Latency qualification** — "latency" alone is ambiguous; always qualify: request latency, TCP connection latency, disk I/O latency (loc 1233). See [[../concepts/latency-vs-throughput|Latency vs throughput]].
- **Knee point** — performance degrades non-linearly past a threshold where contention begins (loc 1393).
- **Saturation point** — at or near 100% utilization, queueing becomes frequent; any saturation is a performance issue because it implies waiting (loc 1396, 1473).
- **Observer effect** — metrics are not free; gathering them costs CPU and perturbs the target (loc 1426). See [[../concepts/use-method|USE method]].
- **Cache runtime formula** — `runtime = hit_rate × hit_latency + miss_rate × miss_latency` (loc 1505).
- **60% utilization ceiling** — averaged utilization above 60% often hides short 100% bursts; non-preemptible resources (disks) can't be interrupted for priority work (loc 1894).
- **[[../concepts/use-method|USE method]]** — for every resource, check Utilization, Saturation, Errors. Companion methodologies: workload characterization, drill-down, static analysis (loc 1966, 2089).
- **Micro- vs macro-benchmarks** — micro tests artificial workloads; macro tests real-world ones (loc 2120).
- **The performance mantra** — "Don't do it. Do it but don't do it again. Do it less. Do it later. Do it when they're not looking. Do it concurrently. Do it more cheaply." (loc 2140).
- **99 Hz profiling** — avoids lockstep aliasing with 100 Hz workloads (loc 3722).
- **CPU cache hierarchy** — L1: few cycles, L2: ~dozen, main memory: ~60 ns / 240 cycles (loc 6240).
- **Suggested methodology order** — performance monitoring → USE method → profiling → micro-benchmarking → static tuning (loc 6492).

## Personal notes fragment

Own note (2023-04-06) started a CPU chapter outline: scheduling domains, performance monitoring counters. Sparse; complemented by the Kindle highlights above.

## Concepts this book anchors

- [[../concepts/use-method|USE method]]
- [[../concepts/latency-vs-throughput|Latency vs throughput]]
- [[../concepts/golden-signals|Golden signals]] (complementary to USE)

## Other notable passages

**Latency as the universal currency.** Gregg anchors performance on time, not rates — latency is "time spent waiting before an operation is performed" (loc 1225), and comparing 100 ms of network I/O vs 50 ms of disk I/O is tractable where comparing "100 network I/O vs 50 disk I/O" is not (loc 1248). A reference time-scale table (loc 1259) grounds the intuition that a cache miss, a disk seek, and a network hop live on different orders of magnitude.

**Trade-offs and where to tune.** "Trade-offs: pick two" (loc 1289) frames the CPU/memory swap — cache results to save CPU, or compress to save memory (loc 1293). Tuning is most effective closest to the work: for app-driven workloads, inside the application (loc 1302). Utilization itself is the throughput-delivered-over-capacity ratio (loc 1456), and a server choosing errors (503) over queueing can preserve linear response-time scalability (loc 1413).

**USE method nuances and averaging pitfalls.** The tollbooth analogy (loc 1815) shows why a 40% daily average utilization can still hide rush-hour 100% bursts — Appendix A's Linux USE checklist (loc 1880) exists precisely to defeat that blind spot. Workload characterization separates architecture problems from load problems: if request duration rose but rate did not, blame the service; if both rose, blame the load (loc 1933), and the same characterization feeds simulation benchmarks (loc 1956). Drill-down analysis narrows from high-level symptoms to specific call paths (loc 1966 is already cited; companion framing here).

**Mode, scheduling, and interrupts.** I/O-heavy workloads run mostly in kernel context; compute-bound ones stay in user mode (loc 2736), and every crossing is a mode switch (loc 2752). Interrupt handling splits into ISRs (loc 2810) and IRQs (loc 2817); a blocked thread's user-stack is frozen while its kernel-stack executes the syscall (loc 2963). Linux scheduling runs on `scheduler_tick()` → `check_preempt_curr()` → `__schedule()` → `pick_next_task()`, with `load_balance()` spreading work (loc 6412). Boot timing drops out of `systemd-analyze(1)` (loc 3400), and KPTI (loc 3402) is the Meltdown-era tax on syscall cost.

**CPU micro-architecture and power.** SMT (loc 6011) shares core resources across threads; P-states and C-states (loc 6151) govern frequency and idle depth. Cache-line size is the transfer unit that makes sequential access win (loc 6258), and cross-CPU coherence requires invalidating stale copies on every write (loc 6263). CPU investigation checklist: system/per-CPU/per-core utilization, thread count, kernel-vs-user callers, interrupt load, interconnect utilization, stall-cycle breakdowns (loc 6557).

**Observability tool taxonomy.** `/proc` is documented in `proc(5)` plus kernel `Documentation/filesystems/proc.txt`, with extended docs for diskstats and scheduler stats (loc 3956); delay accounting lives in `Documentation/accounting/delay-accounting.txt` (loc 3997); socket diag is `sock_diag(7)` (loc 4019). Dynamic tracing layers: tracepoints (loc 4145), kprobes (loc 4223), uprobes (loc 4255), USDT (loc 4283). Hardware counters appear as PMCs (loc 4288) — also called CPCs, PICs, or PMU events (loc 4289), with setup docs at loc 4358. Boot-time summary counters come from the OS since-boot (loc 2511); trace viewers include KernelShark and Trace Compass (loc 2577).

**Monitoring stack and micro-benchmarks.** Linux monitoring agents include Performance Co-Pilot (loc 3800), Prometheus (loc 3801), and collectd (loc 3803); Netflix Atlas (loc 1986) is the cloud-scale counterpart to that list (loc 3799). `iperf(1)` (loc 2123) is the canonical network micro-benchmark, complementing the micro-vs-macro distinction already covered.

## Source

- Personal note: `sources/learning/books/System Performance by Brendon Gregg.md`
- Kindle highlights: `sources/learning/books/Kindle Highlights/Gregg-Systems Performance.md`
