
- Rollback cases
	- Revert the configmap as well
- check if only two pods are running for the load balancer. Ensure all pods won't be tagged to that they don't get deleted
- manual stop cases
- final deployment stage check
- What we finally did was created a bamboo plan that would in the 
	- build phase just create artefacts of the config file that would be used in the deploy phase
	- In the deploy phase we wrote a script to apply the changes of that config to a config map in Kubernetes. once that is done restarts the Haproxy pods, make sure the pods are up and then cleanup the old pods.
	- There is an approval script also which was written to make sure that the changes are approved by peers before it is deployed to production cluster. This works as a first line of defence to avopid pushing wrong changes to prod.
