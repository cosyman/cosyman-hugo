+++
categories = ["java"]
date = "2015-08-12T12:48:51+08:00"
description = ""
keywords = []
title = "Java 性能介绍"

draft = true
+++

1. 性能测试
2. 了解系统

面向对象的本质就是对象与消息交互

System Load 单位时间线程数，理论上接近cpu核数为佳利用，通过cpu，memory，network，io综合曲线可以发现问题。

## 集群

1. http 转发
2. 反向代理
3. IP请求转发，减少了http层点传输等待
4. 数据链路层，mac地址改写，ip相同，用的比较多，性能也最好。

## 缓存
cdn
反向代理
一致性hash， 2<sup>31</sup>个虚拟的圆。每个节点虚拟大概200个虚拟节点，散落在这个虚拟点圆上，增加命中的平均

## 队列

响应时间
解藕，数据的创建与消费分离

## 存储

B+树，3-4层高的树，原因在于磁盘的连续读性能最佳，减少寻址。对于固态硬盘应该有更好的算法。插入较更新快，寻址的时间。

Raid 过去式，向其中磁盘写校验信息，停机恢复。
hdfs

## 异步

线程数初始化计算公式
多线程
非阻塞




## References

http://java-performance.info/
http://www.javaperformancetuning.com/
