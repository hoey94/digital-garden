---
{"dg-publish":true,"permalink":"/002-lean/k8s/K8S理论之从入门到放弃（三）/","dgPassFrontmatter":true}
---


## 1. **K8S的网络模型**

K8S的网络中主要存在4种类型的通信：

- 同一Pod内的容器间通信
- 各个Pod彼此间的通信
- Pod和Service间的通信
- 集群外部流量和Service之间的通信

K8S为Pod和Service资源对象分别使用了各自的专有网络，Pod网络由K8S的网络插件配置实现，而 Ser vice网络则由K8S集群进行指定。如下图：

![image.png](https://hoey-images.oss-cn-hangzhou.aliyuncs.com/img/20240530133100.png)


K8S使用的网络插件需要为每个Pod配置至少一个特定的地址，即Pod IP。Pod IP地址实际存在于某个 网卡（可以是虚拟机设备）上。 而Service的地址却是一个虚拟IP地址，没有任何网络接口配置在此地址上，它由Kube-proxy借助 iptables规则或ipvs规则重定向到本地端口，再将其调度到后端的Pod对象。Service的IP地址是集群提 供服务的接口，也称为Cluster IP。 Pod网络和IP由K8S的网络插件负责配置和管理，具体使用的网络地址可以在管理配置网络插件时进行 指定，如10.244.0.0/16网络。而Cluster网络和IP是由K8S集群负责配置和管理，如10.96.0.0/12网 络。

从上图进行总结起来，一个K8S集群包含是三个网络。

- 节点网络：各主机（Master、Node、ETCD等）自身所属的网络，地址配置在主机的网络接口，用于各主机之 间的通信，又称为节点网络。
- Pod网络：专用于Pod资源对象的网络，它是一个虚拟网络，用于为各Pod对象设定IP地址等网络参数，其地址配 置在Pod中容器的网络接口上。Pod网络需要借助kubenet插件或CNI插件实现。
- Service网络：专用于Service资源对象的网络，它也是一个虚拟网络，用于为K8S集群之中的Service配置IP地 址，但是该地址不会配置在任何主机或容器的网络接口上，而是通过Node上的kube-proxy配置为iptables或 ipvs规则，从而将发往该地址的所有流量调度到后端的各Pod对象之上。

## 2. **K8S的工作流程**

用K8S部署Nginx的过程中，K8S内部各组件是如何协同工作的： **我们在master节点执行一条命令要master部署一个nginx应用**(kubectl create deployment nginx - -image=nginx)

- 这条命令首先发到master节点的网关api server，这是matser的唯一入口
- api server将命令请求交给controller mannager进行控制
- controller mannager 进行应用部署解析
- controller mannager 会生成一次部署信息，并通过api server将信息存入etcd存储中
- scheduler调度器通过api server从etcd存储中，拿到要部署的应用，开始调度看哪个节点有资源适合部署
- scheduler把计算出来的调度信息通过api server再放到etcd中
- 每一个node节点的监控组件kubelet，随时和master保持联系（给api-server发送请求不断获取最新数据），拿 到master节点存储在etcd中的部署信息
- 假设node2的kubelet拿到部署信息，显示他自己节点要部署某某应用
- kubelet就自己run一个应用在当前机器上，并随时给master汇报当前应用的状态信息
- node和master也是通过master的api-server组件联系的
- 每一个机器上的kube-proxy能知道集群的所有网络，只要node访问别人或者别人访问node，node上的kube- proxy网络代理自动计算进行流量转发

![image.png](https://hoey-images.oss-cn-hangzhou.aliyuncs.com/img/20240530133124.png)


## 3. **k8s架构原理六连问**

K8S 是一个基于容器技术的分布式集群管理系统。既然是个分布式系统，那势必有多个 Node 节点（物理主 机或虚拟机），它们共同组成一个分布式集群，并且这些节点中会有一个 Master 节点，由它来统一管理 Node 节点。

如图所示：

![image.png](https://hoey-images.oss-cn-hangzhou.aliyuncs.com/img/20240530133145.png)


**问题一：主节点和工作节点是如何通信的呢？**

首先，Master 节点启动时，会运行一个 kube-apiserver 进程，它提供了集群管理的 API 接口，是集群内各 个功能模块之间数据交互和通信的中心枢纽，并且它页提供了完备的集群安全机制。

在 Node 节点上，使用 K8S 中的 kubelet 组件，在每个 Node 节点上都会运行一个 kubelet 进程，它负责 向 Master 汇报自身节点的运行情况，如 Node 节点的注册、终止、定时上报健康状况等，以及接收 Master 发出的命令，创建相应 Pod。

在 K8S 中，Pod 是最基本的操作单元，它与 docker 的容器有略微的不同，因为 Pod 可能包含一个或多个容 器（可以是 docker 容器），这些内部的容器是共享网络资源的，即可以通过 localhost 进行相互访问。

关 于 Pod  内 是 如 何 做 到 网 络 共 享 的 ， 每 个 Pod  启 动 ， 内 部 都 会 启 动 一 个 pause 容 器 （ google的 一 个 镜 像），它使用默认的网络模式，而其他容器的网络都设置给它，以此来完成网络的共享问题。

如图所示：

![image.png](https://hoey-images.oss-cn-hangzhou.aliyuncs.com/img/20240530133159.png)


**问题二：Master 是如何将 Pod 调度到指定的 Node 上的？**

该工作由 kube-scheduler 来完成，整个调度过程通过执行一些列复杂的算法最终为每个 Pod 计算出一个最 佳的目标 Node，该过程由 kube-scheduler 进程自动完成。常见的有轮询调度（RR）。当然也有可能，我 们需要将 Pod 调度到一个指定的 Node 上，我们可以通过节点的标签（Label）和 Pod 的 nodeSelector 属 性的相互匹配，来达到指定的效果。

如图所示：

![image.png](https://hoey-images.oss-cn-hangzhou.aliyuncs.com/img/20240530133208.png)


**问题三：各节点、Pod 的信息都是统一维护在哪里的，由谁来维护？**

从上面的 Pod 调度的角度看，我们得有一个存储中心，用来存储各节点资源使用情况、健康状态、以及各 Pod 的基本信息等，这样 Pod 的调度来能正常进行。

在 K8S 中，采用 etcd 组件 作为一个高可用强一致性的存储仓库，该组件可以内置在 K8S 中，也可以外部搭 建供 K8S 使用。

集群上的所有配置信息都存储在了 etcd，为了考虑各个组件的相对独立，以及整体的维护性，对于这些存储 数据的增、删、改、查，统一由 kube-apiserver 来进行调用，apiserver 也提供了 REST 的支持，不仅对各 个内部组件提供服务外，还对集群外部用户暴露服务。

外 部 用 户 可 以 通 过 REST 接 口 ， 或 者 kubectl 命 令 行 工 具 进 行 集 群 管 理 ， 其 内 在 都 是 与 apiserver  进 行 通 信。

如图所示：

![image.png](https://hoey-images.oss-cn-hangzhou.aliyuncs.com/img/20240530133218.png)


**问题四：外部用户如何访问集群内运行的 Pod ？**

前面讲了外部用户如何管理 K8S，而我们更关心的是内部运行的 Pod 如何对外访问。使用过Docker 的同学 应该知道，如果使用 bridge 模式，在容器创建时，都会分配一个虚拟 IP，该 IP 外部是没法访问到的，我们 需要做一层端口映射，将容器内端口与宿主机端口进行映射绑定，这样外部通过访问宿主机的指定端口，就 可以访问到内部容器端口了。

那 么 ， K8S 的 外 部 访 问 是 否 也 是 这 样 实 现 的 ？ 答 案 是 否 定 的 ， K8S 中 情 况 要 复 杂 一 些 。 因 为 上 面 讲 的 Docker 是 单 机 模 式 下 的 ， 而 且 一 个 容 器 对 外 就 暴 露 一 个 服 务 。 在 分 布 式 集 群 下 ， 一 个 服 务 往 往 由 多 个 Application 提供，用来分担访问压力，而且这些 Application 可能会分布在多个节点上，这样又涉及到了跨

主机的通信。

这里，K8S 引入了 Service 的概念，将多个相同的 Pod 包装成一个完整的 service 对外提供服务，至于获取 到这些相同的 Pod，每个 Pod 启动时都会设置 labels 属性，在 Service 中我们通过选择器 Selector，选择 具有相同 Name 标签属性的 Pod，作为整体服务，并将服务信息通过 Apiserver 存入 etcd 中，该工作由 Service Controller 来完成。同时，每个节点上会启动一个 kube-proxy 进程，由它来负责服务地址到 Pod 地址的代理以及负载均衡等工作。

如图所示：

![image.png](https://hoey-images.oss-cn-hangzhou.aliyuncs.com/img/20240530133231.png)


**问题五：Pod 如何动态扩容和缩放？**

既然知道了服务是由 Pod 组成的，那么服务的扩容也就意味着 Pod 的扩容。通俗点讲，就是在需要时将 Pod 复制多份，在不需要后，将 Pod 缩减至指定份数。K8S 中通过 Replication Controller 来进行管理，为 每个 Pod 设置一个期望的副本数，当实际副本数与期望不符时，就动态的进行数量调整，以达到期望值。期 望数值可以由我们手动更新，或自动扩容代理来完成。

如图所示：

![image.png](https://hoey-images.oss-cn-hangzhou.aliyuncs.com/img/20240530133240.png)


**问题六：各个组件之间是如何相互协作的？**

最后，讲一下 kube-controller-manager 这个进程的作用。我们知道了 ectd 是作为集群数据的存储中心， apiserver  是 管 理 数 据 中 心 ， 作 为 其 他 进 程 与 数 据 中 心 通 信 的 桥 梁 。 而 Service  Controller 、 Replication Controller 这些统一交由 kube-controller-manager 来管理，kube-controller-manager 作为一个守护进

程，每个 Controller 都是一个控制循环，通过 apiserver 监视集群的共享状态，并尝试将实际状态与期望不 符的进行改变。关于 Controller，manager 中还包含了 Node 节点控制器（Node Controller）、资源配额 管控制器（ResourceQuota Controller）、命名空间控制器（Namespace Controller）等。

如图所示：

![image.png](https://hoey-images.oss-cn-hangzhou.aliyuncs.com/img/20240530133250.png)