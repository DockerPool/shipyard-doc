# 快速入门
这篇文档描述如何快速启动和运行Shipyard。
Shipyard主要有两个组件：RethinkDB和接口。

#RethinkDB
启动一个RethinkDB实例：
```
docker run -it -d --name shipyard-rethinkdb-data --entrypoint /bin/bash shipyard/rethinkdb -l
```
启动一个数据挂载的RethinkDB容器实例：
```
docker run -it -P -d --name shipyard-rethinkdb --volumes-from shipyard-rethinkdb-data shipyard/rethinkdb
```

# 接口
启动Shipyard容器：
```
docker run -it -p 8080:8080 -d --name shipyard \
    --link shipyard-rethinkdb:rethinkdb shipyard/shipyard
```
Shipyard将会创建一个用户名为```admin```密码为```shipyard```的默认账户。接下来你可以打开浏览器访问```http://<your-host-ip>:8080```并登陆查看。

#引擎
接下来你可以使用web UI或者控制台接口来添加引擎。

#设置
注意：基本本地socket(译者注：即unix:/var/run/docker.socket)是有限制的，并且不推荐使用。例如，端口暴露在web UI中不起作用，因为它并不知道引擎的IP。并且拓展镜像也不能基于引擎的IP。推荐的配置是使用TCP。如果你想使用socket设置来调试，请在IRC中访问我们。

为了配置一台主机，你需要使用TCP将Docker经常暴露出来。在Dcoker中配置TCP，你可以查看[Docker文档](https://docs.docker.com/articles/basics/)。你可以使用```http://<docker-host-ip>:<docker-host-port>```作为```addr```在命令控制接口或者web UI增加一个引擎。

要了解更多信息请查看[引擎](/engines.html)

