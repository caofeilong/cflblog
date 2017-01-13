---
title: mongodb 基于角色的访问控制 
tags: [mongdb]
---

MongoDB 提供各种特性，如身份验证、访问控制、加密，来确保MongoDB的部署。

## Manger Users and Roles

#### 创建管理员用户

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


配置config文件开启鉴权 （mongodb v3.4）

```
 vim /etc/mongod.conf 

## 开启权限验证
security:
  authorization: enabled

## 重启服务
systemctl restart mongod

```

重新链接数据库 `mongo -u "admin" -p "pwd" --authenticationDatabase "admin" `


### 用户操作

```
## 创建用户

db.createUser(
  {
    user: "cfl",
    pwd: "cfl",
    roles: [ { role: "readWrite", db: "cms" } ]
  }
)

## 撤销用户角色

db.revokeRolesFromUser('cmsAdmin',[{role:'dbAdmin',db:'cms'}])

## 授予用户角色

db.grantRolesToUser('cmsAdmin',[{role:'dbAdmin',db:'cms'}])

## 修改密码

db.changeUserPassword('cmsAdmin','cmsAdmin456')

```


### mongodb 常用内键角色

1. root 最高角色能够操作所有的库和备份(备份权限要是3.4版本添加的)
2. read  读权限
3. readWrite  写权限
4. dbAdmin  数据库管理员
5. dbOwner 具有 read,readWrite,dbAdmin,userAdmin 的所有特权
6. userAdmin  用户管理角色
7. backup   备份
8. restore  还原
9. readAnyDatabase
10. readWriteAnyDatabase
11. userAdminAnyDatabase
12. dbAdminAnyDatabase
