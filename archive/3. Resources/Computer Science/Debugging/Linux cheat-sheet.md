```Shell
curl -sS  -w 'Total: %{time_total}s\n' -D - https://lk.bookmyshow.com/sri-lanka --header 'CF-Device-Type: mobile' -o /dev/null
```
```shell
 ngrep -Wbyline -q 'HTTP'  not src host 169.254.169.254
```
```Shell
grep  -rnw "./" -e "arrDataInCache[1]"
```
```bash
$ sudo find . -xdev -type f | cut -d "/" -f 2 | sort | uniq -c | sort -n
```

```bash
ngrep  -W byline -q '.*' port 5001
```
```bash
ngrep  -W byline -q '.*HTTP' net 10.28.0.237
```


``` get process with threads
ps -eLf
top and then press f
```


Inodes

find -d -maxdepth 1 -mtime +60 -exec rm -rf {} \;

du --inodes --one-file-system ./build-02096 | sort --numeric-sort


asinfo -v "log/" -l

asinfo -h 127.0.0.1 -p 3000 -v "log-set:id=0;query=debug"

asinfo -h 127.0.0.1 -v "set-config:context=namespace;id=ofp;enable-benchmarks-storage=true"


asinfo -v 'scan-abort:id=8563370910462734123'

```
apt list --installed | grep linux-image



```


Files

filetop
cachestat
opensnoop
latencytop