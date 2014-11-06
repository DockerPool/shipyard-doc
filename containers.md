# 容器
在Shipyard中的一个容器就是一个简单的Docker容器。容器可以部署在一个或多个引擎。

部署一个容器的时候，有下列选项可用：

## Name
这是Docker镜像的名称，例如，``` shipyard/shipyard ```

## CPUs
给容器分配的CPU数量

## Memory
给容器分配的内存（单位MB）

## Type
在Shipyard中，一个容器可以是这些类型：``` service ```，``` unique ```，或者 ``` host ```。

``` service ```类型会使用主机标签来调度容器。Shipyard只会在有这个标签的引擎上运行容器。

``` unique ```类型的容器只会在所有引擎上运行一个实例。这有助于调度的高可用性。

``` host ```类型将会运行在特定的主机上。对于特定的主机，可以使用下列的语法来启动：``` --label host:<host-id> ```例如：``` --label host:local ```。这个容器就只会运行在引擎ID为：``` local ```的主机上。

## Hostname
容器的主机名

## Domain
容器的域名

## ENV
你可以指定多个 ``` --env ```参数来给容器增加多个环境变量。使用``` key=value ```的格式。

## Arg
传递给容器的参数，使用``` --arg ```。同样的可以多次使用。

## Label
调用要使用到的标签

## Port
要暴露端口，使用下列语法：``` --port <proto>/<host-port>:<container-port> ```例如：``` --port tcp/:8080 --port tcp/80:8080 ```。同样的可以多次使用。

## Pull
将会从registry中获取最新的镜像。

## Count
可以指定容器实例在集群中的启动数量。默认为1.

#例子
## 发布一个容器
```
shipyard cli> shipyard run --name ehazlett/go-demo \
    --cpus 0.1 \
    --memory 32 \
    --type service \
    --hostname demo-test \
    --domain local \
    --env FOO=bar \
    --label dev \
    --pull
started 407e39dc1ccc on local
```
## 查看容器列表
```
shipyard cli> shipyard containers
ID              Name                    Host    Ports
407e39dc1ccc    ehazlett/go-demo:latest local   tcp/49166:8080
```
## 查看容器详情
```
shipyard cli> shipyard inspect 407e3
{
  "ports": [
    {
      "container_port": 8080,
      "port": 49166,
      "proto": "tcp"
    }
  ],
  "engine": {
    "labels": [
      "local",
      "dev"
    ],
    "memory": 2048,
    "cpus": 4,
    "addr": "http://10.1.2.3:2375",
    "id": "local"
  },
  "image": {
    "restart_policy": {},
    "labels": [
      "local"
    ],
    "type": "service",
    "hostname": "407e39dc1ccc",
    "environment": {
      "GOROOT": "/goroot",
      "GOPATH": "/gopath"
    },
    "memory": 256,
    "cpus": 0.08,
    "name": "ehazlett/go-demo:latest"
  },
  "id": "407e39dc1cccc675591c86306563e78be6de085745427656ad1"
}
```
## 销毁容器
```
shipyard cli> shipyard destroy 407e39
destroyed 407e39dc1ccc
```
