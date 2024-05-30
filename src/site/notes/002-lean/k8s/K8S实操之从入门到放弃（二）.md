---
{"dg-publish":true,"permalink":"/002-lean/k8s/K8S实操之从入门到放弃（二）/","dgPassFrontmatter":true}
---


## 1. **kubectl命令使用**

kubectl是apiserver的客户端工具，工作在命令行下，能够连接apiserver实现各种增删改查等操作 kubectl官方使用文档：https://kubernetes.io/zh/docs/reference/kubectl/over view/
![image.png](https://hoey-images.oss-cn-hangzhou.aliyuncs.com/img/20240529123739.png)



K8S的各种命令帮助文档做得非常不错，遇到问题可以多查help帮助

## 2. **Namespace**

K8s 中，[命名空间（Namespace）](https://kubernetes.io/zh-cn/docs/concepts/overview/working-with-objects/namespaces/)提供一种机制，将同一集群中的资源划分为相互隔离的组。同一命名空间内的资 源名称要唯一，命名空间是用来隔离资源的，不隔离网络。

Kubernetes 启动时会创建四个初始命名空间：

- **default**

Kubernetes 包含这个命名空间，以便于你无需创建新的命名空间即可开始使用新集群。

- **kube-node-lease**

该命名空间包含用于与各个节点关联的 [Lease（租约）对象。 节点租约允许](https://kubernetes.io/zh-cn/docs/concepts/architecture/leases/) kubelet 发送心跳， 由此 控制面能够检测到节点故障。

- **kube-public**

所有的客户端（包括未经身份验证的客户端）都可以读取该命名空间。 该命名空间主要预留为集群使 用，以便某些资源需要在整个集群中可见可读。 该命名空间的公共属性只是一种约定而非要求。

- **kube-system**

该命名空间用于 Kubernetes 系统创建的对象。

```shell
# 查看namespace
kubectl get namespace
# 查看kube-system下的pod
kubectl get pods -n kube-system
# 查看所有namespace下的pod
kubectl get pods -A
```

**创建Namesapce示例**

- **命令行方式**

可以使用下面的命令创建Namespace：

```shell
kubectl create namespace test
```

- **yaml方式**

新建一个名为 my-namespace.yaml 的 YAML 文件，并写入下列内容：
```shell

apiVersion: v1
kind: Namespace
metadata:
	name: test
```

然后运行：
```shell

kubectl apply -f my-namespace.yaml
```

**删除namesapce**
```shell

kubectl delete namespace tuling

kubectl delete -f my-namespace.yaml
```

## 3. **Pod**

[Pod](https://kubernetes.io/zh-cn/docs/concepts/workloads/pods/) **是可以在 Kubernetes 中创建和管理的、最小的可部署的计算单元。Pod**（就像在鲸鱼荚或者豌 豆荚中）**是一组（一个或多个）容器**； 这些容器共享存储、网络、以及怎样运行这些容器的声明。

![image.png](https://hoey-images.oss-cn-hangzhou.aliyuncs.com/img/20240529124750.png)


**创建Pod示例：运行一个NGINX容器**

- **命令行方式**
```shell
# 创建pod 
kubectl run mynginx --image=nginx:1.14.2
```

![image.png](https://hoey-images.oss-cn-hangzhou.aliyuncs.com/img/20240529125220.png)


```shell
# 获取pod的信息，-owide 表示更详细的显示信息 -n 命名空间 查询对应namespace下的pod
kubectl get pod
kubectl get pod -owide
kubectl get pod -owide -n <namespace-name>

#查看pod的详情
kubectl describe pod <pod-name>

# 查看Pod的运行日志
kubectl logs <pod-name>

# 删除pod
kubectl delete pod <pod-name>
```

- **yaml方式**

```yaml
#vim nginx-pod.yaml

apiVersion: v1
kind: Pod
metadata:
	labels:
		run: mynginx
	name: mynginx
spec:
	containers:
	- name: nginx
		image: nginx:1.14.2
		ports:
		- containerPort: 80
```

然后运行：
```shell

kubectl apply -f  nginx-pod.yaml
```

![image.png](https://hoey-images.oss-cn-hangzhou.aliyuncs.com/img/20240529130404.png)


删除pod
```shell
1 kubectl delete -f  nginx-pod.yaml
```

![image.png](https://hoey-images.oss-cn-hangzhou.aliyuncs.com/img/20240529130454.png)

**思考：一个pod中可以运行多个容器吗？**

```yaml
apiVersion: v1
kind: Pod
metadata:
	labels:
		run: myapp
	name: myapp
spec:
	containers:
	- image: nginx:1.14.2
		name: nginx
	- image: tomcat:9.0.55
		name: tomcat
```

执行下面命令

```
kubectl describe pod myapp
```

可以看到创建出的两个container

![image.png](https://hoey-images.oss-cn-hangzhou.aliyuncs.com/img/20240529131617.png)


## 4. **Deployment**

Deployment负责创建和更新应用程序的实例，**使Pod拥有多副本，自愈，扩缩容等能力**。创建 Deployment后，Kubernetes Master 将应用程序实例调度到集群中的各个节点上。如果托管实例的 节点关闭或被删除，Deployment控制器会将该实例替换为群集中另一个节点上的实例。这提供了一种自我修复机制来解决机器故障维护问题。

![image.png](https://hoey-images.oss-cn-hangzhou.aliyuncs.com/img/20240529131712.png)


**创建一个Tomcat应用程序**

使用  kubectl create deployment 命令可以创建一个应用部署**deployment**与**pod**

```shell
#my-tomcat表示pod的名称 --image表示镜像的地址
kubectl create deployment my-tomcat --image=tomcat:9.0.55

#查看一下deployment的信息
kubectl get deployment

#删除deployment
kubectl delete deployment my-tomcat

#查看Pod打印的日志
kubectl logs my-tomcat-6d6b57c8c8-n5gm4

#使用 exec 可以在Pod的容器中执行命令
kubectl exec my-tomcat-6d6b57c8c8-n5gm4 -- env #使用 env 命令查看环境变量
kubectl exec my-tomcat-6d6b57c8c8-n5gm4 -- ls / # 查看容器的根目录下面内容
kubectl exec my-tomcat-6d6b57c8c8-n5gm4 -- sh #进入Pod容器内部并执行bash命令，如果想退出容器可以使用exit命令
```

![image.png](https://hoey-images.oss-cn-hangzhou.aliyuncs.com/img/20240529132238.png)


思考：下面两个命令有什么区别?

```shell
kubectl create my-tomcat --image=tomcat:9.0.55
kubectl create deployment my-tomcat --image=tomcat:9.0.55
```



**自愈**

现在我们来删除刚刚添加的pod，看看会发生什么

```shell
#查看pod信息，-w意思是一直等待观察pod信息的变动
kubectl get pod -w
```

![image.png](https://hoey-images.oss-cn-hangzhou.aliyuncs.com/img/20240529133048.png)


开另外一个命令窗口执行如下命令，同时观察之前命令窗口的变化情况

```shell
kubectl delete pod  my-tomcat-6d6b57c8c8-n5gm4
```

![image.png](https://hoey-images.oss-cn-hangzhou.aliyuncs.com/img/20240529133106.png)


我们可以看到之前那个tomcat的pod被销毁，但是又重新启动了一个新的tomcat pod，这是k8s的服 务**自愈功能**，不需要运维人员干预

**多副本**

- 命令行的方式
```shell
# 创建3个副本
kubectl create deployment my-tomcat --image=tomcat:9.0.55 --replicas=3
```

![image.png](https://hoey-images.oss-cn-hangzhou.aliyuncs.com/img/20240529133121.png)

- yaml方式
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
	labels:
		app: my-tomcat
	name: my-tomcat
spec:
	replicas: 3
	selector:
		matchLabels:
			app: my-tomcat
	template:
		metadata:
			labels:
				app: my-tomcat
		spec:
			containers:
			- image: tomcat:9.0.55
				name: tomcat

```


**扩缩容**

```shell
# 扩容到5个pod
kubectl scale --replicas=5 deployment my-tomcat
# 缩到3个pod
kubectl scale --replicas=3 deployment my-tomcat
```

![image.png](https://hoey-images.oss-cn-hangzhou.aliyuncs.com/img/20240529133154.png)

```shell
#修改 replicas 
kubectl edit deployment my-tomcat
```

**滚动升级与回滚**

对my-tomcat这个deployment进行滚动升级和回滚，将tomcat版本由tomcat:9.0.55升级到 tomcat:10.1.11，再回滚到tomcat:9.0.55

**滚动升级：**

```shell
kubectl set image deployment my-tomcat tomcat=tomcat:10.1.11 --record
```

可以执行 kubectl get pod -w 观察pod的变动情况，可以看到有的pod在销毁，有的pod在创建 查看pod信息
```shell
kubectl get pod
```

![image.png](https://hoey-images.oss-cn-hangzhou.aliyuncs.com/img/20240530105610.png)

查看某个pod的详细信息，发现pod里的镜像版本已经升级了

```shell
kubectl describe pod my-tomcat-85c5c8f685-lnkfm
```

![image.png](https://hoey-images.oss-cn-hangzhou.aliyuncs.com/img/20240530105621.png)

**版本回滚：** 查看历史版本
```shell
kubectl rollout history deploy my-tomcat
```

![image.png](https://hoey-images.oss-cn-hangzhou.aliyuncs.com/img/20240530105646.png)


回滚到上一个版本
```shell
kubectl rollout undo deployment my-tomcat     #--to-revision 参数可以指定回退的版本

#回滚(回到指定版本)
kubectl rollout undo deployment/my-dep --to-revision=2
```

![image.png](https://hoey-images.oss-cn-hangzhou.aliyuncs.com/img/20240530105724.png)



查看pod详情，发现版本已经回退了

![image.png](https://hoey-images.oss-cn-hangzhou.aliyuncs.com/img/20240530105804.png)

**访问tomcat pod**

**集群内访问**（在集群里任一worker节点都可以访问）
```shell
curl 10.244.169.164:8080
```

![image.png](https://hoey-images.oss-cn-hangzhou.aliyuncs.com/img/20240530105833.png)

**集群外部访问**

![image.png](https://hoey-images.oss-cn-hangzhou.aliyuncs.com/img/20240530111134.png)

当我们在集群之外访问是发现无法访问，那么集群之外的客户端如何才能访问呢？这就需要我们的 ser vice服务了，下面我们就创建一个service，使外部客户端可以访问我们的pod

## 5. **Service**

[Service](https://kubernetes.io/zh-cn/docs/concepts/services-networking/service/)是一个抽象层，它定义了一组Pod的逻辑集，并为这些Pod支持外部流量暴露、负载均衡和服 务发现。

尽管每个Pod 都有一个唯一的IP地址，但是如果没有Service，这些IP不会暴露在群集外部。Service允 许您的应用程序接收流量。Service也可以用在ServiceSpec标记type的方式暴露，type类型如下：

- ClusterIP（默认）：在集群的内部IP上公开Service。这种类型使得Service只能从集群内访问。
- NodePort：使用NAT在集群中每个选定Node的相同端口上公开Service。使用 ``<NodeIP>:<NodePort>`` 从集 群外部访问Service。是ClusterIP的超集。
- LoadBalancer：在当前云中创建一个外部负载均衡器(如果支持的话)，并为Service分配一个固定的外部IP。是 NodePort的超集。
- ExternalName：通过返回带有该名称的CNAME记录，使用任意名称（由spec中的externalName指定）公开 Service。不使用代理。

![image.png](https://hoey-images.oss-cn-hangzhou.aliyuncs.com/img/20240530111922.png)


**创建service示例**

- 命令行的方式

```shell
kubectl expose deployment my-tomcat --name=tomcat --port=8080 --type=NodePort

#查看service信息，port信息里冒号后面的端口号就是对集群外暴露的访问接口
# NodePort范围在 30000-32767 之间
kubectl get svc -o wide
```
![image.png](https://hoey-images.oss-cn-hangzhou.aliyuncs.com/img/20240530113639.png)

访问http://172.22.63.15:32306/
![image.png](https://hoey-images.oss-cn-hangzhou.aliyuncs.com/img/20240530113841.png)



**集群外部访问** 使用集群节点的ip加上暴露的端口就可以访问

tomcat版本太高返回404的解决办法：进入tomcat容器，把 webapps 目录删除，再 把 webapps.dist 重命名为 webapps 即可。

![image.png](https://hoey-images.oss-cn-hangzhou.aliyuncs.com/img/20240530113827.png)


- yaml的方式

```yaml
# vim mytomcat-service.yaml

apiVersion: v1
kind: Service
metadata:
	labels:
		app: my-tomcat
	name: my-tomcat
spec:
	ports:
	- port: 8080 # service的虚拟ip对应的端口，在集群内网机器可以访问用service的虚拟ip加该端口号访问服务
		nodePort: 30001 # service在宿主机上映射的外网访问端口，端口范围必须在30000-32767之间
		protocol: TCP
		targetPort: 8080 # pod暴露的端口，一般与pod内部容器暴露的端口一致
	selector:
		app: my-tomcat
	type: NodePort
```


执行如下命令创建service：

```shell
kubectl apply -f mytomcat-service.yaml 
```
![image.png](https://hoey-images.oss-cn-hangzhou.aliyuncs.com/img/20240530114016.png)




