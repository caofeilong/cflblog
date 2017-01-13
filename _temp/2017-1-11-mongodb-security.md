---
layout: post
title: mongodb security 
tags:mongdb
---



MongoDB 提供各种特性，如身份验证、访问控制、加密，来确保MongoDB的部署。一些关键的安全特性包括。


## Enable Auth

创建用户

```
use admin
db.createUser(
  {
    user: "myUserAdmin",
    pwd: "abc123",
    roles: [ { role: "userAdminAnyDatabase", db: "admin" } ]
  }
)

```


配置config文件 （mongodb v3.4）

```
 vim /etc/mongod.conf 
## 开启权限验证
security:
  authorization: enabled
## 重启服务
systemctl restart mongod

```

链接数据库 `mongo -u "admin" -p "pwd" --authenticationDatabase "admin" `
