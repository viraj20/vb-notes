```log
kubernetes.container_image:registry.bookmyshow.org/pg/pg-order-summary-app:release_213kubernetes.host:ip-10-28-12-252.ap-south-1.compute.internalkubernetes.labels.app:pg-order-summary-appkubernetes.labels.release:pg-order-summary-app-productionkubernetes.namespace_name:pgkubernetes.pod_name:pg-order-summary-app-production-7b557f4d88-f97scmessage.code:text:Error occurred while fulfilling members requestmessage.app:order-summary-appmessage.caller:GetMemberProfilemessage.callerLevel:1message.description:Error occurred while fulfilling members requestmessage.file:/go/src/order-summary-app/src/sal/grpc/members.gomessage.host:pg-order-summary-app-production-7b557f4d88-f97scmessage.line:31message.reference:{"payload":"{\"stackTrace\":\"rpc error: code = DeadlineExceeded desc = context deadline exceeded\
\"}"}message.ts:2023-04-03T13:03:46.309Zmessage.type:warningdc:aps
pg
```
The error here was that the timeout configure was 10ms increasing it to 100ms fixed the issue. The issue would have been mainly coz of more time used by istio proxy which would have increased the overall repsonse time for the app 
