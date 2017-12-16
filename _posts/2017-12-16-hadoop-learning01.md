---
layout:     post
title:      "Hadoop学习笔记1"
subtitle:   "Hadoop简介"
date:       2017-12-16 22:00:00
author:     "Chocolove"
header-img: "img/post-bg-nextgen-web-pwa.jpg"
header-mask: 0.3
catalog:    true
tags:
    - hadoop
    - 大数据
---
# Hadoop
##HDFS体系结构
HDFS采用了主从（Master/Slave）结构模型，一个HDFS集群是由一个NameNode和若干个DataNode组成的。其中NameNode作为主服务器，管理文件系统的命名空间和客户端对文件的访问操作；集群中的DataNode管理存储的数据。NameNode执行文件系统的命名操作，比如打开、关闭、重命名文件或目录等，它也负责数据块到具体DataNode的映射。DataNode负责处理文件系统客户端的文件读写请求，并在NameNode的同意调度下进行数据块的创建、删除和复制工作。

##MapReduce体系结构
MapReduce框架是由一个单独运行在主节点的JobTracker和运行在每个集群从节点的TaskTracker共同组成的。主节点负责调度构成一个作业的所有任务，这些任务分布在不同的从节点上。主节点监控它们的执行情况，并且重新执行之前失败的任务；从节点仅负责由主节点指派的任务。

Hadoop的MapReduce模型是通过输入key/value对进行运算得到输出key/value对。其分为Map过程和Reduce过程。

Map主要的工作是接收一个key/value对，产生一个中间key/value对，之后MapReduce把集合中所有相同key值的value放在一起并传递给Reduce函数。Reduce函数接收key和相关的value集合并合并这些value值，得到一个较小的value集合。

下图是MapReduce的数据流图，体现了MapReduce处理大数据集的过程。这个过程就是将大数据分解为成百上千个小数据集，每个（或若干个）数据集分别由集群中的一个节点进行处理并生成的中间结果，然后这些中间结果又由大量的节点合并，形成最终结果。

![](https://ws1.sinaimg.cn/large/ad74e54fly1fmirvvd1ddj20oh03nac8.jpg)
  