# 控制器
这篇文档描述如何使用Shipyard的控制器。下面的示例假设你正在使用``` shipyard/shipyard ```的Docker镜像。
#查看帮助
```
$> docker run shipyard/shipyard -h

Usage of /app/controller:
  -listen=":8080": listen address
  -rethinkdb-addr="127.0.0.1:28015": rethinkdb address
  -rethinkdb-auth-key="": rethinkdb auth key
  -rethinkdb-database="shipyard": rethinkdb database
```
#侦听
允许改变侦听地址。不应该在运行容器中来改变。

#RethinkDB地址
连接RethinkDB的地址。使用``` <host-or-ip>:<port> ```。

#RethinkDB数据库
Shipyard使用哪个RethinkDB数据库。

#RethinkDB验证密钥
连接RethinkDB时使用的验证密钥。
