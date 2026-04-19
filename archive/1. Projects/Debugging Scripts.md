---
created_date: 2024-01-02
start_date: 2024-01-02
end_date: 2024-01-12
status: Not Started
progress: 0
type: work
dri:
  - "[[Viraj Bharvada]]"
---

---
# Why?
- While debugging issues, there are certain things that are required by the on call SRE, like connections, tcpdump, basic linux monitoring, etc.
- Having a common script that can do this would help in quicker resolution of the issues.
- In future this can be automated to generate a report when ever an alert is generated. This will help the tech support team quickly identify what the issue exactly is.
- This can be used to fix issues in future
- 
# Tasks

# Research

# Discussions / Meetings
- The script should be extensible, where new features can be added as and when required.
- Should be a tool that would be easy to use and integrate with slack in the future.
- Should be possible to write the scripts in any language
- Following can be considered for the scripts
	1. heapdump
		- Check support for different languages
	2. flamegraph 
	3. connections
	4. utilisation
	5. saturation
	6. error
	7. debug tools
	8. tcpdump
	9. input based on what you want
	10. disk stats
	11. RAM
	12. CPU
	13. K8s events
	14. Databases also
	15. Crash Loop Back off Pods
	16.  app runtime metrics
- Running the script as a k8s job to generate a report can be taken up in second phase
- 
## Approaches
- Try to start a different debug container that can get all the details

- Create a wrapper that will be responsible to call all other binaries in different languages
- The wrapper will be responsible to call the other binarires in a given order based on the issue that is being debugged
	- For Eg: if the pod is in a crash loop back off state then first get the exit code and the reason for the pod to be in that state
	- Then based on that try to get the logs of the previously crashed container 
	- And then create a report.
- the wrapper should have a custom input where user defined scripts would be called, that is the name of the script and order can be decided by the user running the script
- This wrapper would be containerized and would have the input of either the alert that was fired or the custom input
- Once this input is received the wrapper would call the appropriate runbook to debug the issue and generate the report
- The input taken would be in json by the wrapper.
- The wrapper would be responsible for converting the input and output from the script that was called
- Should check whether we should give the functionality to execute one one command in the wrapper or execute the entire shell script????
	- One by One Command
		- The processing will have to be done in the wrapper
	- Run entire scrip
		- The processing will be done in the child process which is the shell script
- Rather write a wrapper that can execute both commands and an entire script
- 
There can be three stages to execute shell commands
1. Run the command
2. Then a parser stage that can try to make sense of the output that is received from the 1st command
3. Create an output stage where we can create the output for the report that would be download 
4. 


There will be a module to execute following
1. shell scripts
2. ebpf
3. kubernetes
4. prometheus
5. apm







There would be another wrapper binary that will be responsible for executing the starting the debug container on the appropriate VM or the eks node. Also it should be possible to run the debugging commands manually to debug a specific issue.



1. Create a container that would execute a shell command and create the report in. a file. 
2. Write the wrapper binary that will ensure that the container would start on the correct node and execute that shell and generate the report
	1. This wrappper would have the following commands
	   <app_name> <commands> <flags>
			<commands>
			- Debug mode <this will generate a report based on the runbook>
			- Fix <This command can be used to fix issues>
			- TcpDump mode <which can generate the tcpdump from the ec2 instance or pods>
			- Flame <which can generate the flame graph from the pod or ec2>
			- runbook
			- manual mode <This will create a container with all the debug tools and ssh into that container> 
			- There can be a possibility of taking input directly from a tcp pipe in similar format and perform the operations.



# Conclusion







