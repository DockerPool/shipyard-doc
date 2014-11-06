# 事件
Shipyard记录所有的集群操作，例如容器的创建，启动，停止，service key的管理，引擎的管理等等。

#例子
## 查看事件列表
```
shipyard cli> shipyard events
Time                  Message         Engine  Type     Tags
Sep 09 06:58:13 2014  container:6c07  local   start    docker
Sep 09 06:58:13 2014  container:6c07  local   create   docker
```
