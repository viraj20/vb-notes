---
created_date: 2024-01-01
start_date: 2024-01-01
end_date: 2024-02-29
status:
  - Not Started
progress: "0"
type: work
dri:
  - "[[Ketan Bhalakia]]"
  - "[[Viraj Bharvada]]"
---

---
## Why?

## Tasks

## Research

# Discussions / Meetings
## Plan of Migration [[Viraj Bharvada]] [[Ketan Bhalakia]]

####  Scope of Migration
- Setup a new EKS cluster
	- Istio setup
	- karpenter
	- LB controller
	- add-ons
		- kube-proxy
		- vpc-cni
		- ebs-driver
		- corednms
	- bamboo agents
	- haproxy
- Windows servers
	- IS, PS, CS, DS, BO, BTS
	- Jobs server
		- pg-refund
		- galera migration
		- auto-expiry
		- pending failed transactions
		- [[Ketan]] to check if there are more servers for windows
	- Different server for content might also be required
- RMQ servers
- ccms proxy will have to be created
- one new sit common redis
- one new common mongo (to check if sit mongo can be used for this)
- one new aerospike db setup
- Existing DBs that can be used
	- MSSQL1
	- MySql
		- Maria DB
		- Percona used by DE
		  Galera used in transaction flow
- Route53 changes

##  Implementation Details
- Check if the same db's can be used.
- If not we can check if the India SIT dbs can be used.
- otherwise create new dbs where required ina different VPC
- Route53 with the same VPC might not work, will have to check that if there are any tls connections where https and * .bookmyshow.org is used
- 



## Conclusion







