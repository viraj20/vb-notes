
1. Kubernetes
2. Databases
3. Performance
4. 

Create a docker container with all the scripts
Run the docker container on the VMs or local laptop (K8s) and get the details for debugging

Kubernetes
- CrashLoopBackOff
	- check previous container logs
- ImagePullBackOff
	- Check which image is giving an error
	- Try to pull that image
- Connections from specific container
	- Number of open connections from container 
	- Match it with all the ENIs and other pod ips

Databases
- Slow Query
- Performance
- CPU / Disk / Memory stats
- Database Logs
- Flame Graphs

Performance
- Anomalies in Traffic patterns
- Flame Graphs
- Application Run times
- Memory Dump
- Thread Dump
- Connections
- USE
 - RED
- tcpdump