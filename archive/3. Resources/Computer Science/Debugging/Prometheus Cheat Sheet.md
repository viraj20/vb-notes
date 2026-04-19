Critical- [http://prometheus.bookmyshow.org/graph?g0.expr=sum(max_over_time(ALERTS%7Bseverity%3D%22[…]tab=1&g0.stacked=0&g0.show_exemplars=0&g0.range_input=1h](http://prometheus.bookmyshow.org/graph?g0.expr=sum(max_over_time(ALERTS%7Bseverity%3D%22critical%22%2Calertstate%3D%22firing%22%7D%5B24h%5D))%20by%20(alertname)&g0.tab=1&g0.stacked=0&g0.show_exemplars=0&g0.range_input=1h)  

Warning - [http://prometheus.bookmyshow.org/graph?g0.expr=sum(max_over_time(ALERTS%7Bseverity%3D%22[…]2016%3A08%3A31&g0.moment_input=2023-03-28%2016%3A08%3A31](http://prometheus.bookmyshow.org/graph?g0.expr=sum(max_over_time(ALERTS%7Bseverity%3D%22warning%22%2Calertstate%3D%22firing%22%7D%5B24h%5D))%20by%20(alertname)&g0.tab=1&g0.stacked=0&g0.show_exemplars=0&g0.range_input=2h55m59s978ms&g0.end_input=2023-03-28%2016%3A08%3A31&g0.moment_input=2023-03-28%2016%3A08%3A31)  

Info - [http://prometheus.bookmyshow.org/graph?g0.expr=sum(max_over_time(ALERTS%7Bseverity%3D%22[…]tab=1&g0.stacked=0&g0.show_exemplars=0&g0.range_input=1h](http://prometheus.bookmyshow.org/graph?g0.expr=sum(max_over_time(ALERTS%7Bseverity%3D%22info%22%2Calertstate%3D%22firing%22%7D%5B24h%5D))%20by%20(alertname)&g0.tab=1&g0.stacked=0&g0.show_exemplars=0&g0.range_input=1h)


```
(sum(kube_pod_container_resource_requests{ resource="cpu",job="kube-state-metrics"}) ) 
```
```
delta(kube_horizontalpodautoscaler_status_current_replicas[1d]) >2 
```



