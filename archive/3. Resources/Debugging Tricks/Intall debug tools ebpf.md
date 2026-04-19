


```
sudo apt install -y zip bison build-essential cmake flex git libedit-dev \
  libllvm12 llvm-12-dev libclang-12-dev python zlib1g-dev libelf-dev libfl-dev python3-setuptools \
  liblzma-dev arping netperf iperf
```


git clone https://github.com/iovisor/bcc.git
mkdir bcc/build; cd bcc/build
cmake ..
make
sudo make install
cmake -DPYTHON_CMD=python3 .. # build python3 binding
pushd src/python/
make
sudo make install
```
bpftrace -e 'BEGIN { printf("hello world\n"); }'
```

- To find the members args of the trace
```
  bpftrace -vl tracepoint:syscalls:sys_enter_openat
```

```
bpftrace -e 'tracepoint:raw_syscalls:sys_enter { @[comm] = count(); }'
```
