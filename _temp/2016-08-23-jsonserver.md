---
title: JSON Server
tags: [技术]
---


在前端开发中，有很多时候会因为后端接口不能提供导致前端的工作不能继续进行，为此我们采用了很多方发来moc数据，jsonServer 是一个可以快速方便的moc数据的server。

得到一个完整的假REST API为零编码在不到30秒  
创建< 3对前端开发人员需要快速后端原型和模拟。


## 安装JSON Server

```
npm install -g json-server
```

## Example

创建db.json

```
{
  "posts": [
    { "id": 1, "title": "json-server", "author": "typicode" }
  ],
  "comments": [
    { "id": 1, "body": "some comment", "postId": 1 }
  ],
  "profile": { "name": "typicode" }
}
```


开启JSON Server

```
json-server --watch db.json
```

现在如果你去访问  http://localhost:3000/posts/1  你会得到

```
{ "id": 1, "title": "json-server", "author": "typicode" }
```

