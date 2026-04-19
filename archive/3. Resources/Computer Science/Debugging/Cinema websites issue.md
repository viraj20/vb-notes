```
cinema-websites-app-production-84968bdfcd-4qvfg         2/2     Running   0          23m
cinema-websites-app-production-84968bdfcd-f5nnf         2/2     Running   0          8m10s
lg-bms-stream-tv-app-preprod-6587dd6dd6-p8thq           2/2     Running   0          8h
lg-bms-stream-tv-app-production-7bb44c455d-fhgdr        2/2     Running   0          16h
lg-bms-stream-tv-app-production-7bb44c455d-g4mxh        2/2     Running   0          17h
mobile-web-app-preprod-557fbb5766-5lj6l                 4/4     Running   0          18h
mobile-web-app-production-7f4677f44f-6wwwj              4/4     Running   0          18h
mobile-web-app-production-7f4677f44f-r5k5l              4/4     Running   0          18h
mobile-web-app-production-7f4677f44f-stf76              4/4     Running   0          8h
mobile-web-app-production-7f4677f44f-vpqbn              4/4     Running   0          9h
mobile-web-mailer-cms-app-production-68994844bc-598tm   1/1     Running   0          135m
samsung-bms-stream-tv-app-preprod-7f67759cdd-fr8gw      2/2     Running   0          4h25m
samsung-bms-stream-tv-app-production-667649557d-vsc75   2/2     Running   0          18h










cinema-websites-app-production-68cdb75dc-skpwl          0/2     Pending   0          0s
cinema-websites-app-production-68cdb75dc-skpwl          0/2     Pending   0          0s
cinema-websites-app-production-68cdb75dc-skpwl          0/2     Init:0/1   0          0s
cinema-websites-app-production-68cdb75dc-tgv54          0/2     Pending    0          0s
cinema-websites-app-production-68cdb75dc-tgv54          0/2     Pending    0          0s
cinema-websites-app-production-68cdb75dc-tgv54          0/2     Init:0/1   0          0s
cinema-websites-app-production-glbhh                    0/1     Pending    0          0s
cinema-websites-app-production-glbhh                    0/1     Pending    0          0s
cinema-websites-app-production-glbhh                    0/1     ContainerCreating   0          0s
cinema-websites-app-production-68cdb75dc-tgv54          0/2     PodInitializing     0          1s
cinema-websites-app-production-68cdb75dc-skpwl          0/2     PodInitializing     0          1s
cinema-websites-app-production-glbhh                    0/1     Completed           0          5s
cinema-websites-app-production-glbhh                    0/1     Completed           0          7s
cinema-websites-app-production-glbhh                    0/1     Terminating         0          7s
cinema-websites-app-production-glbhh                    0/1     Terminating         0          7s
cinema-websites-app-production-68cdb75dc-skpwl          0/2     Running             0          9s
cinema-websites-app-production-68cdb75dc-skpwl          1/2     Running             0          9s
cinema-websites-app-production-68cdb75dc-skpwl          2/2     Running             0          11s
cinema-websites-app-production-84968bdfcd-f5nnf         2/2     Terminating         0          8m38s
cinema-websites-app-production-68cdb75dc-tgv54          0/2     Running             0          16s
cinema-websites-app-production-68cdb75dc-tgv54          1/2     Running             0          16s
cinema-websites-app-production-68cdb75dc-tgv54          2/2     Running             0          20s
cinema-websites-app-production-84968bdfcd-4qvfg         2/2     Terminating         0          23m
cinema-websites-app-production-84968bdfcd-f5nnf         1/2     Terminating         0          8m50s
cinema-websites-app-production-84968bdfcd-f5nnf         0/2     Terminating         0          8m54s
cinema-websites-app-production-84968bdfcd-f5nnf         0/2     Terminating         0          8m54s
cinema-websites-app-production-84968bdfcd-f5nnf         0/2     Terminating         0          8m54s
cinema-websites-app-production-84968bdfcd-4qvfg         1/2     Terminating         0          24m
cinema-websites-app-production-84968bdfcd-4qvfg         0/2     Terminating         0          24m
cinema-websites-app-production-84968bdfcd-4qvfg         0/2     Terminating         0          24m
cinema-websites-app-production-84968bdfcd-4qvfg         0/2     Terminating         0          24m
```



