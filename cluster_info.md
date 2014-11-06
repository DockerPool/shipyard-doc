# 集群信息
Shipyard提供查看集群状态信息。将会汇报所有集群的资源如CPUs和内存，容器数，镜像数，引擎数，以及CPUs和内存的使用率。

#例子
## 查看集群信息
```
shipyard cli> shipyard info
Cpus: 4.00
Memory: 8192.00 MB
Containers: 2
Images: 5
Engines: 1
Reserved Cpus: 4.00% (0.16)
Reserved Memory: 3.52% (288.00 MB)
```
