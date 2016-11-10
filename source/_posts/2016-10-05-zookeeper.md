---
layout: post
title: zookeeper 学习
---

Zookeeper是一个开放源码的分布式服务协调组件，他解决的分布式数据一致性问题，提供了顺序一致性、原子性、单一视图、可靠性、实时性等。
ZooKeeper的核心实现算法 Zab，就是解决了分布式系统下数据如何在多个服务之间保持同步问题的。


### zookeeper  安装

[下载](http://www.apache.org/dyn/closer.cgi/zookeeper/)

### zookeeper 服务启动

```

./zkServer.sh start
./zkServer.sh stop
./zkServer.sh status
./zkServer.sh restart

```

### zookeeper 节点操作

启动客户端 ./zkCli.sh

```
create /nodeName  nodeValue  创建节点
get /nodeName 获取节点的值
set /nodeName  newValue 修改节点的内容
ls /nodeName   查看子节点
delete /nodeName  删除节点
rmr  /nodeName 将创建的zk目录以及它下面的子目录都删除

```


### 使用get 命令获取内容时

```
czxid. 节点创建时的zxid.
mzxid. 节点最新一次更新发生时的zxid.
ctime. 节点创建时的时间戳.
mtime. 节点最新一次更新发生时的时间戳.
dataVersion. 节点数据的更新次数.
cversion. 其子节点的更新次数.
aclVersion. 节点ACL(授权信息)的更新次数.
ephemeralOwner. 如果该节点为ephemeral节点, ephemeralOwner值表示与该节点绑定的session id. 如果该节点不是ephemeral节点, ephemeralOwner值为0. 至于什么是ephemeral节点, 请看后面的讲述.
dataLength. 节点数据的字节数.
numChildren. 子节点个数.
```


### node 使用 zookeeper 

使用库 **node-zookeeper-client**

```javascript

let zookeeper = require('node-zookeeper-client');
let client = zookeeper.createClient("127.0.0.1:2181", {
        sessionTimeout: 100,
        spinDelay: 1000,
        retries: 1
    }
);
client.connect();
client.once('connected', function () {
    console.info("zookeeper connected");
})

client.on('state', function (state) {
    console.log(state);
});

exports.createNode = function (nodeurl, value) {
    client.create(
        nodeurl,
        new Buffer(value),
        zookeeper.CreateMode.PERSISTENT,
        function (error, path) {
            if (error) {
                console.log(error.stack);
                return;
            }
            console.log('Node: %s is created.', path);
        }
    );
}

exports.getData = function (nodeUrl) {
    client.getData(nodeUrl, function (event) {
            console.log('Got event: %s.', event);
            exports.getData(nodeUrl);
        },
        function (error, value) {
            console.info("value:" + value.toString());
        }
    )
}


exports.setData = function (nodeUrl, value, version) {
    client.setData(nodeUrl, new Buffer(value), version, function (error, stat) {
        if (error) {
            console.log(error.stack);
            return;
        }
        console.log('Data is set.');
    });
}

exports.remove = function (nodeUrl, version) {
    client.remove(nodeUrl, version, function (error) {
        if (error) {
            console.log(error.stack);
            return;
        }
        console.log('Node is deleted.');
    });
}


exports.getChildren = function (nodeUrl) {
    client.getChildren(nodeUrl, function (event) {
        console.log('Got event: %s.', event);
        exports.getChildren(nodeUrl);
    }, function (error, children, stats) {
        if (error) {
            console.log(error.stack);
            return;
        }
        console.log('Children are: %j.', children);
    });
}
 
```




### 参考链接

[zookeeper](http://zookeeper.apache.org/)
[zookeeperWiki](https://cwiki.apache.org/confluence/display/ZOOKEEPER/Index;jsessionid=18FE23C9C838C34CB58AC237D3C7B7AC)


