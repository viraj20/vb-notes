
1. What is the block size of any EBS volume. From fdisk -l command we can see the sector size to be 512bytes. According to the list-changed-blocks aws cli command the block size is 512kb
3. We have a volume which is 600Gb in size the avg write is around 600Kb/s from iostat output. We had setup taking snapshot every 6 hour for that volume. When we compared the snapshot for two consecutive instances the difference came out to be 230Gb. If we consider the avg write of 600Kb/s the difference for 6 hours should be (600kb/s*86400sec in a day)/1024/1024/4 ~12GB.
4. Can we assume that the garbage collection, writes for EBS gp3 volume would work like any other SSDs?
5. In that case when we take snapshots are the blocks which are invalid considered while taking a snapshot?