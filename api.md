# 接口
Shipyard的核心接口。这个接口可以管理集群中的所有操作。

##账户
 * [账户列表](#get-accounts)
 * [创建账户](#post-accounts)
 * [删除账户](#delete-account)

##角色
 * [角色列表](#get-roles)
 * [角色详情](#get-roles)
 * [创建角色](#post-roles)
 * [删除角色](#delete-role)

##容器
 * [容器列表](#get-containers)
 * [发布容器](#post-containers)
 * [容器详情](#get-container)
 * [删除容器](#delete-container)
 * [停止容器](#stop-container)
 * [重启容器](#restart-container)
 * [拓展容器](#scale-container)
 * [获取容器日志](#get-container-logs)

##引擎
 * [引擎列表](#get-engines)
 * [引擎详情](#get-engine)
 * [增加引擎](#post-engine)
 * [删除引擎](#delete-engine)

##Service Keys
 * [Service Keys列表](#get-service-keys)
 * [增加Service Key](#post-service-keys)
 * [删除Service Key](#delete-service-key)

## Webhook Keys
 * [Webhook Keys列表](#get-webhook-keys)
 * [增加Webhook Key](#post-webhook-key)
 * [删除Webhook Key](#delete-webhook-key)

## 事件
 * [事件列表](#get-events)

## 集群
 * [集群详情](#get-cluster-info)

## Docker中心
 * [发布](#deloyment)

# 身份验证
要使用Shipyard接口就必要要身份验证。要使用接口，需要创建一个[Service Key](/service_keys.html)。所有的请求都必须在请求头里添加``` X-Service-Key ```。
```
curl -s -H "X-Service-Key: Lpc.usH1skelCuqwvjAtF.lJsWGwaKiwey2K" \
    http://localhost:8080/api/cluster/info
{
  "reserved_memory": 1024,
  "reserved_cpus": 0.32,
  "image_count": 17,
  "engine_count": 1,
  "container_count": 4,
  "memory": 4096,
  "cpus": 4
}
```
#账户

## GET /api/accounts
获取账户列表

Request

``` GET /api/accounts HTTP/1.1 ```

Response
```
[
  {
    "role": {
      "name": "admin",
      "id": "8c10fe3d-bf10-4bb9-ab4c-002502b71f13"
    },
    "password": "$2a$10$UvzJ8tssyF0Uvpaxmr06QOVbyJn5gTS4gDLapwo",
    "username": "admin",
    "id": "5f8e6567-9244-4fb2-bde9-24fb5e630b63"
  },
  {
    "role": {
      "name": "user",
      "id": "ddc9a1b1-771b-4a07-807a-42cd027922a5"
    },
    "password": "$2a$10$EEkqHiOjC.018pnqr1giDe0ODVcGaDUC/2lXg",
    "username": "test",
    "id": "44a22dd3-ae74-4fe3-bdf6-58bbd0094f98"
  }
]
```
## POST /api/accounts
创建账户

Request
```
POST /api/accounts HTTP/1.1
Content-Type application/json

{
  "username": "foo",
  "password": "bar",
  "role": {
    "name": "user"
  }
}
```
Response

``` HTTP/1.1 204 No Content ```


## DELETE /api/accounts
删除账户

Request
```
DELETE /api/accounts HTTP/1.1
Content-Type application/json

{
  "username": "foo"
}
```
Response

``` HTTP/1.1 204 No Content ```

#角色

## GET /api/roles
获取角色列表

Request

``` GET /api/roles HTTP/1.1 ```

Response
```
[
  {
    "name": "admin",
    "id": "448ebe2d-89d9-412c-aab9-ad774d1ec78f"
  },
  {
    "name": "user",
    "id": "2243edf5-55f1-43ad-9ebb-c36c5233f007"
  }
]
```
## GET /api/roles/<username>
查看角色详情

Request

``` GET /api/roles/admin HTTP/1.1 ```

Response
```
{
  "name": "admin",
  "id": "448ebe2d-89d9-412c-aab9-ad774d1ec78f"
}
```
## POST /api/roles
创建角色

Request
```
POST /api/roles HTTP/1.1
Content-Type application/json
{
  "name": "test"
}
```
Response

``` HTTP/1.1 204 No Content ```


## DELETE /api/roles
删除角色

Request
```
DELETE /api/roles HTTP/1.1
Content-Type application/json

{
  "name": "test"
}
```
Response

``` HTTP/1.1 204 No Content ```

#容器

## GET /api/containers
容器列表

Response
```
GET /api/containers HTTP/1.1

[
  {
    "state": {
      "started_at": "2014-09-12T00:48:23.824260519Z",
      "pid": 5845,
      "running": true
    },
    "ports": [
      {
        "container_port": 8080,
        "port": 49159,
        "proto": "tcp"
      }
    ],
    "engine": {
      "labels": [
        "local",
        "dev"
      ],
      "memory": 4096,
      "cpus": 4,
      "addr": "http://172.16.1.50:2375",
      "id": "local"
    },
    "image": {
      "restart_policy": {},
      "labels": [
        ""
      ],
      "type": "service",
      "hostname": "cbe68bf32f1a",
      "environment": {
        "GOROOT": "/goroot",
        "GOPATH": "/gopath"
      },
      "memory": 256,
      "cpus": 0.08,
      "name": "ehazlett/go-demo:latest"
    },
    "id": "cbe68bf32f1a08218693dbee9c66ea018c1a99c75c463a76b"
  },
  {
    "state": {
      "started_at": "2014-09-12T00:48:23.824260519Z",
      "pid": 5846,
      "running": true
    },
    "ports": [
      {
        "container_port": 8080,
        "port": 49158,
        "proto": "tcp"
      }
    ],
    "engine": {
      "labels": [
        "local",
        "dev"
      ],
      "memory": 4096,
      "cpus": 4,
      "addr": "http://172.16.1.50:2375",
      "id": "local"
    },
    "image": {
      "restart_policy": {},
      "labels": [
        ""
      ],
      "type": "service",
      "hostname": "eca254ecd76e",
      "environment": {
        "GOROOT": "/goroot",
        "GOPATH": "/gopath"
      },
      "memory": 256,
      "cpus": 0.08,
      "name": "ehazlett/go-demo:latest"
    },
    "id": "eca254ecd76eb9d887995114ff811cc5b7c14fe13630"
  }
]
```
##POST /api/containers
发布容器

Request
```
POST /api/containers HTTP/1.1
Content-Type application/json

{
  "name": "ehazlett/go-demo",
  "cpus": 0.1,
  "memory": 32,
  "type": "service",
  "hostname": "",
  "domain": "",
  "labels": ["local"],
  "args": [],
  "environment": {
    "FOO": "bar"
  },
  "restart_policy": {
    "name": "always"
  },
  "bind_ports": [
    {
      "host_ip": "10.1.2.3",
      "proto": "tcp",
      "container_port": 8080
    },
    {
      "proto": "tcp",
      "port": 80,
      "container_port": 8080
    }
  ],
  "links": {
    "redis": "db"
  }
}
```
Response
```
HTTP/1.1 201 Created

[
  {
    "state": {
      "started_at": "2014-09-12T00:48:23.824260519Z",
      "pid": 5890,
      "running": true
    },
    "ports": [
      {
        "container_port": 8080,
        "host_ip": "10.1.2.3",
        "port": 49172,
        "proto": "tcp"
      }
    ],
    "engine": {
      "labels": [
        "local",
        "dev"
      ],
      "memory": 4096,
      "cpus": 4,
      "addr": "http://172.16.1.50:2375",
      "id": "local"
    },
    "image": {
      "restart_policy": {
        "name": "always"
      },
      "labels": [
        "local"
      ],
      "bind_ports": [
        {
          "proto": "tcp",
          "port": 49153,
          "container_port": 8080
        },
        {
          "proto": "tcp",
          "port": 80,
          "container_port": 8080
        }
      ],
      "links": {
        "redis": "db"
      },
      "type": "service",
      "memory": 32,
      "cpus": 0.1,
      "name": "ehazlett/go-demo"
    },
    "id": "4a5da04b8428e7241a9d9993699513d11b89948399dedfa12"
  }
]
```
## GET /api/containers/<id>
容器详情

Request

``` GET /api/containers/3e532b HTTP/1.1 ```

Response
```
{
  "state": {
    "started_at": "2014-09-12T00:48:23.824260519Z",
    "pid": 5891,
    "running": true
  },
  "ports": [
    {
      "container_port": 8080,
      "port": 49155,
      "proto": "tcp"
    }
  ],
  "engine": {
    "labels": [
      "local",
      "dev"
    ],
    "memory": 4096,
    "cpus": 4,
    "addr": "http://172.16.1.50:2375",
    "id": "local"
  },
  "image": {
    "restart_policy": {},
    "labels": [
      "local"
    ],
    "type": "service",
    "hostname": "demo-1",
    "environment": {
      "GOROOT": "/goroot",
      "GOPATH": "/gopath"
    },
    "memory": 256,
    "cpus": 0.08,
    "name": "ehazlett/go-demo:latest"
  },
  "id": "3e532b000891e90e93ca3781031e7c1ddb76d8378dfdfd3"
}
```
##DELETE /api/containers/<id>
删除容器

Request

``` DELETE /api/containers/3e532 HTTP/1.1 ```

Response

``` HTTP/1.1 204 No Content ```


##GET /api/containers/<id>/stop
停止容器

Request

``` GET /api/containers/3e532/stop HTTP/1.1 ```

Response

``` HTTP/1.1 204 No Content ```


## GET /api/containers/<id>/restart
重启容器

Request

``` GET /api/containers/3e532/restart HTTP/1.1 ```

Response

```HTTP/1.1 204 No Content ```


##GET /api/containers/<id>/scale?count=<count>
拓展容器到指定数目

Request

``` GET /api/containers/3e532/scale?count=10 HTTP/1.1 ```

Response

``` HTTP/1.1 204 No Content ```


## GET /api/containers/<id>/logs
容器日志

Request

``` GET /api/containers/3e532b/logs HTTP/1.1 ```

Response
```
listening on :8080
```
#引擎

##GET /api/engines
引擎列表

Request

``` GET /api/engines HTTP/1.1 ```

Response
```
GET /api/engines HTTP/1.1

[
  {
    "engine": {
      "labels": [
        "local",
        "dev"
      ],
      "memory": 4096,
      "cpus": 4,
      "addr": "http://172.16.1.50:2375",
      "id": "local"
    },
    "id": "99095f5f-7579-4a70-9369-04ad73c21312"
  }
]
```
##GET /api/engines/<id>
引擎详情

Request

``` GET /api/engines/local HTTP/1.1 ```

Response
```
GET /api/engines/local HTTP/1.1

{
  "engine": {
    "labels": [
      "local",
      "dev"
    ],
    "memory": 4096,
    "cpus": 4,
    "addr": "http://172.16.1.50:2375",
    "id": "local"
  },
  "id": "99095f5f-7579-4a70-9369-04ad73c21312"
}
```
##POST /api/engines
向集群中增加引擎

Request
```
POST /api/engines HTTP/1.1
Content-Type application/json

{
  "id": "local",
  "ssl_cert": "",
  "ssl_key": "",
  "ca_cert": "",
  "engine": {
    "id": "local",
    "addr": "http://10.1.2.3:2375",
    "cpus": 4.0,
    "memory": 8192,
    "labels": [
      "local",
      "dev"
    ]
  }
}
```
Response

``` HTTP/1.1 201 Created ```


##DELETE /api/engines/<id>
删除引擎

Request

``` DELETE /api/engines/99095f5f-7579-4a70-9369-04ad73c21312 HTTP/1.1 ```

Response

``` HTTP/1.1 204 No Content ```

#Service Keys

##GET /api/servicekeys
service keys列表

Request

``` GET /api/servicekeys HTTP/1.1 ```

Response
```
GET /api/servicekeys HTTP/1.1

[
  {
    "description": "test",
    "key": "3pYgOl4K7vlkymoi1TMLIAQIJqcYhkGWY04."
  },
  {
    "description": "demo",
    "key": "Lpc.usH1skelCuqwvjAtF.lJsWGwaKiwey2K"
  }
]
```
##POST /api/servicekeys
创建service key

Request
```
POST /api/servicekeys HTTP/1.1
Content-Type application/json

{
  "description": "test key"
}
```
Response
```
{
  "description": "test key",
  "key": "zuoWetDKDRhPyUNRZro5cLo7yaFLKgzcqijW"
}
```
##DELETE /api/servicekeys
删除service key

Request
```
DELETE /api/servicekeys HTTP/1.1
Content-Type application/json

{
  "key": "zuoWetDKDRhPyUNRZro5cLo7yaFLKgzcqijW"
}
```
Response

``` HTTP/1.1 204 No Content ```

#Webhook Keys
Webhook keys被用来发布镜像到Docker中心。


##GET /api/webhookkeys
webhook keys列表

Request

``` GET /api/webhookkeys HTTP/1.1 ```

Response
```
GET /api/servicekeys HTTP/1.1

[
  {
    "key": "fc563339166b3c69",
    "image": "ehazlett/go-demo",
    "id": "d7c68d6f-65bc-4e0c-8134-8e281a6b4d9b"
  }
]
```
##POST /api/webhookkeys
增加webhook key

Request
```
POST /api/webhookkeys HTTP/1.1
Content-Type application/json

{
  "image": "ehazlett/redis"
}
```
Response
```
{
    "image": "ehazlett/redis",
    "key":"8d710a03c7d965aa"
}
```
##DELETE /api/webhooks/<id>
删除webhook key

Request

``` DELETE /api/webhooks/8d710a03c7d965aa HTTP/1.1 ```

Response

``` HTTP/1.1 204 No Content ```

#Info

##GET /api/cluster/info
查看集群信息

Request

``` GET /api/cluster/info HTTP/1.1 ```

Response
```
GET /api/cluster/info HTTP/1.1

{
  "reserved_memory": 768,
  "reserved_cpus": 0.24,
  "image_count": 6,
  "engine_count": 1,
  "container_count": 3,
  "memory": 4096,
  "cpus": 4
}
```
#Docker中心

##POST /hub/webhook/
通过Docker中心webhook自动部署。 将会在从Docker中心获取最新镜像并且重启集群中的所有镜像名称容器。查看如下例子:

要使自动部署生效，你可以在Docker中心的库设置中添加一个Webbook指向``` http://<shipyard-url>/hub/webhook/ ```

Request

``` POST /hub/webhook HTTP/1.1 ```
```
POST /hub/webhook HTTP/1.1
Content-Type application/json

{
   "push_data":{
      "pushed_at":1385141110,
      "images":[
         "imagehash1",
         "imagehash2",
         "imagehash3"
      ],
      "pusher":"username"
   },
   "repository":{
      "status":"Active",
      "description":"my docker repo that does cool things",
      "is_trusted":false,
      "full_description":"This is my full description",
      "repo_url":"https://registry.hub.docker.com/u/username/reponame/",
      "owner":"username",
      "is_official":false,
      "is_private":false,
      "name":"reponame",
      "namespace":"username",
      "star_count":1,
      "comment_count":1,
      "date_created":1370174400,
      "dockerfile":"my full dockerfile is listed here",
      "repo_name":"username/reponame"
   }
}
```
Response

``` HTTP/1.1 200 OK ```
