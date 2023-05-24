---
layout: default
title: Redis
parent: Database
nav_order: 2
last_modified_date:   2023-05-23 17:09:29 +0800
---

<details  markdown="block">
  <summary>
    Table of contents
  </summary>

<!-- TOC -->

- [1. Redis 特性](#1-redis-特性)
    - [1.1. 持久化](#11-持久化)
        - [1.1.1. 分类](#111-分类)
        - [1.1.2. 原理](#112-原理)
    - [1.2. 主从复制](#12-主从复制)
    - [1.3. 哨兵：高可用](#13-哨兵高可用)
    - [1.4. 集群：分布式](#14-集群分布式)

<!-- /TOC -->

</details>

# 1. Redis 特性
参考：https://www.cnblogs.com/kismetv/p/9853040.html,
它的实现原理和一些解决方案非常值得学习

## 1.1. 持久化

### 1.1.1. 分类
- RDB
- AOF

### 1.1.2. 原理
- 参考：https://www.cnblogs.com/kismetv/p/9853040.html

## 1.2. 主从复制
- 一主多从
- 读写分离

## 1.3. 哨兵：高可用
- 需要独立的哨兵进程，哨兵进程会监控 Redis master 和 slave 进程
- 故障转移，自动实现主从切换
- 监控，负责监控 Redis master 和 slave 进程是否正常工作

## 1.4. 集群：分布式