###### kubectl --help 
```txt
--alsologtostderr[=false]: 同时输出日志到标准错误控制台和文件。
--api-version="": 和服务端交互使用的API版本。
--certificate-authority="": 用以进行认证授权的.cert文件路径。
--client-certificate="": TLS使用的客户端证书路径。
--client-key="": TLS使用的客户端密钥路径。
--cluster="": 指定使用的kubeconfig配置文件中的集群名。
--context="": 指定使用的kubeconfig配置文件中的环境名。
--insecure-skip-tls-verify[=false]: 如果为true，将不会检查服务器凭证的有效性，这会导致你的HTTPS链接变得不安全。
--kubeconfig="": 命令行请求使用的配置文件路径。
--log-backtrace-at=:0: 当日志长度超过定义的行数时，忽略堆栈信息。
--log-dir="": 如果不为空，将日志文件写入此目录。
--log-flush-frequency=5s: 刷新日志的最大时间间隔。
--logtostderr[=true]: 输出日志到标准错误控制台，不输出到文件。
--match-server-version[=false]: 要求服务端和客户端版本匹配。
--namespace="": 如果不为空，命令将使用此namespace。
--password="": API Server进行简单认证使用的密码。
-s, --server="": Kubernetes API Server的地址和端口号。
--stderrthreshold=2: 高于此级别的日志将被输出到错误控制台。
--token="": 认证到API Server使用的令牌。
--user="": 指定使用的kubeconfig配置文件中的用户名。
--username="": API Server进行简单认证使用的用户名。
--v=0: 指定输出日志的级别。
--vmodule=: 指定输出日志的模块，格式如下：pattern=N，使用逗号分隔。

kubectl annotate – 更新资源的注解。
kubectl api-versions – 以“组/版本”的格式输出服务端支持的API版本。
kubectl apply – 通过文件名或控制台输入，对资源进行配置。
kubectl attach – 连接到一个正在运行的容器。
kubectl autoscale – 对replication controller进行自动伸缩。
kubectl cluster-info – 输出集群信息。
kubectl config – 修改kubeconfig配置文件。
kubectl create – 通过文件名或控制台输入，创建资源。
kubectl delete – 通过文件名、控制台输入、资源名或者label selector删除资源。
kubectl describe – 输出指定的一个/多个资源的详细信息。
kubectl edit – 编辑服务端的资源。
kubectl exec – 在容器内部执行命令。
kubectl expose – 输入replication controller，service或者pod，并将其暴露为新的kubernetes service。
kubectl get – 输出一个/多个资源。
kubectl label – 更新资源的label。
kubectl logs – 输出pod中一个容器的日志。
kubectl namespace -（已停用）设置或查看当前使用的namespace。
kubectl patch – 通过控制台输入更新资源中的字段。
kubectl port-forward – 将本地端口转发到Pod。
kubectl proxy – 为Kubernetes API server启动代理服务器。
kubectl replace – 通过文件名或控制台输入替换资源。
kubectl rolling-update – 对指定的replication controller执行滚动升级。
kubectl run – 在集群中使用指定镜像启动容器。
kubectl scale – 为replication controller设置新的副本数。
kubectl stop – （已停用）通过资源名或控制台输入安全删除资源。
kubectl version – 输出服务端和客户端的版本信息。

kubectl get pods
kubectl get rc
kubectl get service
kubectl get componentstatuses
kubectl get endpoints
kubectl cluster-info
kubectl create -f redis-master-controller.yaml
kubectl delete -f redis-master-controller.yaml
kubectl delete pod nginx-772ai
kubectl logs -f pods/heapster-xxxxx -n kube-system #查看日志
kubectl scale rc redis-slave --replicas=3 #修改RC的副本数量，来实现Pod的动态缩放

etcdctl cluster-health #检查网络集群健康状态
etcdctl --endpoints=https://192.168.71.221:2379 cluster-health #带有安全认证检查网络集群健康状态
etcdctl member list
etcdctl set /k8s/network/config '{ "Network": "10.1.0.0/16" }'
etcdctl get /k8s/network/config

kubectl get services kubernetes-dashboard -n kube-system #查看所有service
kubectl get deployment kubernetes-dashboard -n kube-system #查看所有发布
kubectl get pods --all-namespaces #查看所有pod
kubectl get pods -o wide --all-namespaces #查看所有pod的IP及节点
kubectl get pods -n kube-system | grep dashboard
kubectl describe service/kubernetes-dashboard --namespace="kube-system"
kubectl describe pods/kubernetes-dashboard-349859023-g6q8c --namespace="kube-system" #指定类型查看
kubectl describe pod nginx-772ai #查看pod详细信息
kubectl scale rc nginx --replicas=5 # 动态伸缩
kubectl scale deployment redis-slave --replicas=5 #动态伸缩
kubectl scale --replicas=2 -f redis-slave-deployment.yaml #动态伸缩
kubectl exec -it redis-master-1033017107-q47hh /bin/bash #进入容器
kubectl label nodes node1 zone=north #增加节点lable值 spec.nodeSelector: zone: north #指定pod在哪个节点
kubectl get nodes -lzone #获取zone的节点
kubectl label pod redis-master-1033017107-q47hh role=master #增加lable值 [key]=[value]
kubectl label pod redis-master-1033017107-q47hh role- #删除lable值
kubectl label pod redis-master-1033017107-q47hh role=backend --overwrite #修改lable值
kubectl rolling-update redis-master -f redis-master-controller-v2.yaml #配置文件滚动升级
kubectl rolling-update redis-master --image=redis-master:2.0 #命令升级
kubectl rolling-update redis-master --image=redis-master:1.0 --rollback #pod版本回滚
```
```txt
# 查看集群信息
kubectl cluster-info

# 查看各组件信息
kubectl -s http://localhost:8080 get componentstatuses

# 查看pods所在的运行节点
kubectl get pods -o wide

# 查看pods定义的详细信息
kubectl get pods -o yaml

# 查看Replication Controller信息
kubectl get rc

# 查看service的信息
kubectl get service

# 查看节点信息
kubectl get nodes

# 按selector名来查找pod
kubectl get pod --selector name=redis

# 查看运行的pod的环境变量
kubectl exec pod名 env

2 操作类命令

# 创建
kubectl create -f 文件名

# 重建
kubectl replace -f 文件名  [--force]

# 删除
kubectl delete -f 文件名
kubectl delete pod pod名
kubectl delete rc rc名
kubectl delete service service名
kubectl delete pod --all

```