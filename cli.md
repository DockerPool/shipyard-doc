# CLI使用
这篇文档描述怎样使用Shipyard CLI（command line interface）来工作。

#查看帮助
```
shipyard cli> shipyard help
NAME:
   shipyard - manage a shipyard cluster

USAGE:
   shipyard [global options] command [command options] [arguments...]

VERSION:
   2.0.3

COMMANDS:
   login                login to a shipyard cluster
   change-password      update your password
   accounts             show accounts
   add-account          add account
   delete-account       delete account
   containers           list containers
   inspect              inspect container
   run                  run a container
   stop                 stop a container
   restart              restart a container
   scale                scale a container
   logs                 show container logs
   destroy              destroy a container
   engines              list engines
   add-engine           add shipyard engine
   remove-engine        removes an engine
   inspect-engine       inspect an engine
   service-keys         list service keys
   add-service-key      adds a service key
   remove-service-key   removes a service key
   extensions           show extensions
   add-extension        add extension
   remove-extension     remove an extension
   webhook-keys         list webhook keys
   add-webhook-key      adds a webhook key
   remove-webhook-key   removes a webhook key
   info                 show cluster info
   events               show cluster events
   help, h              Shows a list of commands or help for one command

GLOBAL OPTIONS:
   --help, -h                   show help
   --generate-bash-completion
   --version, -v                print the version
```
#登录
登录Shipyard集群。将会保存授权信息到``` ~/.shipyardrc ```。
```
shipyard cli> shipyard login
URL: http://localhost:8080
Username: admin
Password: **********
```
#修改密码
只要登录了系统，你就可以使用 ``` change-password ```来修改账户的密码。
```
shipyard cli> shipyard change-password
Password: **********
Confirm: **********
```
#账户列表
列出所有Shipyard账户
```
shipyard cli> shipyard accounts
Username        Role
admin           admin
demo            user
```
#增加账户
使用命令 ``` add-account ```。
## 可选项
 * ``` --username,-u ```:账户名称
 * ``` --password,-p ```:账户密码
 * ``` --role,-r ```:账户角色（admin/user）
```
shipyard cli> shipyard add-account -u demo -p demo123 -r user
```
#删除账户
使用命令``` delete-account ```。
```
shipyard cli> shipyard delete-account demo
```
#查看容器列表
查看集群所有容器列表使用 ``` containers ```。
```
shipyard cli> shipyard containers
ID              Name                    Host    Ports
7b55a8eb9f57    redis:2.8.11            local   tcp/49167:6379
3e532b000891    ehazlett/go-demo:latest local   tcp/49155:8080
```
#查看容器详情
```
shipyard cli> shipyard inspect 3e53
{
    "id": "3e532b000891e90e93ca3781031e7c1ddb76d8378dfdfd3a34f",
    "image": {
        "name": "ehazlett/go-demo:latest",
        "cpus": 0.08,
        "memory": 256,
        "environment": {
            "GOPATH": "/gopath",
            "GOROOT": "/goroot"
        },
        "hostname": "demo-1",
        "type": "service",
        "labels": [
            "local"
        ],
        "restart_policy": {}
    },
    "engine": {
        "id": "local",
        "addr": "http://10.1.2.3:2375",
        "cpus": 4,
        "memory": 8192,
        "labels": [
            "dev",
            "local"
        ]
    },
    "ports": [
        {
            "proto": "tcp",
            "port": 49155,
            "container_port": 8080
        }
    ]
}
```
#发布容器
使用命令 ``` run ```。
## 可选项
 * ``` --name ```:Docker镜像名称
 * ``` --container-name ```:容器名称
 * ``` --cpus ```:可使用的cpus
 * ``` --memory ```:可使用的内存单位MB
 * ``` --type ```:容器类型（service，host，unique）
 * ``` --hostname ```:容器主机名
 * ``` --domain ```:容器域名
 * ``` --env ```:设置容器环境变量
 * ``` --link ```:连接其他容器
 * ``` --arg ```:容器命令行参数
 * ``` --vol ```:容器挂载点（``` /host/path:/container/path ```或者```/container/path ```）
 * ``` --label ```:用来调度的标签
 * ``` --port ```:容器暴露的端口（```<proto>/<host-ip>:<host-port>:<container-port>```）
 * ``` --publish ```:暴露所有端口
 * ``` --pull ```:启动之前获取最新镜像
 * ``` --count ```:容器启动数量
 * ``` --restart ```:重启策略（失败时，总是，失败次数：5等等）
```
shipyard cli> shipyard run --name ehazlett/go-demo \
    --cpus 0.1 \
    --memory 32 \
    --type service \
    --hostname demo-test \
    --domain local \
    --link redis:db \
    --port tcp/10.1.2.3:80:8080 \
    --port tcp/::8000 \
    --restart "on-failure:5" \
    --env FOO=bar \
    --label dev \
    --pull
started 407e39dc1ccc on local
```
#容器扩展
将扩展容器到想要的数量。
```
shipyard cli> shipyard scale --id 407e --count 10
scaled 407e39dc1ccc to 10
```
#查看容器日志
显示容器的日志。
```
shipyard cli> shipyard logs 407e39
listening on :8080
```
#销毁容器
杀掉和删除容器。
```
shipyard cli> shipyard destroy 407e
destroyed 407e39dc1ccc
```
#查看引擎列表
显示集群上的引擎列表。
```
shipyard cli> shipyard engines
ID      Cpus    Memory  Host                    Labels
local   4.00    8192.00 http://10.1.2.3:2375    dev,local
```
#增加引擎
使用``` add-engine ```。
## 可选项
 * ``` --id ```:引擎id
 * ``` --addr ```:引擎地址（例如：http://10.1.2.3:2375）
 * ``` --cpus ```:引擎cpus
 * ``` --memory ```:引擎内存
 * ``` --label ```:调度使用的标签
 * ``` --ssl-cert ```:（可选）ssl证书地址
 * ``` --ssl-key ```:（可选）ssl key
 * ``` --ca-cert ```:（可选）ca证书地址
```
shipyard cli> shipyard add-engine --id demo --add http://10.1.2.3:2375 --cpus 4.0 --memory 4096 --label local --label dev
```
#查看引擎详情
使用``` inspect-engine ```查看引擎详情。
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
#删除引擎
使用 ``` remove-engine ```从集群中删除引擎
```
shipyard cli> shipyard remove-engine demo
```
#创建Service key
使用 ``` add-service-key ```。
## 可选项
 * ``` --description,-d ```:key的描述
```
shipyard cli> shipyard add-service-key -d "test key"
created key: Z2uwezQGoaIcfiRSQBRbktrzdbFRWKlVTEry
```
#查看Service key列表
使用 ``` service-keys ```查看集群的service key 列表
```
shipyard cli> shipyard service-keys
Key                                     Description
Z2uwezQGoaIcfiRSQBRbktrzdbFRWKlVTEry    test key
```
#查看集群信息
使用 ``` info ```。
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
#查看事件列表
使用``` events ```。
```
shipyard cli> shipyard events
Time                  Message         Engine  Type     Tags
Sep 09 06:58:13 2014  container:6c07  local   start    docker
Sep 09 06:58:13 2014  container:6c07  local   create   docker
```

