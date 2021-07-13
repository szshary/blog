# 解散kubernetes集群

本文档将介绍解散现有集群

## 解散集群

### worker

在每一个worker节点，进行下述步骤:
在每一个worker节点，进行下述步骤:
在每一个worker节点，进行下述步骤:

执行reset，命令:

```bash
kubeadm reset
```

重启服务，命令:

```bash
systemctl restart docker
systemctl restart kubelet
```

清理容器，命令:

```bash
docker container prune
```

查询所有镜像，命令:

```bash
docker images
```

然后清理残留的服务/引擎镜像（替换镜像名为需要清理的镜像）:

```bash
docker rmi x.x.x.x:xx/xxx-xx-xxxxxxx
```

#### 移除网络

```
停止服务:

​```bash
sytemctl stop docker
sytemctl stop kubelet
​```

清理:

​```bash
ifconfig cni0 down
ip link delete cni0
​```

启动服务:

​```bash
sytemctl start docker
sytemctl start kubelet
​```
```



### master

在master节点，将每个worker节点移除，命令(节点名注意替换)：

```bash
kubectl get nodes   # 查询节点
kubectl delete node worker-node-1
kubectl delete node worker-node-2
kubectl delete node worker-node-3
kubectl delete node worker-node-4
...
```

执行reset，命令:

```bash
kubeadm reset
```

重启服务，命令:

```bash
systemctl restart docker
systemctl restart kubelet
```

清理容器，命令:

```bash
docker container prune
```

查询所有镜像，命令:

```bash
docker images
```

然后清理残留的服务/引擎镜像（替换镜像名为需要清理的镜像）:

```bash
docker rmi x.x.x.x:xx/xxx-xx-xxxxxxx
```

