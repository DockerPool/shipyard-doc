# 引擎
一个Shipyard集群包含一个或者多个“引擎”。一个引擎就是一个Docker后台程序，它提供socket（本地使用）或者供其他机器使用的TCP端口。除此之外再没有其他任何的代理或者安装远程程序来激活管理；仅仅只是通过Docker的接口。

Docker后台程序侦听TCP端口请参看[Docker文档](https://docs.docker.com/articles/basics/)在“Bind Docker to another host/port or a Unix socket”。

当一个引擎被添加到Shipyard中，你就可以为一个特殊的引擎定义资源限制了。在调度容器时会使用这些限制来确保引擎适应所有的请求。你可以使用SSL证书来保证安全通信。

# ID
每个引擎都必须有一个可以识别的标示符。

# 地址
这个地址是用来和引擎交互的。对于本地用户，你可以使用``` unix:///path/to/docker.sock ```。对于多机配置，使用非SSL端口``` http:// ```或者基于SSL协议的``` https:// ```

# 资源
每个引擎都应该定义对资源的限制。它们可以是CPU和内存（单位MB）。

# 标签
一个引擎可以有一个或多个标签。这些都是用来调度和决策容器的。

# SSL
一个引擎可以配置成使用SSL。参看[Docker文档](https://docs.docker.com/articles/https/)来运行SSL。

#例子
## 增加引擎
```
shipyard cli> shipyard add-engine --id local \
    --addr http://10.1.2.3:2375 \
    --cpus 4.0 \
    --memory 8192 \
    --label dev \
    --label local
```
你也可以使用Docker socket来添加引擎，这样的话就只能运行单机环境了。你也可以在Shipyard控制器运行时添加一个挂载项（``` -v /var/run/docker.sock:/docker.sock ```）

```
shipyard cli> shipyard add-engine --id local-socket \
    --addr unix:///docker.sock \
    --cpus 4.0 \
    --memory 8192 \
    --label dev \
    --label local
```
## 查看引擎列表
```
shipyard cli> shipyard engines
ID      Cpus    Memory  Host                    Labels
local   4.00    8192.00 http://172.16.1.50:2375 local,dev
```

## 查看引擎详情
```
shipyard cli> shipyard inspect-engine local
{
  "engine": {
    "labels": [
      "local",
      "dev"
    ],
    "memory": 2048,
    "cpus": 4,
    "addr": "http://172.16.1.50:2375",
    "id": "local"
  },
  "id": "a08b8518-e963-4eb5-959a-566bd270cd28"
}
```
##删除引擎
```
shipyard cli> shipyard remove-engine a08b8518-e963-4eb5-959a-566bd270cd28
removed local
```
