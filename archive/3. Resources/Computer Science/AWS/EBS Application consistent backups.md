
Check on how to achieve EBS app consistent backups for our databases like Mongo, MySql, Aerospike, Redis, Elastic Search

- EBS backups are by default crash consistent and not application consistent. It means that the it restores the state as if the power cord if the machine is removed.
- All the contents that are present in the memory, buffers, which are not written to the disk would be lost making it hard to recover and a possibility of data corruption.
- We will have to check how to achieve App consistent backups on an App by App basis

[[Mongo DB]]
- To get a correct snapshot of a running [`mongod`](https://www.mongodb.com/docs/manual/reference/program/mongod/#mongodb-binary-bin.mongod) process, you must have journaling enabled and the journal must reside on the same logical volume as the other MongoDB data files. Without journaling enabled, there is no guarantee that the snapshot will be consistent or valid.
- [Ref](https://www.mongodb.com/docs/manual/core/backups/#:~:text=MongoDB%20Cloud%20Manager%20continually%20backs,replica%20sets%20and%20sharded%20clusters.)
- [monog-consistent-backups](https://n2ws.com/blog/aws-ec2-backup/mongodb-consistent-backup)
- [serverfault link](https://serverfault.com/questions/929242/mongodb-on-aws-ec2-backup-strategy)
[[MySql]]
- _MySQL supports locking and flushing through the_ `_FLUSH TABLES WITH READ LOCK_` _command_
- One consideration when utilizing EBS snapshots for backups is to make sure the MySQL data remains consistent. During an EBS snapshot, any data not flushed from the InnoDB buffer cache to disk will not be captured. There is a MySQL command flush tables with read lock that will flush all the data in the tables to disk and only allow database reads but put a lock on database writes. The lock only needs to last for a brief period of time until the EBS snapshot starts. The snapshot will take a point-in-time capture of all the content within that volume. The database lock needs to be active until the snapshot process starts, but it doesn’t have to wait for the snapshot to complete before releasing the lock.
- [Ref](https://docs.aws.amazon.com/whitepapers/latest/optimizing-mysql-on-ec2-using-amazon-ebs/mysql-backups.html)
[[Aerospike]]
[Backup and Restore ](https://aerospike.com/docs/deploy_guides/aws/backup)
[[Redis]]

[[ElasticSearch]]
- **Taking a snapshot is the only reliable and supported way to back up a cluster.** You cannot back up an Elasticsearch cluster by making copies of the data directories of its nodes. There are no supported methods to restore any data from a filesystem-level backup. If you try to restore a cluster from such a backup, it may fail with reports of corruption or missing files or other data inconsistencies, or it may appear to have succeeded having silently lost some of your data.  
- A copy of the data directories of a cluster’s nodes does not work as a backup because it is not a consistent representation of their contents at a single point in time. You cannot fix this by shutting down nodes while making the copies, nor by taking atomic filesystem-level snapshots, because Elasticsearch has consistency requirements that span the whole cluster. You must use the built-in snapshot functionality for cluster backups.
[Snapshots]([https://www.elastic.co/guide/en/elasticsearch/reference/current/snapshot-restore.html#snapshots-shard-allocation](https://www.elastic.co/guide/en/elasticsearch/reference/current/snapshot-restore.html#snapshots-shard-allocation))
