---
layout: post
title: Mongodb 常用方法
tags: [mongdb]
---

好记性不如烂笔头，由于mongo不是天天用所以用过之后就忘了，每次用都得重新看文档，于是谢了一个简单的笔记记下来常用的一些方法，持续更新每次会把用到的东西更新上来。

可视化工具：robomongo


```javascript

//查询
db.collectionname.find(); //查询所有
db.collectionname.find({KEY:VALUE}); //条件查询
db.collectionname.find({KEY:RegExp})//模糊查询
db.collectionname.find({KEY:{$in:[VALUES]}}) //$in 查询
db.collectionname.find({key:{$gte:VALUE,$lte:VALUE}})//范围查询$gt大于 $lt小于 $ne不等于
db.collectionname.find().sort({KEY:1}) //排序查询
db.collectionname.find({$or:[{KEY:VALYE}]})//$or
db.collectionname.find().limit(5).skip(2)//limit(显示的调试)  skip(跳过的条数)
db.collectionname.sort({KEY:1}); //1正序 -1 倒序
db.collectionname.find().explain(); //查询分析
db.collectionname.aggregate(); //聚合
db.collectionname.count({components:{$exists:true}})  //查询字段是否存在
//更新
db.collectionname.update({},{$unset:{components:null}}) //删除components 这个为null的字段
db.collectionname.update({条件},{$set:{修改字段}}) //修改部分字段  使用$set 只会更新有变化的字段，其他字段不受影响
{$push:{需要push的对象}} //为list结构的数据添加内容
{$pull:{删除条件}} //删除list结构中的数据
//更新list结构字段中的内容
db.collectionname.update({条件},{'字段名.$.list结构中字段的名称'})


// 索引
db.tablesname.ensureIndex({KEY:1}); //创建索引
db.tablesname.ensureIndex({KEY:1},{unique:true}); //创建唯一索引




//使用mongo连接远程的mongodb
mongo ip:port -u username -p passowrd 

```
