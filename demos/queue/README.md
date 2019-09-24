# Example Guide
1. Create another queue which has equal weight to the default queue: `kubectl apply -f another-default-queue.yaml`
2. Ensure both queues are existed via command: `kubectl get queues.scheduling.sigs.dev -o yaml`
```$xslt
apiVersion: v1
items:
- apiVersion: scheduling.sigs.dev/v1alpha2
  kind: Queue
  metadata:
    creationTimestamp: "2019-09-23T12:26:03Z"
    generation: 1
    name: default
    resourceVersion: "27783"
    selfLink: /apis/scheduling.sigs.dev/v1alpha2/queues/default
    uid: f3bf33cd-4c7b-437b-a8d2-4ab1e265f9be
  spec:
    weight: 1
- apiVersion: scheduling.sigs.dev/v1alpha2
  kind: Queue
  metadata:
    annotations:
      kubectl.kubernetes.io/last-applied-configuration: |
        {"apiVersion":"scheduling.sigs.dev/v1alpha2","kind":"Queue","metadata":{"annotations":{},"name":"default2"},"spec":{"weight":1}}
    creationTimestamp: "2019-09-24T03:04:21Z"
    generation: 1
    name: default2
    resourceVersion: "120260"
    selfLink: /apis/scheduling.sigs.dev/v1alpha2/queues/default2
    uid: f9e1fd31-42d0-4239-a314-96b9e197c06c
  spec:
    weight: 1
kind: List
metadata:
  resourceVersion: ""
  selfLink: ""
```
2. Submit the jobs that are bound to these two queues: `kubectl apply -f job-on-queue.yaml`
   Check the job status and we will find there is one executor pods get blocked in each queue
   and they will start only when the first job get finished.
```$xslt
pyspark-pi-job1-on-queue-default-1569237312176-exec-1    1/1     Running   0          13s
pyspark-pi-job1-on-queue-default-driver                  1/1     Running   0          28s
pyspark-pi-job1-on-queue-default2-1569237311893-exec-1   1/1     Running   0          13s
pyspark-pi-job1-on-queue-default2-driver                 1/1     Running   0          28s
pyspark-pi-job2-on-queue-default-1569237311927-exec-1    0/1     Pending   0          14s
pyspark-pi-job2-on-queue-default-driver                  1/1     Running   0          28s
pyspark-pi-job2-on-queue-default2-1569237312082-exec-1   0/1     Pending   0          13s
pyspark-pi-job2-on-queue-default2-driver                 1/1     Running   0          28s
```

and
```$xslt
pyspark-pi-job1-on-queue-default-driver                  0/1     Completed           0          60s
pyspark-pi-job1-on-queue-default2-driver                 0/1     Completed           0          60s
pyspark-pi-job2-on-queue-default-1569237311927-exec-1    0/1     ContainerCreating   0          46s
pyspark-pi-job2-on-queue-default-driver                  1/1     Running             0          60s
pyspark-pi-job2-on-queue-default2-1569237312082-exec-1   0/1     ContainerCreating   0          45s
pyspark-pi-job2-on-queue-default2-driver                 1/1     Running             0          60s
```


