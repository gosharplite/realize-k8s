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
##网路
服务器 名称 | IP
------------ | -------------
master | 10.128.112.15
worker1 | 10.128.112.25
worker2 | 10.128.112.26
