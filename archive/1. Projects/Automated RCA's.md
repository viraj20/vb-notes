---
created_date: 
start_date: 
end_date: 
status: 
progress: 
type: 
dri:
---

---
# Why?

# Tasks

# Research


IP:  app_name / instance_name


Check if it is a public or private app

Public app
	- Check the traffic pattern on HaProxy
	- Check for HaProxy stats 5xx and queue

Both
- Check for k8s events
- App is running/pending/crashloop
- Check Memory and CPU Utilization
- Check coralogix logs
- 


Infra Debugging

- Check traffic patterns --> Cloudflare/Clevertap
- Check 5xx metrics  --> Prometheus
- Check 5xx logs  --> Coralogix
- Check HaProxy queueing  -> Prometheus
- Check k8s events  --> Coralogix
- Check app status is running in K8s  --> Kubernetes

App Debugging

- Check mem and CPU (utilisation/throttling) utilisation of the Apps  --> Prometheus
- Check coralogix logs  -> Coralogix
- Check APM throughput and response times  -> APM/Elastic 
- Check dependent DBs  --> Backstage dependency
- Check logs with code  --> Stash and Coralogix
- Check the latest changes to the application  --> Coralogix
Future Scope
- Check detailed CPU Debugging with flame graphs
- Check detailed mem debugging with mem dumps
- Possible Fixes

Instance Debugging

- Check mem cpu network and disk for the dbs and compare it with what's provisioned. --> Prometheus
- Check slow queries  --> Coralogix
- Check connection counts  --> Prometheus
- Run scripts to get linux monitoring --> Linux shell


1. Simple Arch 1 node with tools
2. Give a full run book on how to debug
3. 



Impact

    - Check transaction dip --> Prometheus


To Read
# Chain of Thought promt
# RAGs
# LangChain
# 

# Discussions / Meetings

# Conclusion



Prompt engineering

- Lets think step by step






