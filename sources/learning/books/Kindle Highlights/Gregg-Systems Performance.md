---
kindle-sync:
  bookId: '14545'
  title: Systems Performance
  author: Brendan Gregg
  asin: B08J5QZPNC
  lastAnnotatedDate: '2023-05-01'
  bookImageUrl: 'https://m.media-amazon.com/images/I/61aoW2kC0kL._SY160.jpg'
  highlightsCount: 59
captured: 2023-06-09
captured_via: kindle
wiki_compiled: true
---
# Systems Performance
## Metadata
* Author: [Brendan Gregg](https://www.amazon.comundefined)
* ASIN: B08J5QZPNC
* Reference: https://www.amazon.com/dp/B08J5QZPNC
* [Kindle link](kindle://book?action=open&asin=B08J5QZPNC)

## Highlights
The latency is the time spent waiting before an operation is performed. — location: [1225](kindle://book?action=open&asin=B08J5QZPNC&location=1225) ^ref-26997

---
Since the single word “latency” can be ambiguous, it is best to include qualifying terms to explain what it measures: request latency, TCP connection latency, etc. — location: [1233](kindle://book?action=open&asin=B08J5QZPNC&location=1233) ^ref-24966

---
If you had to choose between 100 network I/O or 50 disk I/O, how would you know which would perform better? It’s a complicated question, involving many factors: network hops, rate of network drops and retransmits, I/O size, random or sequential I/O, disk types, and so on. But if you compare 100 ms of total network I/O and 50 ms of total disk I/O, the difference is clear. — location: [1248](kindle://book?action=open&asin=B08J5QZPNC&location=1248) ^ref-60836

---
Example time scale of system latencies — location: [1259](kindle://book?action=open&asin=B08J5QZPNC&location=1259) ^ref-4739

---
Trade-offs: pick two — location: [1289](kindle://book?action=open&asin=B08J5QZPNC&location=1289) ^ref-39789

---
A common trade-off in performance tuning is the one between CPU and memory, as memory can be used to cache results, reducing CPU usage. On modern systems with an abundance of CPU, the trade may work the other way: CPU time may be spent compressing data to reduce memory usage. — location: [1293](kindle://book?action=open&asin=B08J5QZPNC&location=1293) ^ref-16471

---
Performance tuning is most effective when done closest to where the work is performed. For workloads driven by applications, this means within the application itself. — location: [1302](kindle://book?action=open&asin=B08J5QZPNC&location=1302) ^ref-20086

---
A point is then reached, marked with a dotted line, where contention for a resource begins to degrade throughput. This point can be described as a knee point, — location: [1393](kindle://book?action=open&asin=B08J5QZPNC&location=1393) ^ref-51289

---
This point may occur when a component reaches 100% utilization: the saturation point. It may also occur when a component approaches 100% utilization and queueing begins to be frequent and significant. — location: [1396](kindle://book?action=open&asin=B08J5QZPNC&location=1396) ^ref-30237

---
Linear scalability of response time could occur if the application begins to return errors when resources are unavailable, instead of queueing work. For example, a web server may return 503 “Service Unavailable” instead of adding requests to a queue, so that those requests that are served can be performed with a consistent response time. — location: [1413](kindle://book?action=open&asin=B08J5QZPNC&location=1413) ^ref-25059

---
Performance metrics are not free; at some point, CPU cycles must be spent to gather and store them. This causes overhead, which can negatively affect the performance of the target of measurement. This is called the observer effect. — location: [1426](kindle://book?action=open&asin=B08J5QZPNC&location=1426) ^ref-42963

---
A system or component (such as a disk drive) is able to deliver a certain amount of throughput. At any level of performance, the system or component is working at some proportion of its capacity. That proportion is called the utilization. — location: [1456](kindle://book?action=open&asin=B08J5QZPNC&location=1456) ^ref-12227

---
Any degree of saturation is a performance issue, as time is spent waiting (latency). — location: [1473](kindle://book?action=open&asin=B08J5QZPNC&location=1473) ^ref-16032

---
runtime = (hit rate × hit latency) + (miss rate × miss latency) — location: [1505](kindle://book?action=open&asin=B08J5QZPNC&location=1505) ^ref-3219

---
Consider a toll plaza on a highway. Utilization can be defined as how many tollbooths were busy servicing a car. Utilization at 100% means you can’t find an empty booth and must queue behind someone (saturation). If I told you the booths were at 40% utilization across the entire day, could you tell me whether any cars had queued at any time during that day? They probably did during rush hour, when utilization was at 100%, but that isn’t visible in the daily average. — location: [1815](kindle://book?action=open&asin=B08J5QZPNC&location=1815) ^ref-59512

---
Appendix A is an example USE method checklist for Linux systems, — location: [1880](kindle://book?action=open&asin=B08J5QZPNC&location=1880) ^ref-63211

---
Utilization beyond 60% can be a problem for a couple of reasons: depending on the interval, it can hide short bursts of 100% utilization. Also, some resources such as hard disks (but not CPUs) usually cannot be interrupted during an operation, even for higher-priority work. — location: [1894](kindle://book?action=open&asin=B08J5QZPNC&location=1894) ^ref-26436

---
If the request rate has been steady but the request duration has increased, it points to a problem with the architecture: the service itself. If both the request rate and duration have increased, then the problem may be one of the load applied. This can be further investigated using workload characterization. — location: [1933](kindle://book?action=open&asin=B08J5QZPNC&location=1933) ^ref-1359

---
Apart from identifying issues, workload characterization can also be input for the design of simulation benchmarks. — location: [1956](kindle://book?action=open&asin=B08J5QZPNC&location=1956) ^ref-27783

---
Drill-down analysis starts with examining an issue at a high level, then narrowing the focus based on the previous findings, discarding areas that seem uninteresting, and digging deeper into the interesting ones. — location: [1966](kindle://book?action=open&asin=B08J5QZPNC&location=1966) ^ref-52226

---
Netflix Atlas: — location: [1986](kindle://book?action=open&asin=B08J5QZPNC&location=1986) ^ref-10094

---
Static performance analysis can be performed when the system is at rest and no load is applied. — location: [2089](kindle://book?action=open&asin=B08J5QZPNC&location=2089) ^ref-34045

---
Micro-benchmarking tests the performance of simple and artificial workloads. This differs from macro-benchmarking (or industry benchmarking), which typically aims to test a real-world and natural workload. — location: [2120](kindle://book?action=open&asin=B08J5QZPNC&location=2120) ^ref-28128

---
iperf(1), — location: [2123](kindle://book?action=open&asin=B08J5QZPNC&location=2123) ^ref-24518

---
Don’t do it. Do it, but don’t do it again. Do it less. Do it later. Do it when they’re not looking. Do it concurrently. Do it more cheaply. — location: [2140](kindle://book?action=open&asin=B08J5QZPNC&location=2140) ^ref-19040

---
Then there was the man who drowned crossing a stream with an average depth of six inches. — location: [2455](kindle://book?action=open&asin=B08J5QZPNC&location=2455) ^ref-9617

---
summary-since-boot values are available from the operating system, — location: [2511](kindle://book?action=open&asin=B08J5QZPNC&location=2511) ^ref-44063

---
KernelShark — location: [2577](kindle://book?action=open&asin=B08J5QZPNC&location=2577) ^ref-46238

---
Trace Compass — location: [2577](kindle://book?action=open&asin=B08J5QZPNC&location=2577) ^ref-41258

---
Workloads that perform frequent I/O, such as web servers, execute mostly in kernel context. Workloads that are compute-intensive usually run in user mode, uninterrupted by the kernel. — location: [2736](kindle://book?action=open&asin=B08J5QZPNC&location=2736) ^ref-19377

---
Switching between user and kernel modes is a mode switch. — location: [2752](kindle://book?action=open&asin=B08J5QZPNC&location=2752) ^ref-42268

---
interrupt service routine (ISR) — location: [2810](kindle://book?action=open&asin=B08J5QZPNC&location=2810) ^ref-13038

---
interrupt service requests (IRQs) — location: [2817](kindle://book?action=open&asin=B08J5QZPNC&location=2817) ^ref-31446

---
The user-level stack of the blocked thread does not change for the duration of a system call, as the thread is using a separate kernel-level stack while executing in kernel context. — location: [2963](kindle://book?action=open&asin=B08J5QZPNC&location=2963) ^ref-26691

---
systemd-analyze(1) — location: [3400](kindle://book?action=open&asin=B08J5QZPNC&location=3400) ^ref-33202

---
kernel page table isolation (KPTI) — location: [3402](kindle://book?action=open&asin=B08J5QZPNC&location=3402) ^ref-62605

---
Profiling tools, or profilers, often use 99 Hz instead of 100 Hz to avoid sampling in lockstep with target activity, which could lead to over- or undercounting. — location: [3722](kindle://book?action=open&asin=B08J5QZPNC&location=3722) ^ref-53241

---
Monitoring software and agents for Linux include: — location: [3799](kindle://book?action=open&asin=B08J5QZPNC&location=3799) ^ref-49613

---
Performance Co-Pilot (PCP): — location: [3800](kindle://book?action=open&asin=B08J5QZPNC&location=3800) ^ref-34768

---
Prometheus: — location: [3801](kindle://book?action=open&asin=B08J5QZPNC&location=3801) ^ref-17802

---
collectd: — location: [3803](kindle://book?action=open&asin=B08J5QZPNC&location=3803) ^ref-25735

---
The contents of /proc are documented in the proc(5) man page and in the Linux kernel documentation: Documentation/filesystems/proc.txt [Bowden 20]. Some parts have extended documentation, such as diskstats in Documentation/iostats.txt and scheduler stats in Documentation/scheduler/sched-stats.txt. Apart from the documentation, you can also study the kernel source code to understand the exact origin of all items in /proc. It can also be helpful to read the source to the tools that consume them. — location: [3956](kindle://book?action=open&asin=B08J5QZPNC&location=3956) ^ref-63547

---
Documentation/accounting/delay-accounting.txt: — location: [3997](kindle://book?action=open&asin=B08J5QZPNC&location=3997) ^ref-21572

---
It is documented in the sock_diag(7) man page. — location: [4019](kindle://book?action=open&asin=B08J5QZPNC&location=4019) ^ref-52508

---
Documentation/trace/tracepoints.rst. — location: [4145](kindle://book?action=open&asin=B08J5QZPNC&location=4145) ^ref-1110

---
Documentation/kprobes.txt. — location: [4223](kindle://book?action=open&asin=B08J5QZPNC&location=4223) ^ref-7013

---
Documentation/trace/uprobetracer.rst. — location: [4255](kindle://book?action=open&asin=B08J5QZPNC&location=4255) ^ref-29112

---
USDT Documentation — location: [4283](kindle://book?action=open&asin=B08J5QZPNC&location=4283) ^ref-64353

---
performance monitoring counters (PMCs). — location: [4288](kindle://book?action=open&asin=B08J5QZPNC&location=4288) ^ref-3051

---
CPU performance counters (CPCs), performance instrumentation counters (PICs), and performance monitoring unit events (PMU events). — location: [4289](kindle://book?action=open&asin=B08J5QZPNC&location=4289) ^ref-7118

---
PMCs Documentation — location: [4358](kindle://book?action=open&asin=B08J5QZPNC&location=4358) ^ref-7252

---
Simultaneous multithreading — location: [6011](kindle://book?action=open&asin=B08J5QZPNC&location=6011) ^ref-12597

---
Intel processors, defines processor performance states (P-states) and processor power states (C-states) [ACPI 17]. — location: [6151](kindle://book?action=open&asin=B08J5QZPNC&location=6151) ^ref-29694

---
The access time for the Level 1 cache is typically a few CPU clock cycles, and for the larger Level 2 cache around a dozen clock cycles. Main memory access can take around 60 ns (around 240 cycles for a 4 GHz processor), and address translation by the MMU also adds latency. — location: [6240](kindle://book?action=open&asin=B08J5QZPNC&location=6240) ^ref-53656

---
Another characteristic of CPU caches is their cache line size. This is a range of bytes that are stored and transferred as a unit, improving memory throughput. — location: [6258](kindle://book?action=open&asin=B08J5QZPNC&location=6258) ^ref-41373

---
Memory may be cached in multiple CPU caches on different processors at the same time. When one CPU modifies memory, all caches need to be aware that their cached copy is now stale and should be discarded, so that any future reads will retrieve the newly modified copy. — location: [6263](kindle://book?action=open&asin=B08J5QZPNC&location=6263) ^ref-62903

---
In Linux, time sharing is driven by the system timer interrupt by calling scheduler_tick(), which calls scheduler class functions to manage priorities and the expiration of units of CPU time called time slices. Preemption is triggered when threads become runnable and the scheduler class check_preempt_curr() function is called. Thread switching is managed by __schedule(), which selects the highest-priority thread via pick_next_task() for running. Load balancing is performed by the load_balance() function. — location: [6412](kindle://book?action=open&asin=B08J5QZPNC&location=6412) ^ref-33662

---
My suggestion is to use the following, in this order: performance monitoring, the USE method, profiling, micro-benchmarking, and static performance tuning. — location: [6492](kindle://book?action=open&asin=B08J5QZPNC&location=6492) ^ref-19639

---

What is the CPU utilization system-wide? Per CPU? Per core? How parallel is the CPU load? Is it single-threaded? How many threads? Which applications or users are using the CPUs? How much? Which kernel threads are using the CPUs? How much? What is the CPU usage of interrupts? What is the CPU interconnect utilization? Why are the CPUs being used (user- and kernel-level call paths)? What types of stall cycles are encountered? — location: [6557](kindle://book?action=open&asin=B08J5QZPNC&location=6557) ^ref-21750

---
