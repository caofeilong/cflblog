---
layout: post
title: mongodb security 
tags:mongdb
---


MongoDB 提供各种特性，如身份验证、访问控制、加密，来确保MongoDB的部署。一些关键的安全特性包括。

|身份验证|授权|TLS/SSl|企业认证|
|:--:|:--:|:--:|:--:|
|Authentication
SCRAM-SHA-1
x.509| 基于角色的访问控制，开启身份验证，管理用户和角色|传输加密，Configure mongod and mongos for TLS/SSL
TLS/SSL Configuration for Clients|Kerberos 验证，ldap代理验证，Encryption at Rest，Auditing|

##  Security CheckList

MongoDb 总是也提供了  security List 的推荐列表来保护mongoDB 的部署

1.  开启访问控制
2.  配置基于角色的访问控制
3.  加密通信
4.  加密和保护数据
5.  限制网络曝光
6.  审计系统活动
7.  用特定的用户运行MongoDB
8.  使用安全的配置运行MongoDB
9.  使用安全的技术实现指南
8.  
8.  