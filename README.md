# spark-operator-volcano-demo
This repo used to demonstrate the features that volcano can bring to spark operator. It builds the demo environment via
kind with 1 control plane and 4 workers.

# Requirements:
1. go.
2. git.
3. docker
4. kubectl.

# Install
```$xslt
mkdir -p ${GOPATH}/sr/github.com/tommylike
cd ${GOPATH}/sr/github.com/tommylike
git clone https://github.com/TommyLike/spark-operator-volcano-demo
cd spark-operator-volcano-demo
make install
```
# Examples
All of the related demos are located in `demos` folder.
 
**NOTE:** some demos assume the host instance do (and only) have 4 Cores, if the environment
is different, the expected behaviour would change.
1. **pod-delay-creation**: demonstrates that volcano can block driver pod from creating when there
   is not enough resource for the whole spark application in cluster.
2. **queue**: demonstrates that all cluster resources are distributed to different queues and
   spark application is bound to one specific queue.
3. **priorityClass**: demonstrates that spark application with higher priority will get scheduled first.
4. **more demos** will be added...

# Links
1. Official website [github](https://github.com/volcano-sh/volcano)
2. More demo and examples [here](https://github.com/volcano-sh/volcano/tree/master/example)
