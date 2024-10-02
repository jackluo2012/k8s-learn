### 安装docker
```bash
# 加载 bridge-utils 工具包
yum install -y epel-release
yum install -y bridge-utils

 # 加载 br_netfilter 模块 所能经过的桥接都 要被 防火墙 拦截
modprobe br_netfilter
# 添加 br_netfilter 模块到模块加载配置文件 开机自动加载
echo 'br_netfilter' >> /etc/modules-load.d/bridge.conf
# 添加 net.bridge.bridge-nf-call-ip6tables 参数到 sysctl 配置文件
echo 'net.bridge.bridge-nf-call-ip6tables = 1' >> /etc/sysctl.d/99-sysctl.conf 
# 添加 net.bridge.bridge-nf-call-iptables 参数到 sysctl 配置文件
echo 'net.bridge.bridge-nf-call-iptables = 1' >> /etc/sysctl.d/99-sysctl.conf 
# 添加 net.ipv4.ip_forward 参数到 sysctl 配置文件
echo 'net.ipv4.ip_forward = 1' >> /etc/sysctl.d/99-sysctl.conf 
# 重新加载 sysctl 配置文件
sysctl -p 



### 
sudo dnf install -y yum-utils device-mapper-persistent-data lvm2

# 添加 Docker CE 的阿里云 YUM 源
sudo dnf config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo
sudo dnf makecache
# 安装 docker
sudo dnf install -y docker-ce docker-ce-cli containerd.io

# 配置 daemon
sudo mkdir -p /etc/docker
sudo tee /etc/docker/daemon.json <<-'EOF'
{
  "default-ipc-mode": "shareable",
  "data-root": "/data/docker",
  "exec-opts": ["native.cgroupdriver=systemd"],
  "log-driver": "json-file",
  "log-opts": {
    "max-size": "100m",
    "max-file": "100"
  },
  "insecure-registries": ["harbor.xinxianghf.com"],
  "registry-mirrors": ["https://olmwsf82.mirror.aliyuncs.com"]
}
EOF
# 创建docker 启动的管理 目录 
mkdir -p /etc/systemd/system/docker.service.d

#重启 并设置开机自启动
sudo systemctl daemon-reload && systemctl restart docker && systemctl enable docker

```
