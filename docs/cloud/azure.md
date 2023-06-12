---
layout: default
title: Azure
parent: Cloud
nav_order: 1
last_modified_date: 2023-05-25 16:09:29 +0800
---
<details  markdown="block">
  <summary>
    TOC
  </summary>

<!-- TOC -->

- [Azure](#azure)
    - [注意事项](#注意事项)

<!-- /TOC -->
</details>

# Azure
---
## 注意事项
- 创建一个 Pay-As-You-Go 订阅，停用后3天后才能删除，停用期间可能无法创建新的订阅。
- 公网ip，内部虚拟网络, managed disk，monitor都是收费的，而且不想 虚拟机那样可以在选择时计算价格。
- 如果是测试，不使用 managed disk 避免收费，只有部分 Gen1 的系统才支持 unmanaged disk，Gen2 的系统必须使用 managed disk。
- 帐号的type影响是否可以使用 savings plan, 个人帐号不可以使用 savings plan。
- 但在可以在 subscription 下面选择  advisor recommendation，购买1年或者3年的预付费，可以节省很多钱，它的折扣和 savings plan 是一样的。
- azure portal 缓存非常严重，经常需要刷新才能看到最新状态，扣费状态甚至需要延迟1天才计算出来。
- storage account 的 container 可以查看 vhd 的类型，如果DiskType 是 OS，那么这个 vhd 是系统盘，如果是 Data，那么这个 vhd 是数据盘。
- storage account 提供 30GB 的免费存储空间，但是如果使用了 managed disk，会有额外费用。而且写需要收费，存储免费。
