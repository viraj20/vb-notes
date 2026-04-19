
```
awk '{for (i=1; i<=NF; i++) printf strtonum("0x" $i) (i==NF?"\n":" ")}' /proc/net/softnet_stat | column -t
```
net.core.netdev_max_backlog = 2000

 3rd column
sysctl net.core.netdev_budget_usecs net.core.netdev_budget


```
tc -s qdisc show dev enp1s0
```

ip link set dev enp1s0 txqueuelen 2000




iperf3 --server

iperf3 --time 60 --zerocopy --client 192.0.2.1



net.ipv4.tcp_rmem = 4096  131072  6291456
net.ipv4.tcp_wmem = 4096  16384   4194304



https://www.alibabacloud.com/blog/tcp-syn-queue-and-accept-queue-overflow-explained_599203


https://docs.redhat.com/en/documentation/red_hat_enterprise_linux/8/html/monitoring_and_managing_system_status_and_performance/tuning-the-network-performance_monitoring-and-managing-system-status-and-performance#detecting-packet-drops_tuning-udp-connections