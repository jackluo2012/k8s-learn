### 01.什么是资源
- 资源是k8s集群中的一个实体，例如节点、pod、service、deployment等。
### 资源类别
#### 名称空间级别
- 工作负载型资源:Pod、ReplicaSet、Deployment .
- 服务发现及负载均衡型资源:Service、Ingress.
- 配置与存储型资源:Volume、CSl
- 特殊类型的存储卷:ConfigMap、Secre.
#### 集群级资源
- Namespace、Node、ClusterRole、ClusterRoleBinding
#### 元数据型资源
- HPA、PodTemplate、LimitRange


02.资源清单的编写
```
apiVersion: v1 # group/apiversion 接口组/版本
kind: Pod # 资源类型
metadata: # 元数据
  name: my-pod # 资源名称
  namespace: default # 名称空间
  labels:
    app: my-app # 标签
spec:   # 期望状态
  containers: # 容器
    - name: my-container # 容器名称
      image: my-image:latest # 容器镜像
      ports:
        - containerPort: 80 # 容器端口
status: # 当前状态
  phase: Running # 容器状态
  conditions: # 容器状态
    - type: Ready # 容器状态
      status: "True" # 容器状态
      lastProbeTime: "2024-02-20T12:00:00Z" # 容器状态
      lastTransitionTime: "2024-02-20T12:00:00Z" # 容器状态
      reason: "ContainerReady" # 容器状态
      message: "Container is ready" # 容器状态
```
#### pod demo
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: busybox-pod
  labels:
    app: busybox
spec:
  containers:
  - name: busybox
    image: busybox:latest
    command: ['sh', '-c', 'echo "Hello from busybox!" && sleep 3600']
  restartPolicy: Always
```



03.Pod 的生命周期

04.Pod 是如何被调度运行的