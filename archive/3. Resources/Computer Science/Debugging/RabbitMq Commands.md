
## To rejoin a node back to the cluster
```
rabbitmqctl stop_app
rabbitmqctl reset
rabbitmqctl join_cluster rabbit@rabbit@in-temp-rmq-1.sit.aps1.bookmyshow.org
rabbitmqctl start_app
```


## Considering we need to remove node2 from cluster 

```
rabbitmqctl stop_app on node 2
## From node1 
rabbitmqctl reset --node rabbit@in-rmq-arm-2.prod.aps.bookmyshow.org

```


```
rabbitmqctl cluster_status
```
