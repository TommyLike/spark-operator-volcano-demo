# Example Guide
1. Submit the normal job first via command: `kubectl apply -f pyspark-pi-normal-job.yaml`
2. Submit the delay job when the normal jobs are running. `kubectl apply -f pyspark-pi-delay-job.yaml`
3. The delay job would be blocked since there is not enough resource left now.
```$xslt
pyspark-pi-delay-job-driver                   0/1     Pending   0          5s
pyspark-pi-normal-job1-1569291526064-exec-1   1/1     Running   0          16s
pyspark-pi-normal-job1-driver                 1/1     Running   0          26s
pyspark-pi-normal-job2-1569291526081-exec-1   1/1     Running   0          16s
pyspark-pi-normal-job2-driver                 1/1     Running   0          26s
```
4. delay job would start only when normal job finished:
```
pyspark-pi-delay-job-driver     1/1     Running     0          26s
pyspark-pi-normal-job1-driver   0/1     Completed   0          47s
pyspark-pi-normal-job2-driver   0/1     Completed   0          47s
```


