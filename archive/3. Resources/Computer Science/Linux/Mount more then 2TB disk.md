 #linux  #disk
Steps
- parted /dev/nvme2n1
	- mklabel gpt
	- unit TB
	- print
	- mkpart primary 0% 100%
	- print
	- quit

## Create LVM
- pvcreate /dev/nvme2n1p1
- vgcreate data /dev/nvme2n1p1
- lvcreate -n mariadb -l 100%FREE data

## Mount Files
- mkfs.xfs /dev/data/mariadb
- /dev/data/mariadb /data3 xfs defaults,noatime,nodiratime 0 0~~~~

```bash
meta-data=/dev/data/mariadb      isize=512    agcount=32, agsize=45055968 blks
         =                       sectsz=512   attr=2, projid32bit=1
         =                       crc=1        finobt=1, sparse=1, rmapbt=0
         =                       reflink=1
data     =                       bsize=4096   blocks=1441790976, imaxpct=5
         =                       sunit=1      swidth=1 blks
naming   =version 2              bsize=4096   ascii-ci=0, ftype=1
log      =internal log           bsize=4096   blocks=521728, version=2
         =                       sectsz=512   sunit=1 blks, lazy-count=1
realtime =none                   extsz=4096   blocks=0, rtextents=0
```
