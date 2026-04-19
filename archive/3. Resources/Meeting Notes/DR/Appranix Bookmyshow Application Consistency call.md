---
date: 2024-01-16
name: Appranix Bookmyshow Application Consistency call
---

Date:  2024-01-16
Attendees:[[Avani Singhal]]
Projects: [[1. Projects/Disaster Recovery|Disaster Recovery]]
---

# Agenda
1. Discuss on how to achieve App consistency with Appranix
2. Doubts we had on the recoveries we had tried
# Discussion notes
- They can proved a resource level hook which can be triggered pre snapshot and post snapshot
- it would take approx 5secs
- If it fails then also we can call the post snapshot hook
- There is a case of exponential backoff which can take around 25secs
- Need 

- For most of the cases there would be some application function that would stop the writes then we can trigger the snapshots and start the writes again
- RDS handles this on when it takes the snapshots.


 - For Elastic search it is possible to take ES snapshot and then take the snapshot of the disk.
 - We can create different read replicas and take snapshots from those disks.


- 
# Questions??
- [ ] Can the same Key be attached to the VM
	- Can be done, will be released in future release in one Qtr
- [ ] what will happen if the hosted zone is already created
	- 
- [ ] ips pattern was different in existing vpc
	- 
- [ ] Any better way to give the mappings
	- To check tag mapping is possible
- [ ] Yaml/APIs configurations possible?
	- Will take couple of qtrs
- Encrypted Disks
# Action items
- [ ] #ToDo #t1 Need to try out https://aws.amazon.com/blogs/compute/automating-the-creation-of-consistent-amazon-ebs-snapshots-with-amazon-ec2-systems-manager-part-1/
- [ ] #ToDo #followup Nitya to share the analysis of why the snapshots failed ➕ 2024-01-16
- [ ] 


