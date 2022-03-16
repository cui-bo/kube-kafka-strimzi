# Simple project allows creating kafka cluster

## Installation tools
1. Install windows chocolatey

    ``https://chocolatey.org/install``

    Chocolatey v0.12.1
	
2. Install Minikube

   ``https://dev.to/sanjaybsm/installing-minikube-kubectl-with-chocolatey-windows-5gc7``
	
    Ou
    
    ``https://redhat-developer-demos.github.io/kafka-tutorial/kafka-tutorial/1.0.x/07-kubernetes.html``
	
    minikube version
    minikube version: v1.25.2
	
    kubectl version
    Client Version: version.Info {Major:"1", Minor:"21", GitVersion:"v1.21.2", GitCommit:"092fbfbf53427de67cac1e9fa54aaa09a28371d7", GitTreeState:"clean", BuildDate:"2021-06-16T12:59:11Z", GoVersion:"go1.16.5", Compiler:"gc", Platform:"windows/amd64"}
	
	
3. Install podman by choco

   ``https://community.chocolatey.org/packages/podman-cli``

    podman -v

   ``C:\ProgramData\chocolatey\lib\podman-cli\tools\podman-v1.8.1-rc1\podman.exe version 1.8.1-rc1``
	
4. Install Minishift
   ``https://github.com/minishift/minishift/releases``


## Configuration environment

### Create new namespace

    $ kubectl create -f create-namespace.yaml

### Create strimzi cluster operator
    $ kubectl create -f create-strimzi-cluster-operator.yaml -n mykafka

### Create kafka cluster
    $ kubectl create -f create-kafka-cluster.yaml -n mykafka

    kafka.kafka.strimzi.io/mycluster created

### Get cluster information
    $ kubectl get pods -n mykafka

    NAME                                         READY   STATUS    RESTARTS   AGE
    kafka-producer                               1/1     Running   0          6m44s
    mycluster-entity-operator-54f44bc9cf-b4cjx   3/3     Running   0          13m
    mycluster-kafka-0                            1/1     Running   0          14m
    mycluster-kafka-1                            1/1     Running   0          14m
    mycluster-kafka-2                            1/1     Running   0          14m
    mycluster-zookeeper-0                        1/1     Running   0          16m
    mycluster-zookeeper-1                        1/1     Running   0          16m
    mycluster-zookeeper-2                        1/1     Running   0          16m
    strimzi-cluster-operator-7599bc57cb-2h6p6    1/1     Running   0          20m

### List all services
    $ kubectl get services -n mykafka

    NAME                         TYPE        CLUSTER-IP       EXTERNAL-IP   PORT(S)                               AGE
    mycluster-kafka-bootstrap    ClusterIP   10.107.137.162   <none>        9091/TCP,9092/TCP,9093/TCP            15m
    mycluster-kafka-brokers      ClusterIP   None             <none>        9090/TCP,9091/TCP,9092/TCP,9093/TCP   15m
    mycluster-zookeeper-client   ClusterIP   10.97.163.190    <none>        2181/TCP                              17m
    mycluster-zookeeper-nodes    ClusterIP   None             <none>        2181/TCP,2888/TCP,3888/TCP            17m