```0s          Normal    ScalingReplicaSet              deployment/cinema-websites-app-production                                 Scaled up replica set cinema-websites-app-production-68cdb75dc to 2
0s          Normal    SuccessfulCreate               replicaset/cinema-websites-app-production-68cdb75dc                       Created pod: cinema-websites-app-production-68cdb75dc-skpwl
0s          Normal    Scheduled                      pod/cinema-websites-app-production-68cdb75dc-skpwl                        Successfully assigned mobile-web/cinema-websites-app-production-68cdb75dc-skpwl to ip-10-28-24-84.ap-south-1.compute.internal
0s          Normal    SuccessfulCreate               replicaset/cinema-websites-app-production-68cdb75dc                       Created pod: cinema-websites-app-production-68cdb75dc-tgv54
0s          Normal    Scheduled                      pod/cinema-websites-app-production-68cdb75dc-tgv54                        Successfully assigned mobile-web/cinema-websites-app-production-68cdb75dc-tgv54 to ip-10-28-7-34.ap-south-1.compute.internal
0s          Normal    SuccessfulCreate               job/cinema-websites-app-production                                        Created pod: cinema-websites-app-production-glbhh
0s          Normal    Scheduled                      pod/cinema-websites-app-production-glbhh                                  Successfully assigned mobile-web/cinema-websites-app-production-glbhh to ip-10-28-11-70.ap-south-1.compute.internal
0s          Normal    Pulled                         pod/cinema-websites-app-production-68cdb75dc-skpwl                        Container image "registry.bookmyshow.org/istio/proxyv2:1.15.3" already present on machine
0s          Normal    Created                        pod/cinema-websites-app-production-68cdb75dc-skpwl                        Created container istio-init
0s          Normal    Pulled                         pod/cinema-websites-app-production-68cdb75dc-tgv54                        Container image "registry.bookmyshow.org/istio/proxyv2:1.15.3" already present on machine
0s          Normal    Created                        pod/cinema-websites-app-production-68cdb75dc-tgv54                        Created container istio-init
0s          Normal    Started                        pod/cinema-websites-app-production-68cdb75dc-skpwl                        Started container istio-init
0s          Normal    Started                        pod/cinema-websites-app-production-68cdb75dc-tgv54                        Started container istio-init
0s          Normal    Pulling                        pod/cinema-websites-app-production-glbhh                                  Pulling image "registry.bookmyshow.org/sre/post-deployment-job:latest"
0s          Normal    Pulled                         pod/cinema-websites-app-production-68cdb75dc-tgv54                        Container image "registry.bookmyshow.org/istio/proxyv2:1.15.3" already present on machine
0s          Normal    Created                        pod/cinema-websites-app-production-68cdb75dc-tgv54                        Created container istio-proxy
0s          Normal    Started                        pod/cinema-websites-app-production-68cdb75dc-tgv54                        Started container istio-proxy
0s          Normal    Pulled                         pod/cinema-websites-app-production-68cdb75dc-skpwl                        Container image "registry.bookmyshow.org/istio/proxyv2:1.15.3" already present on machine
0s          Normal    Created                        pod/cinema-websites-app-production-68cdb75dc-skpwl                        Created container istio-proxy
0s          Normal    Started                        pod/cinema-websites-app-production-68cdb75dc-skpwl                        Started container istio-proxy
0s          Normal    Pulling                        pod/cinema-websites-app-production-68cdb75dc-tgv54                        Pulling image "registry.bookmyshow.org/mobile-web/cinema-websites-app:release_29"
0s          Normal    Pulled                         pod/cinema-websites-app-production-glbhh                                  Successfully pulled image "registry.bookmyshow.org/sre/post-deployment-job:latest" in 2.857448929s
0s          Normal    Created                        pod/cinema-websites-app-production-glbhh                                  Created container post-upgrade-job
0s          Normal    Started                        pod/cinema-websites-app-production-glbhh                                  Started container post-upgrade-job
0s          Normal    Completed                      job/cinema-websites-app-production                                        Job completed
0s          Normal    Pulling                        pod/cinema-websites-app-production-68cdb75dc-skpwl                        Pulling image "registry.bookmyshow.org/mobile-web/cinema-websites-app:release_29"
0s          Normal    Pulled                         pod/cinema-websites-app-production-68cdb75dc-skpwl                        Successfully pulled image "registry.bookmyshow.org/mobile-web/cinema-websites-app:release_29" in 86.136809ms
0s          Normal    Created                        pod/cinema-websites-app-production-68cdb75dc-skpwl                        Created container cinema-websites-app
0s          Normal    Started                        pod/cinema-websites-app-production-68cdb75dc-skpwl                        Started container cinema-websites-app
0s          Warning   Unhealthy                      pod/cinema-websites-app-production-68cdb75dc-skpwl                        Readiness probe failed: HTTP probe failed with statuscode: 500
0s          Warning   Unhealthy                      pod/cinema-websites-app-production-68cdb75dc-skpwl                        Liveness probe failed: HTTP probe failed with statuscode: 500
0s          Warning   Unhealthy                      pod/cinema-websites-app-production-68cdb75dc-skpwl                        Readiness probe failed: HTTP probe failed with statuscode: 502
0s          Normal    ScalingReplicaSet              deployment/cinema-websites-app-production                                 Scaled down replica set cinema-websites-app-production-84968bdfcd to 1
0s          Normal    SuccessfulDelete               replicaset/cinema-websites-app-production-84968bdfcd                      Deleted pod: cinema-websites-app-production-84968bdfcd-f5nnf
0s          Normal    Killing                        pod/cinema-websites-app-production-84968bdfcd-f5nnf                       Stopping container istio-proxy
0s          Normal    Killing                        pod/cinema-websites-app-production-84968bdfcd-f5nnf                       Stopping container cinema-websites-app
0s          Normal    Pulled                         pod/cinema-websites-app-production-68cdb75dc-tgv54                        Successfully pulled image "registry.bookmyshow.org/mobile-web/cinema-websites-app:release_29" in 9.605924513s
0s          Warning   Unhealthy                      pod/cinema-websites-app-production-84968bdfcd-f5nnf                       Readiness probe failed: HTTP probe failed with statuscode: 503
0s          Warning   Unhealthy                      pod/cinema-websites-app-production-84968bdfcd-f5nnf                       Readiness probe failed: Get "http://10.28.29.252:15020/app-health/cinema-websites-app/readyz": dial tcp 10.28.29.252:15020: connect: connection refused
0s          Warning   Unhealthy                      pod/cinema-websites-app-production-84968bdfcd-f5nnf                       Readiness probe failed: HTTP probe failed with statuscode: 503
0s          Normal    Created                        pod/cinema-websites-app-production-68cdb75dc-tgv54                        Created container cinema-websites-app
0s          Normal    Started                        pod/cinema-websites-app-production-68cdb75dc-tgv54                        Started container cinema-websites-app
0s          Warning   Unhealthy                      pod/cinema-websites-app-production-68cdb75dc-tgv54                        Readiness probe failed: HTTP probe failed with statuscode: 500
0s          Warning   Unhealthy                      pod/cinema-websites-app-production-84968bdfcd-f5nnf                       Readiness probe failed: HTTP probe failed with statuscode: 503
0s          Warning   Unhealthy                      pod/cinema-websites-app-production-68cdb75dc-tgv54                        Readiness probe failed: HTTP probe failed with statuscode: 500
0s          Warning   Unhealthy                      pod/cinema-websites-app-production-68cdb75dc-tgv54                        Readiness probe failed: HTTP probe failed with statuscode: 502
0s          Warning   Unhealthy                      pod/cinema-websites-app-production-84968bdfcd-f5nnf                       Readiness probe failed: Get "http://10.28.29.252:15021/healthz/ready": dial tcp 10.28.29.252:15021: connect: connection refused
0s          Warning   Unhealthy                      pod/cinema-websites-app-production-84968bdfcd-f5nnf                       Readiness probe failed: Get "http://10.28.29.252:15020/app-health/cinema-websites-app/readyz": dial tcp 10.28.29.252:15020: connect: connection refused
0s          Normal    ScalingReplicaSet              deployment/cinema-websites-app-production                                 Scaled down replica set cinema-websites-app-production-84968bdfcd to 0
0s          Normal    SuccessfulDelete               replicaset/cinema-websites-app-production-84968bdfcd                      Deleted pod: cinema-websites-app-production-84968bdfcd-4qvfg
0s          Normal    Killing                        pod/cinema-websites-app-production-84968bdfcd-4qvfg                       Stopping container istio-proxy
0s          Normal    Killing                        pod/cinema-websites-app-production-84968bdfcd-4qvfg                       Stopping container cinema-websites-app
0s          Warning   Unhealthy                      pod/cinema-websites-app-production-84968bdfcd-f5nnf                       Readiness probe failed: Get "http://10.28.29.252:15021/healthz/ready": dial tcp 10.28.29.252:15021: connect: connection refused
0s          Warning   Unhealthy                      pod/cinema-websites-app-production-84968bdfcd-4qvfg                       Readiness probe failed: Get "http://10.28.20.13:15020/app-health/cinema-websites-app/readyz": dial tcp 10.28.20.13:15020: connect: connection refused
0s          Warning   Unhealthy                      pod/cinema-websites-app-production-84968bdfcd-4qvfg                       Readiness probe failed: HTTP probe failed with statuscode: 503
0s          Warning   Unhealthy                      pod/cinema-websites-app-production-84968bdfcd-f5nnf                       Readiness probe failed: Get "http://10.28.29.252:15021/healthz/ready": dial tcp 10.28.29.252:15021: connect: connection refused
0s          Warning   Unhealthy                      pod/cinema-websites-app-production-84968bdfcd-4qvfg                       Readiness probe failed: HTTP probe failed with statuscode: 503
0s          Warning   Unhealthy                      pod/cinema-websites-app-production-84968bdfcd-f5nnf                       Readiness probe failed: Get "http://10.28.29.252:15020/app-health/cinema-websites-app/readyz": dial tcp 10.28.29.252:15020: connect: connection refused
0s          Warning   Unhealthy                      pod/cinema-websites-app-production-84968bdfcd-f5nnf                       Readiness probe failed: Get "http://10.28.29.252:15021/healthz/ready": dial tcp 10.28.29.252:15021: connect: connection refused
0s          Warning   Unhealthy                      pod/cinema-websites-app-production-84968bdfcd-4qvfg                       Readiness probe failed: HTTP probe failed with statuscode: 503
0s          Warning   Unhealthy                      pod/cinema-websites-app-production-84968bdfcd-4qvfg                       Readiness probe failed: Get "http://10.28.20.13:15020/app-health/cinema-websites-app/readyz": dial tcp 10.28.20.13:15020: connect: connection refused
0s          Warning   Unhealthy                      pod/cinema-websites-app-production-84968bdfcd-4qvfg                       Readiness probe failed: Get "http://10.28.20.13:15021/healthz/ready": dial tcp 10.28.20.13:15021: connect: connection refused
0s          Warning   Unhealthy                      pod/cinema-websites-app-production-84968bdfcd-4qvfg                       Readiness probe failed: Get "http://10.28.20.13:15021/healthz/ready": dial tcp 10.28.20.13:15021: connect: connection refused
0s          Warning   Unhealthy                      pod/cinema-websites-app-production-84968bdfcd-4qvfg                       Readiness probe failed: Get "http://10.28.20.13:15020/app-health/cinema-websites-app/readyz": dial tcp 10.28.20.13:15020: connect: connection refused
0s          Warning   Unhealthy                      pod/cinema-websites-app-production-84968bdfcd-4qvfg                       Readiness probe failed: Get "http://10.28.20.13:15021/healthz/ready": dial tcp 10.28.20.13:15021: connect: connection refused
0s          Warning   Unhealthy                      pod/cinema-websites-app-production-84968bdfcd-4qvfg                       Readiness probe failed: Get "http://10.28.20.13:15021/healthz/ready": dial tcp 10.28.20.13:15021: connect: connection refused
0s          Warning   FailedGetResourceMetric        horizontalpodautoscaler/cinema-websites-app-production                    failed to get memory utilization: did not receive metrics for any ready pods
0s          Warning   FailedGetResourceMetric        horizontalpodautoscaler/cinema-websites-app-production                    failed to get cpu utilization: did not receive metrics for any ready pods
0s          Warning   FailedComputeMetricsReplicas   horizontalpodautoscaler/cinema-websites-app-production                    invalid metrics (2 invalid out of 2), first error is: failed to get memory utilization: did not receive metrics for any ready pods
0s          Warning   Unhealthy                      pod/cinema-websites-app-production-84968bdfcd-4qvfg                       Readiness probe failed: Get "http://10.28.20.13:15021/healthz/ready": dial tcp 10.28.20.13:15021: connect: connection refused
0s          Normal    Killing                        pod/cinema-websites-app-production-84968bdfcd-4qvfg                       Stopping container cinema-websites-app
0s          Warning   FailedKillPod                  pod/cinema-websites-app-production-84968bdfcd-4qvfg                       error killing pod: failed to "KillContainer" for "cinema-websites-app" with KillContainerError: "rpc error: code = Unknown desc = Error response from daemon: No such container: 13111833f8561a8b9a127192b9895eb5a8e37dd3a5a0db05b6daea0441829c32"
0s          Warning   FailedGetResourceMetric        horizontalpodautoscaler/cinema-websites-app-production                    failed to get memory utilization: unable to get metrics for resource memory: no metrics returned from resource metrics API
0s          Warning   FailedGetResourceMetric        horizontalpodautoscaler/cinema-websites-app-production                    failed to get cpu utilization: unable to get metrics for resource cpu: no metrics returned from resource metrics API
0s          Warning   FailedComputeMetricsReplicas   horizontalpodautoscaler/cinema-websites-app-production                    invalid metrics (2 invalid out of 2), first error is: failed to get memory utilization: unable to get metrics for resource memory: no metrics returned from resource metrics API
0s          Warning   FailedGetResourceMetric        horizontalpodautoscaler/cinema-websites-app-production                    failed to get memory utilization: unable to get metrics for resource memory: no metrics returned from resource metrics API
0s          Warning   FailedGetResourceMetric        horizontalpodautoscaler/cinema-websites-app-production                    failed to get cpu utilization: unable to get metrics for resource cpu: no metrics returned from resource metrics API
0s          Warning   FailedComputeMetricsReplicas   horizontalpodautoscaler/cinema-websites-app-production                    invalid metrics (2 invalid out of 2), first error is: failed to get memory utilization: unable to get metrics for resource memory: no metrics returned from resource metrics API
0s          Warning   FailedGetResourceMetric        horizontalpodautoscaler/cinema-websites-app-production                    failed to get cpu utilization: did not receive metrics for any ready pods
0s          Warning   FailedGetResourceMetric        horizontalpodautoscaler/cinema-websites-app-production                    failed to get cpu utilization: did not receive metrics for any ready pods
```