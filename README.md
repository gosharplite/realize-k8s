# 实现集群运维层 K8S
<p align="center">
<img src="https://raw.githubusercontent.com/gosharplite/realize-k8s/master/new-stack.png" width="600">
</p>
K8S为[Kubernetes](http://kubernetes.io/)的简称，是Google的开原项目，已经送给[CNCF基金会](https://cncf.io/)主导。K8S 位于集群运维层，它结合多台服务器的资源，管理分散式容器架构，实现应用需求和硬件的解耦。台北研究院已在机房建构出K8S，共开发人员使用，运行资料将纪录在此。深入了解K8S请浏览[此页](https://github.com/gosharplite/the-new-stack/blob/master/README.md)。
##进入系统
```
$ mkdir zeta; cd zeta
$ wget http://10.128.112.15:8087/kubernetes/v1.0.6/kubectl
$ sudo chmod +x kubectl
$ wget http://10.128.112.15:8087/tyd/v0.7/srv/kube-apiserver/config-droi
$ export KUBECONFIG="./config-droi"
$ ./kubectl version
Client Version: version.Info{Major:"1", Minor:"0", GitVersion:"v1.0.6", GitCommit:"388061f00f0d9e4d641f9ed4971c775e1654579d", GitTreeState:"clean"}
Server Version: version.Info{Major:"1", Minor:"0", GitVersion:"v1.0.6", GitCommit:"388061f00f0d9e4d641f9ed4971c775e1654579d", GitTreeState:"clean"}
```
##网络
服务器 名称 | IP
------------ | -------------
master | 10.128.112.15
worker1 | 10.128.112.25
worker2 | 10.128.112.26

為了符合K8S的网络需求，flannel的虚拟联网功能建立覆盖（ overlay ）网络`11.1.0.0/16`。每个worker先分到一块网络，再分配给容器（pod）。

服务器 名称 | 覆盖网络
------------ | -------------
worker1 | 11.1.92.0/24
worker2 | 11.1.81.0/24

pod 名称 | IP
------------ | -------------
frontend-60e4n | 11.1.92.20
frontend-b7tgj | 11.1.81.5
redis-master-207ve | 11.1.92.21
redis-slave-0rkpg | 11.1.81.7
heapster-knf9o | 11.1.92.25

应用程序开发者通过K8S服务代理访问所需的服务，无需知道提供服务的容器具体位于网络何处。K8S服务发现功能使用拟网络`11.0.0.0/16`。
