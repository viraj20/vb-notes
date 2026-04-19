CAP Theorem

Active/Passive
Backup and Restore
- RPO in hours RTO 24h
Pilot Light
- RPO in minutes RTO hours
Warm Standby scale is not equal to primary region
- App are running

Active/Active
- single writer multiple reader async replication
	- app should tolerate read after write
- single writer multiple reader sync replication
	- latency
- dual writes
	- app has to take care of data
	- atomicity in the app
- multi writer and multi reads
![[Screenshot 2023-05-19 at 3.18.45 PM.png]]