downstream --> Istio-proxy --> upstream
Filter 
	Each fitler is usually tied up with a single functionality that may have an impact on the request/data
Cluster
	An abstraction for UPSTREAM
	
```
istioctl proxy-config cluster -n custexp cx-chatbot-app-production-6dc475cbdd-bvt96.custexp
```
```
istioctl proxy-config listeners cx-chatbot-app-production-6dc475cbdd-bvt96.custexp -n custexp
```
```
istioctl proxy-config listeners cx-chatbot-app-production-6dc475cbdd-bvt96.custexp -o json --address 0.0.0.0 --port 5001
```
```
istioctl proxy-config routes cx-chatbot-app-production-6dc475cbdd-bvt96.custexp --name 5001 -o json
```

```
kubectl exec my-service-7d846b757c-nh4cn -c istio-proxy -- pilot-agent request GET config_dump |grep -i terminationDrainDuration
```

15006 for inbound traffic
15001 for outbound traffic
Listeners
1. pod ip and port for inbound traffic
2. service ip per each non http port for outbound traffic
3. 0.0.0.0 for each http port for outbound traffic
