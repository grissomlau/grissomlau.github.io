---
layout: default
title: Redis
parent: Database
nav_order: 2
last_modified_date:   2023-05-23 17:09:29 +0800
---

<details  markdown="block">
  <summary>
    TOC
  </summary>

<!-- TOC -->

- [Redis](#redis)
    - [Redis 特性](#redis-特性)
        - [持久化](#持久化)
            - [分类](#分类)
            - [原理](#原理)
        - [主从复制](#主从复制)
        - [哨兵：高可用](#哨兵高可用)
        - [集群：分布式](#集群分布式)

<!-- /TOC -->

</details>

# Redis
---
## Redis 特性
参考：https://www.cnblogs.com/kismetv/p/9853040.html,
它的实现原理和一些解决方案非常值得学习

### 持久化

#### 分类
- RDB
- AOF

#### 原理
- 参考：https://www.cnblogs.com/kismetv/p/9853040.html

### 主从复制
- 一主多从
- 读写分离

### 哨兵：高可用
- 需要独立的哨兵进程，哨兵进程会监控 Redis master 和 slave 进程
- 故障转移，自动实现主从切换
- 监控，负责监控 Redis master 和 slave 进程是否正常工作

### 集群：分布式