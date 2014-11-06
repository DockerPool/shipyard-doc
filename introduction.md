# Shipyard
Docker集群管理

基于Docker集群管理工具[Citadel](https://github.com/citadel/citadel),Shipeyard使我们能够管理Docker的资源，包括容器，主机等等。

Shipyard与其他docker管理工具不同之处在于，它偏向于组件的组合性。Shipyard的核心部分是管理Dokcker（容器等）。但是它也可以通过拓展镜像的方式来添加诸如容器路由和负载均衡，中心化日志，更好的部署以及其他。你可以使用任何组件来适应你的需求。
![Shipyard后台管理](http://shipyard-project.com/images/dashboard.png)

# Web UI
web接口提供了一些简单的基于Docker集群的管理。你可以通过简单的接口查看Docker集群和宿主引擎的使用率，创建和销毁容器，查看Docker集群通用事件和其他更多的。

#命令行接口
Shipyard提供了一个强大的命令行接口。利用API，你完全可以管理所有的Docker集群。
![Shipyard UI](http://shipyard-project.com/images/cli.png)

#接口
Shipyard的核心是API。Shipyard构建于中心化的API。CLI和web UI都是使用API来提供所有的功能。通过使用service key，你可以直接通过Shipyard API来和Docker集群交互和自定义构建集群。
![Shipyard API](http://shipyard-project.com/images/api.png)

#更多信息
查看[文档](/doc.html)来了解更多关于Shipyard是如何工作的。
查看[快速入门](/quickstart.html)来获取Shipyard实例来开发。

#帮助
如果你遇到任何问题，请毫不犹豫地在聊天室（#shipyard on Freenode）或者[GitHub](https://github.com/shipyard/shipyard)工程来获得帮助。



