- uptime/top: to check load averages
- PSI: /proc/pressure/cpu

- vmstat with 1 sec interval
- mpstat: for per-cpu check, to identify hot cpus
		- mpstat -P ALL 1
- SAR
	- /etc/default/sysstat to enable
	- -u 
- top: which processes are top cpu consumers
	- atop short lived processes, htop
- pidstat: break down the top cpu into user and system time
	- -p ALL, -t per thread stats
- perf/profile: profile CPU usage stack traces
- perf: Measure IPC as an indicator of cycle based inefficiencies 
- showboost/turboboost: check current cpu clock rates
- dmesg: check for cpu temperature stalled message 
- time
- pmcarch
- tlbstat

- syscall rate
- user-time to sys time ratios
- context switch rate
- interrupt rate

- profiling
	- timer based samping
		  99Hz per CPU to avoid lock-sampling
		  profile file writing can cause I/Os use bpf based profile instead
	-  function tracing
		  higher overhead ~10%

- cycle analysis
