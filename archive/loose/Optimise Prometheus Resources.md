
https://blog.cloudflare.com/how-cloudflare-runs-prometheus-at-scale/
https://blog.cloudflare.com/monitoring-our-monitoring/
- There are 3 concepts you need to understand first
- metrics
- timeseries
- sample
Metrics
- It is something that we can observe
Sample
- Sample is the individual value of our metric
Time Series
- With prometheus scrapes the metrics, it adds timestamps and all the other labels to create a time series


the name of the metrics is also stored as a label  name__
So there is not practical distinction between how the data is stored and name of the metric
For example
{__name="cpu_utilization", host="test",cpu="3"}

After this there is a 16bytes of samples stored
8 bytes if float64 and 8 bytes of timestamp

Intitally the time series are stored in memory
we use a hash value of the labels to store the data which is mapped to memSeries

![[Screenshot 2024-09-10 at 11.43.24 PM.png]]


memSeries is the datastricture that stores all the label values as well the chunk the timeseries is stored in

The chunk size is generally of 2 hours with 120 sample.

after every 2 hours the chunks are persisted to disk

The problem that can happen here is that the time series got created and there are no smaples getting appended to it. in that case the time series will stay in memory for one to two hours.


```
go_memstats_alloc_bytes / prometheus_tsdb_head_series
```

![[Screenshot 2024-09-11 at 5.52.18 AM.png]]

2.6 mil
4.48 mil

![[Screenshot 2024-09-22 at 2.10.42 PM.png]]




![[Screenshot 2024-09-22 at 2.10.59 PM.png]]




![[Screenshot 2024-09-22 at 2.11.35 PM.png]]


![[Screenshot 2024-09-22 at 2.11.56 PM.png]]![[Screenshot 2024-09-22 at 2.12.14 PM.png]]