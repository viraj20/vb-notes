Introducing Storage engine
* What is a storage engine? 
* Forms of block IO 
* Data structures for a storage engine 
* Role of B+Tree in MongoDB and Postgres
LSM 
* Understanding the LSM tree and its components 
* Tradeoffs between LSM tree and B+tree 
* Building Segmented Write-ahead log 
* Introducing memtable based on ConcurrentHashMap 
* Building Memtable with "put" and "get" 
* Role of LSM-tree in BadgerDB 
* Implementation of Z-set in Redis 
SSTable and Bloom filter x
* Introducing SSTable 
* Converting Memtable to SSTable 
* Introducing Bloom filter 
* Writing a bloom filter and attaching it to SSTable
Compaction 
* Searching in SSTable 
* Introducing Compaction 
* Connecting all the dots in our storage engine