# 文档
这份文档描述Shipyard是如何工作的。你可以使用[快速入门](/quickstart.html)来部署Shipyard。

注意：这份文档展示的例子都是通过Shipyard命令控制接口面完成。你可以通过``` shipyard/shipyard-cli ```来运行一个Docker容器实例。例如：

```
docker run -it shipyard/shipyard-cli
```

#RethinkDB
RethinkDB用来保存账户，引擎，service key和拓展元信息。它不会保存任何Docker容器和镜像的信息。在```shipyard/rethinkdb```镜像中``` /data ```是数据挂载目录。

#相关概念
查看下面的文档以了解详情。
* [权限控制](/authentication.html)
* [引擎](/engines.html)
* [容器](/containers.html)
* [Service Keys](/service_keys.html)
* [Webhook Kyes](/webhook_keys.html)
* [事件](/events.html)
* [集群信息](/cluster_info.html)

#使用
* [命令控制接口](/cli.html)
* [控制器](/controller.html)

#接口
Shipyard提供功能强大的API来管理集群。
* [接口文档](api.html)

#使用说明
默认情况下,控制器将在后台定期报告使用信息。包括引擎数量等等。它是后台运行的（包括ip和镜像名称的记录）。你可以在启动控制器时通过使用```-disable-usage-info```参数来禁用该特性。
