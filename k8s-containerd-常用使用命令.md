#### k8s-containerd 常用命令 crictl（kubernetes）主要用于k8s
### 配置镜像源配置
[text](https://gist.github.com/y0ngb1n/7e8f16af3242c7815e7ca2f0833d3ea6)
```
vim /etc/containerd/config.toml
sudo systemctl restart containerd
```

```
crictl -n k8s.io namespaces ls #查看所有的命名空间
```
#### 查看，所有的镜像 
```
crictl images ls
```
### 拉取镜像
```
ctr -n k8s.io images pull m.daocloud.io/docker.io/library/nginx:
```
### 导入镜像
```
ctr -n k8s.io image import 
```
