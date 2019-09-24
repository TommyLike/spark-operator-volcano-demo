# spark-operator-volcano-demo
This repo used to demonstrate the features that volcano can bring to spark operator.

# Requirements:
1. go.
2. git.
3. kubectl.

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
1. **pod-delay-creation**: demonstrates that volcano can block driver pod from creating when there
   is not enough resource for the whole spark application in cluster.
2. **queue**: demonstrates that all cluster resources are distributed to different queues and
   spark application is bound to one specific queue.
3. **priorityClass**: demonstrates that spark application with higher priority will get scheduled first.
