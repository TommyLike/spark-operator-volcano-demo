# Example Guide
1. Create the priority class that used by spark application: `kubectl apply -f priorityclass.yaml`
2. Submit the high and low priority jobs simultaneously: `kubectl apply -f pyspark-pi-priority.yaml`
3. Check the pod's AGE to figure out their schedule time.
```$xslt
pyspark-pi-high-job1-1569292655639-exec-1   1/1     Running   0          42s
pyspark-pi-high-job1-driver                 1/1     Running   0          59s
pyspark-pi-high-job2-1569292655050-exec-1   1/1     Running   0          42s
pyspark-pi-high-job2-driver                 1/1     Running   0          59s
pyspark-pi-high-job3-1569292654992-exec-1   1/1     Running   0          42s
pyspark-pi-high-job3-driver                 1/1     Running   0          60s
pyspark-pi-low-job1-1569292655732-exec-1    1/1     Running   0          35s
pyspark-pi-low-job1-driver                  1/1     Running   0          59s
pyspark-pi-low-job2-1569292655104-exec-1    1/1     Running   0          36s
pyspark-pi-low-job2-driver                  1/1     Running   0          60s
```


