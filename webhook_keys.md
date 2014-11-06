# Webhook keys
Webhook keys用来连接Docker Hub。Webhooks主要作用是在Docker中心触发生成新的镜像和在Shipyard中重新部署。

# 工作流程
 * Docker中心被触发构建新的Docker镜像
 * Docker中心发送一个webhook提醒到Shipyard
 * Shipy检查webhook key的授权
 * Shipyard从Docker中心获取最新的镜像
 * Shipyard停止和删除当前容器并且发布新的容器

# 使用webhook key
要使用webhook key，只需为Docker中心的镜像在如下地址添加一个webhook：``` http://<shipyard-url>/hub/webhook/<key> ```
例如：
``` http://controller.example.com/hub/webhook/010f2af9db29f43a ```。

#例子
## 创建一个webhook key
```
shipyard cli> shipyard add-webhook-key --image ehazlett/go-demo
created key: 010f2af9db29f43a
```
## 查看webhook key列表
```
shipyard cli> shipyard webhook-keys
Image                   Key
ehazlett/go-demo        010f2af9db29f43a
```
## 删除webhook key
```
shipyard cli> shipyard remove-webhook-key 010f2af9db29f43a
removed 010f2af9db29f43a
```
