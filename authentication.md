# 权限控制
Shipyard支持多用户。你必须登录才能使用Shipyard集群。

注意：Shipyard将会在初次启动时自动创建一个管理用户。在登录之后你可以查看控制器的登录log。

#账户
你可以通过管理员身份来创建多个用户以控制访问权限。

#角色
在Shipyard中有两种角色：```admin```和```user```。
``` admin ```角色拥有全部的权限。
``` user ``` 角色除了不能管理账户和service keys之外其他都可以。

#例子
## 创建一个账户
```
shipyard cli> shipyard add-account -u demo -p demo123 -r user
```
## 查看所有账户
```
shipyard cli> shipyard accounts
Username        Role
admin           admin
test            user
```
## 删除账户
```
shipyard cli> shipyard delete-account demo
```
