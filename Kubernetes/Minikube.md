# Minikube部署

使用minikube安装单机测试Kubernetes集群

### 检查虚拟化的支持

```
grep -E --color 'vmx|svm' /proc/cpuinfo
```

如果上面的命令返回的不是空就可以

## 安装kubectl

```
https://dl.k8s.io/release/v1.18.2/bin/linux/amd64/kubectl
chmod +x kubectl
sudo mv kubectl /usr/local/bin/
```

v1.18.2是版本，不同版本自行选择

### 安装minikube

```
sudo curl -Lo minikube https://github.com/kubernetes/minikube/releases/download/v1.13.1/minikube-linux-amd64 && sudo chmod +x minikube && sudo mv minikube /usr/local/bin/
```

### 启动

墙内用户方式，墙外按教程就行

```
docker pull anjone/kicbase
minikube start --vm-driver=docker --base-image="anjone/kicbase" --image-mirror-country='cn' --image-repository='registry.cn-hangzhou.aliyuncs.com/google_containers'
```

## 检测状态

```
minikube status
```

### 正确状态返回

```
minikube
type: Control Plane
host: Running
kubelet: Running
apiserver: Running
kubeconfig: Configured
```

