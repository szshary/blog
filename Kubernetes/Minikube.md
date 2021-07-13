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

### 部署测试
```
kubectl create deployment hello-minikube --image=registry.aliyuncs.com/google_containers/echoserver:1.10
```

## 访问dashboard

###  启动dashboard

```
minikube dashboard --url
```
#### 输出
```
http://127.0.0.1:33685/api/v1/namespaces/kubernetes-dashboard/services/http:kubernetes-dashboard:/proxy
```

### 启动kubectl proxy
```
kubectl proxy --port=8001 --address='192.168.1.230' --accept-hosts='^.*'
```
#### 输出
```
Starting to serve on 192.168.1.230:8001
```
### 访问地址
```
192.168.1.230:8001/api/v1/namespaces/kubernetes-dashboard/services/http:kubernetes-dashboard:/proxy
```


