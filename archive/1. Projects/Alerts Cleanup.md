---
created_date: 2024-05-08
start_date: 
end_date: 
status: 
progress: 
type: 
dri:
---

---
# Why?

- Alert Fatigue is a very big problem
- There are a lot of alert channels to check.
- Most of the current alerts have no action
- This is causes problems like, techsupport teams needs to continuously monitor the dashboards
- Long times to detect when actual issues happen.
- Actual issues are either reported by users or accedentaly detected, which becomes reactive instead of pro active.
- 

# Tasks

Plan
- Clean up channels one by one
- the main reason for this happening is that we have setup generic alerts, and not alerts for specific use cases. What that does is there are always cases where false positive alerts are created.
- For Prometheus alerting where most of the alerts are self configured, we can create a CI/CD way to automate the alerting so that devs can setup the required alerts.
- Best would be to have a user interface, but would require a lot of effort to create, maintain and automate.


- Try to include more black box testing which will alert on symptoms
- 

# Research

- https://docs.google.com/document/d/199PqyG3UsyXlwieHaqbGiWVa8eMWi8zzAn0YfcApr8Q/edit#heading=h.fs3knmjt7fjy
	- Over-monitoring is a harder problem to solve
	- Pages should be urgent and actionable
	- Classify alerts into 
		- Availablity
			- no 500
			- no hung requests
			- Anything that breaks the core service in some way should be considered unavailability
		- latency
		  
		- correctness
		- Feature specific problem
	- Symptoms are a better way to capture more problems
	- Weekly review of the alerts

Blackbox Testing
- https://github.com/prometheus/blackbox_exporter
Rule Validating
	- https://blog.cloudflare.com/monitoring-our-monitoring
# Discussions / Meetings



# Conclusion







