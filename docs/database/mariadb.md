---
layout: default
title: MariaDB
parent: Database
nav_order: 2
last_modified_date:   2023-05-23 17:09:29 +0800
---
<details  markdown="block">
  <summary>
    TOC
  </summary>

1. [安装](#安装)
    1. [服务端](#服务端)
    2. [客户端](#客户端)
2. [配置](#配置)
    1. [服务端(ip绑定和用户权限)](#config-server)
        1. [初始化root密码](#初始化root密码)
        2. [ip绑定](#ip绑定)
        3. [用户权限](#用户权限)
3. [拉数据](#拉数据)
    1. [快速导出excel,效率最高的方式](#快速导出excel效率最高的方式)
</details>



# 安装
## 服务端
```bash
sudo apt-get install mariadb-server
```

## 客户端
### Ubuntu 命令行客户端
```bash
sudo apt-get install mariadb-client
```

### Windows 客户端
- [MySQL Workbench](https://dev.mysql.com/downloads/workbench/)
- [HeidiSQL](https://www.heidisql.com/download.php)
- [Navicat](https://www.navicat.com.cn/download/navicat-premium)
- [SQLyog](https://www.webyog.com/en/downloads)

### Mac 客户端
- [Sequel Pro](https://sequelpro.com/download)

## 配置
### 服务端(ip绑定和用户权限)<a id="config-server"></a>
#### 初始化root密码
```bash
sudo mysql_secure_installation
```
#### ip绑定
- 需要修改配置文件，使其支持远程连接，这里远程是指 server 绑定到多个网卡的 IP 地址，允许通过这些本机的网卡 IP 地址连接到 server

```bash
sudo vim /etc/mysql/mariadb.conf.d/50-server.cnf
# 修改 bind-address 为 0.0.0.0, 默认是 127.0.0.1, 即只能本地 localhost 连接 ,然后重启服务

```
#### 用户权限
- 配置用户权限

```bash
# 登录 mysql
mysql -u root -p
# 选择数据库
use mysql;
# 查看用户
select user,host from user;

# 创建用户，下面的 % 是指所有 IP 地址都可以连接，如果指定 IP 地址，如 '用户名'@'192.168.10.8', 也可以用通配符指定网段 '用户名'@'192.168.10.%'
create user '用户名'@'%' identified by '密码';

# 授权，% 可改成具体的ip地址，'用户名'@'%' 必须存在于 user 表中，*.* 表示所有数据库，all privileges 表示所有权限
grant all privileges on *.* to '用户名'@'%';

# 查看用户权限
show grants for '用户名'@'%';

# 刷新权限
flush privileges;

```
- 移除用户权限

```bash
# 移除权限
revoke all privileges on *.* from '用户名'@'%';

# 删除用户
drop user '用户名'@'%';

```
---

# 拉数据
## 快速导出excel,效率最高的方式
```bash
# 导出csv
select * from table_name into outfile '/tmp/table_name.csv' fields terminated by ',' optionally enclosed by '"' escaped by '"' lines terminated by '\n';
# 使用 bash 导出 csv
mysql -u your_username -p your_database_name -e "SELECT * FROM your_table_name;" | sed 's/\t/","/g;s/"NULL"/""/g;s/^/"/;s/$/"/' > /path/to/export/directory/your_table_name.csv
# 然后用 zip 压缩
zip -r your_table_name.zip your_table_name.csv
# 最后用 scp/ftp 拉到本地
scp your_username@your_server_ip:/path/to/your_table_name.zip /path/to/your_local_directory

```