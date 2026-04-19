
![[Screenshot 2024-09-22 at 10.43.56 PM.png]]

Members main received 600K RPM![[Screenshot 2024-09-22 at 10.45.03 PM.png]]

- ![[Screenshot 2024-09-22 at 10.54.54 PM.png]]
- Here we can see the dynamic requests doubled around 11:58
- 
![[Screenshot 2024-09-22 at 11.00.13 PM.png]]



- 11:56 the load balancer mobile-web started to restart
- At 12:06 we increased the replicas to 4 and at 12:17 to 6
- 12:06:37 to 12:18:19 there were more
- ![[Screenshot 2024-09-22 at 11.07.52 PM.png]]
- 
- than 2 lbs running
- ![[Screenshot 2024-09-22 at 11.50.27 PM.png]]

- The load was 6.56 million at 11:56. It scaled to 28 million by 12:00.
- So basically every minute we got 6 million new requests.

# APIs
- /api/v3/mobile/initialize from 11:56 to 12:00 we got 4.45 million per minute out of this 3.73 million were blocked at CF.
- 
![[Screenshot 2024-09-23 at 12.00.38 AM.png]]
- Here we got a 503 error also on the same API. As this api is responsible for signups it would have caused users to fail to open the apps at the time. This time also matches with the lb restarts
- ![[Screenshot 2024-09-23 at 12.03.22 AM.png]]

- Although LB's were restarting the count of 200s was not completely to zero althogh it was significantly lower than 503s
![[Screenshot 2024-09-23 at 12.05.50 AM.png]]

- Checking the origin the 200s almost went to zero. Indicating that the earlier 200s could have been served from cache.
- 



Action Items
- Fix Fluentd config or use some other tool that works. No logs were visible during the event.
- Have an authentication between out clients and servers.
- We could have initialized fault tolerance for init api
- 
