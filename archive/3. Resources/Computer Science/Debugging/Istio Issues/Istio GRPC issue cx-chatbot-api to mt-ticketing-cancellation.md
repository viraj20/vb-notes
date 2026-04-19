```log
{\"code\":14,\"details\":\"No connection established\",\"metadata\":{\"internalRepr\":{},\"options\":{}}}
```
``

mt-ticket-cancellation-app-production.movies

in-mt-ticket-cancellation-app.prod.aps.bookmyshow.org:5001


10.28.22.149 cx-chatbot-app-


10.28.15.237


MacBook-Pro-10:SRE viraj.bharvada$ kubectl logs -f cx-chatbot-app-production-7dc77bb4f6-67dm6 -n custexp -c istio-proxy | grep mt
[2023-04-10T11:12:50.277Z] "- - -" 0 - - - "-" 407 0 1 - "-" "-" "-" "-" "10.77.31.99:5001" PassthroughCluster 10.28.22.149:48586 10.77.31.99:5001 10.28.22.149:48576 mt-ticket-cancellation-app-production.movies -
[2023-04-10T11:13:00.894Z] "- - -" 0 - - - "-" 407 0 0 - "-" "-" "-" "-" "10.77.31.99:5001" PassthroughCluster 10.28.22.149:38496 10.77.31.99:5001 10.28.22.149:38490 mt-ticket-cancellation-app-production.movies -
[2023-04-10T11:13:05.880Z] "- - -" 0 - - - "-" 407 0 0 - "-" "-" "-" "-" "10.77.31.99:5001" PassthroughCluster 10.28.22.149:54082 10.77.31.99:5001 10.28.22.149:54078 mt-ticket-cancellation-app-production.movies -



[2023-04-10T12:09:04.933Z] "POST /TicketCancellation.TicketCancellationService/GetMemberCancellationCount HTTP/2" 200 - via_upstream - "-" 28 148 2 1 "-" "grpc-node-js/1.3.7" "89b5fed5-f5bc-9b14-a9ce-5babf814976a" "mt-ticket-cancellation-app-production.movies:5001" "10.28.15.237:5001" outbound|5001||mt-ticket-cancellation-app-production.movies.svc.cluster.local 10.28.0.160:50590 10.77.31.99:5001 10.28.0.160:54810 - -


Cause
connection was secure instead of insecure for this call from cx
