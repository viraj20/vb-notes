Goals:
- Reducing the dependencies from SRE
# On Call:
	##Goals:
		1. Avoid calls by being proactive to solve issues
		2. Try to resolve the issue without any human intervention
		3. Define the priority of the issue
		4. Have all the relevant stakeholders on the call
		5. Have runbooks in place to help the on call engineer
		6. Compulsory RCA after every call
	## Solution
		1. Every p0 alert in prometheus should have a zenduty configured.
		2. Generate a debug repot based on the alert to help the on call engineers
		3. 


Monitoring/Alerting:
1. Runtime metrics
2. whitebox vs blackbox monitoring
3. Effective Dashboards
4. Alert Tickets/Pages
	1. Why
		1. Data Trends
		2. user counts growing
		3. comparing two systems
		4. site faster then last week
		5. debugging
		6. security breaches
5. 4 Golden Signals
	1. Latency
		1. track latency with error codes
	2. Traffic
		1. Measure the demand on each system
	3. Errors
6. Tail Values
7. keep it simple
8. Every page should be actionable and require intelligence
9. Automated responses to pages
10. Parameters
	1. Speed
	2. Retention
11. logs
12. Metrics
13. distributed tracing
14. profiling
15. consistent set of metrics across teams


1. Logs
	1. Lot of unwanted logs
	2. Logs cleanup
	3. Alerting
2. Metrics
	1. Application run time metrics
	2. Awareness
	3. DB queries data
	4. Effective dashboards
3. Tracing
	1. Missing
		1. Without making changes Pixie
		2. Build the confidence by having something reliable in place
4. APM
	1. Stability
	2. Retention ( 1 week )
	3. 
5. Profiling
	1. Missing



	Debugging

CI/CD:
1. 

Cloud:
1. 

Automation:
1. 

Infra Governance:
1. 

Developer Productivity:


# Problem Statements

1. No way currently to track each service's performance and how it impacts the entire mesh of micro services
	1. SLA/SLI/SLO
2. During an issue it takes very long to identify issues, no way to track that as well. A lot of to and fro happens on the calls
	1. Distributed Tracing
	2. Debugging Scripts ***
	3. Monitoring Reliability - APM, Prometheus, Grafana, Logs ***
	4. Better Awareness of Tools
	5. 
3. Resource optimisations needs to be done every quarter
4. Scaling up and scaling down databases during movie releases
5. Proper way to manage AWS resources
6. Usage of Canary Deployments and other Istio features
	1. It has to be very easy to use and get started with, otherwise its difficult for everyone to start using it.
	2. Use Istio for all the traffic that is flowing through the infra
	3. Istio Metrics, can also help for SLA, SLI, SLO
	4. mTLS
7. White Labelling Solutions
8. Rostering System
9. CI/CD

 # What can be made better
 1. Automated Tracing without instrumentations
 2. Disaster Recovery ***
 3. Dev Productivity
	 1. Easy Testing Env
 4. Benchmarks
 5. AI/Ops
	 1. Predicting the load well in advance
	 2. Log Analysis using AI
	 3. New deployment analysis using AI
 6. 




