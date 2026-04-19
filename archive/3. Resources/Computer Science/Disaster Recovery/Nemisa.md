- Multi account, iam
	- EC2
	- EBS
	- RDS
	- S3
	- LB
	- EFS
	
- Will have to create a Backup Group with the logical group of services that needs to be backed up
- EKS 
	  Backup of the cluster resources will have to be self-managed
- Route53 is not yet supported, so will have to handle it ourselves
- 20-40 mins the users should be able to use the apps
- NAT Gateway, its possible to set a user defined IP address
- LB DNSes will be newly created will have to update that everywhere
- Certs need to be present in the DR region
- VPC tunnels are not supported
  
  Application Policy vs AWS Service??


Cluster contents backed up?
tunnel
20mins
certs need to be present

public IP address

15 mins
Eks 20 mins(max 150 at a time)

LB DNS
ECR
S3 buckets
