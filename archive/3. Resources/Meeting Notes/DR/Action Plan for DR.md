
# Goals
- Move all the application components from one region to another
- Components to consider
	- Databases
		- Mongo
		- Maria
		- Redis
		- Aerospike
		- MSSql
	- RabbitMQ
	- Kafka
	- EKS
	- Whatsapp

https://bookmyshow.slack.com/archives/CKP0XP884/p1714110947049029

# Strategy

- There will be one VPC already created in the Hyderabad region
- The snapshots of the VMs would be taken and kept in sync with the Hyderabad region
- During a DR situation, on the press of one button/trigger, new db instances would be spawned in the Hyderabad region. These new instances would use the snapshots which are already kept in sync across the regions.
- The snapshots would have a retention policy.
- 
-  

## Database Level
- Pros
- Cons
## Tribe Level
- Pros
- Cons
## All at once


Finally there are two main approaches for DR
1. AWS backup
	1. Approach
		Pros:
		Cons:
1. Appranix
		Pros:
		Cons:


## Phase 1




**Questions based on discussions with AWS** 
- better way for rds backup?
- cost for RDS strategy
- Logging in AWS?



- Check if snapshot actully happens in 15mins?
- 
- latency?? services are also there?
- hard coding ip addresses in the application code?
- 
- Fast snapshot restore?
- service quota and limit increase in the DR region
- similar instance family is available


- Use Trusted Advisor for well architected framework


- point in time snapshots RDS backup and AWS Backup
- 
  
- Cost
- ECR?
- RDS with AWS backup?
- Fast snapshot restore cost? 0.75
- 