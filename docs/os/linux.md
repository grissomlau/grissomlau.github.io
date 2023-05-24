---
layout: default
title: Linux
parent: OS
nav_order: 2
last_modified_date:   2023-05-23 17:09:29 +0800
---

<details  markdown="block">
  <summary>
    Table of contents
  </summary>

1. [登录](#登录)
    1. [SSH 帐号和密码](#ssh-帐号和密码)
    2. [SSH 帐号和公钥](#ssh-帐号和公钥)
2. [常用命令](#常用命令)
    1. [查看命令](#查看命令)
    2. [操作命令](#操作命令)
3. [linux 常识](#linux-常识)
    1. [linux 文件系统](#linux-文件系统)
    2. [linux 哲学](#linux-哲学)
    3. [常见的配置文件和位置](#常见的配置文件和位置)
    4. [linux 常用目录](#linux-常用目录)

</details>

# 登录
## SSH 帐号和密码 

## SSH 帐号和公钥
```bash
ssh-keygen
# 一路回车，生成 id_rsa 和 id_rsa.pub，也可以输入passphrase，来保护 key, 每次使用 key 时都需要输入 passphrase
# 将 id_rsa.pub 的内容添加到 ~/.ssh/authorized_keys 中
cat id_rsa.pub >> ~/.ssh/authorized_keys
# 将 id_rsa 拉到本地，供 xshell 使用 ssh 远程到服务器时使用
``` 
---
# 常用命令
## 查看命令

- 进入 root

```bash
sudo -i
```

- 查看系统信息

```bash
uname -a
```
- 查看用户信息

```bash
whoami
id grissom # 查看 grissom 用户
```
- 查看系统版本

```bash
cat /etc/issue # 查看系统版本
cat /proc/version # 查看内核版本
```
- 查看当前目录

```bash
pwd
```
- 查看当前目录下的文件

```bash
ls
# 包括隐藏文件
ls -a
# 包括隐藏文件，包括文件的详细信息
ls -al

ls -lh # 查看文件大小,人性化显示
```
- 查看端口占用情况

```bash
# 查看所有端口占用情况
netstat -anp
# 查看所有端口占用情况，只显示监听端口
netstat -anp | grep LISTEN
# 查看指定端口占用情况
lsof -i:8080 

ss -anp | grep 8080

ss -tunlp | grep 8080

```
- 查看进程

```bash
ps -e
# 查看所有进程
ps -ef
# 查看zookeeper进程
ps -ef |grep zookeeper 
# 显示cpu,内存,启动时间,命令行,并按内存使用量倒序排序
ps -aux --sort=-%mem
top #实时查看进程, shift+m 按内存排序
```
- 查看日志

```bash
# 查看最后10行日志
tail -n 10 /var/log/messages
# 查看最后10行日志，实时刷新
tail -f -n 10 /var/log/messages
# 查看前面10行日志
head -n 10 /var/log/messages
```
- 查看文件

```bash
# 查看文件内容
cat /var/log/messages
# 查看文件内容，实时刷新
tail -f /var/log/messages
```
- 查看文件大小

```bash
# 查看文件大小
du -sh /var/log/messages
# 查看文件夹大小
du -sh /var/log
dh -h /var/log
dh -h --max-depth=1 # 查看当前目录下的文件夹大小,深度为1

wc [-lmw] [file] # 统计文件的行数、字数、字节数
ls |wc -l # 统计当前目录下的文件个数
```
- 查看磁盘使用情况

```bash
# 查看磁盘使用情况
df -h
```
- 查看内存使用量

```bash
# 查看内存使用量
free -m
```
- 查看系统负载

```bash
# 查看系统负载
uptime
```
- 查看系统时间

```bash
# 查看系统时间
date
```
- 查看系统环境变量

```bash
# 查看系统环境变量
env
```
- 查看防火墙状态

```bash
# 查看防火墙状态
systemctl status firewalld
# 查看防火墙开放的端口
firewall-cmd --list-ports
# 查看防火墙开放的服务
firewall-cmd --list-services

# 查看 ubuntu 防火墙状态
systemctl status ufw
# 查看 ubuntu 防火墙开放的端口
ufw status
# 查看 ubuntu 防火墙开放的服务
ufw status numbered

# 云服务器不需要防火墙,通过安全组来控制端口
```
- 查看命令

```bash
# 查看命令所在位置
which java
whereis java # 查看命令所在位置，包括源码位置，以及配置文件位置
# 查看命令的帮助信息
man java
```

- 查看ip

```bash
# 查看ip
ifconfig
# 查看ip，只显示ip
ifconfig | grep inet | grep -v inet6 | awk '{print $2}'
```

- 查看日志

```bash
# 查看日志
journalctl -u nginx.service
```

## 操作命令
- 用户和用户组管理

```bash
# 修改用户密码
passwd grissom
# 修改系统时间
date -s "2020-01-01 00:00:00"
# 修改系统时区
timedatectl set-timezone Asia/Shanghai
# 修改系统语言
localectl set-locale LANG=zh_CN.UTF-8
# 修改系统主机名
hostnamectl set-hostname grissom
# 添加用户
useradd grissom
# 修改用户密码
passwd grissom
# 添加用户到 sudo 组
usermod -aG sudo grissom
# 添加用户到 root 组
usermod -aG root grissom
# 删除用户
userdel grissom
# 添加用户组
groupadd g1
# 删除用户组
groupdel g1
# 添加用户到用户组
usermod -aG g1 grissom
# 删除用户从用户组
gpasswd -d grissom g1
# 查看用户组
cat /etc/group
# 查看用户
cat /etc/passwd
# 查看用户所在组
cat /etc/group | grep grissom
```

- 创建、删除、修改文件夹

```bash
# 创建文件夹
mkdir -p ./data/{dir1,dir2}
# 删除文件夹
rm -rf ./data/{dir1,dir2}
# 复制文件夹, -r 递归复制，-f 强制覆盖
cp -r ./data/{dir1,dir2} ./data/{dir1.bak,dir2.bak}
# 修改文件权限,4r,2w,1x, 下面命令 owner 分rwx,group 分rx,other 分r
chmod -R 777 ./data/{dir1,dir2}
chmod +x sth.sh # 给文件添加可执行权限
chmod ug-x sth.sh # 给文件删除用户和组的可执行权限
# 修改文件所有者，grissom 是用户名，groupname 是用户组名, 如果用户组不存在，则会创建用户组,也可以不指定用户组
chown -R grissom:grissom ./data/{dir1,dir2}
# 修改文件夹所有者和权限
chown -R grissom:grissom ./data/{dir1,dir2} && chmod -R 777 ./data/{dir1,dir2}
# 文件夹重命名
mv ./data/logs ./data/logs.bak
```
- 创建、删除、修改文件

```bash
# 创建文件
touch ./data/logs/test.log
# 写入文件内容，如果文件不存在，则创建文件，如果文件存在，则追加内容, >> 表示追加，> 表示覆盖
echo "hello world" >> ./data/logs/test.log
# 删除文件
rm -rf ./data/logs/test.log
# 复制文件夹, -r 递归复制，-f 强制覆盖
cp -r ./data/test1/{txt1.txt,txt2.txt} ./data/test2
# 修改文件权限,4r,2w,1x, 下面命令 owner 分rwx,group 分rx,other 分r
chmod 754 ./data/logs/test.log
# 修改文件所有者，grissom 是用户名，groupname 是用户组名, 如果用户组不存在，则会创建用户组,也可以不指定用户组
chown grissom:groupname ./data/logs/test.log
# 修改文件所有者和权限
chown grissom:groupname ./data/logs/test.log && chmod 777 ./data/logs/test.log
# 文件重命名
mv ./data/logs/test.log ./data/logs/test.bak
```

- 批量操作

```bash
# 批量创建文件夹
mkdir -p ./data/{dir1,dir2}
# 批量删除文件夹
rm -rf ./data/{dir1,dir2}
# 批量复制文件夹, -r 递归复制，-f 强制覆盖
cp -r ./data/{dir1,dir2} ./data/{dir1.bak,dir2.bak}
# 批量修改文件权限,4r,2w,1x, 下面命令 owner 分rwx,group 分rx,other 分r
chmod -R 777 ./data/{dir1,dir2}
# 批量执行 shell 文件
find ./data -name "*.sh" | xargs -I {} sh {}
for file in $(ls ./data/*.sh); do sh $file; done

```
---
# linux 常识
## linux 文件系统
文件系统是一种数据结构，用于组织、管理和存储数据
## linux 哲学
 do one thing and do it well, 一个程序只做一件事，做好这件事
## 常见的配置文件和位置
```bash
# /etc/passwd 用户信息，不要直接修改，使用 useradd usermod userdel 等命令来修改
# /etc/shadow 用户密码,不要直接修改，使用 passwd 命令来修改
# /etc/group 用户组信息,不要直接修改，使用 groupadd groupdel 等命令来修改
# /etc/hosts 主机名和ip映射，可以直接修改
# /etc/hostname 主机名，可以直接修改
# /etc/profile 系统环境变量,使用 source /etc/profile 命令来生效
# /etc/my.cnf mysql 配置文件
# /etc/nginx/nginx.conf nginx 配置文件
# /etc/nginx/conf.d/ nginx 配置文件目录
# ~/.bashrc 用户环境变量,使用 source ~/.bashrc 命令来生效
# ~/.bash_profile 用户环境变量,使用 source ~/.bash_profile 命令来生效
# ~/.vimrc vim 配置文件
# ~/.gitconfig git 配置文件
# ~/.ssh/authorized_keys ssh 公钥
# ~/.ssh/id_rsa ssh 私钥
# ~/.ssh/id_rsa.pub ssh 公钥
```
## linux 常用目录
```bash
# /bin 常用命令
# /sbin 系统管理命令
# /etc 配置文件
# /home 用户目录
# /root root 用户目录
# /usr/bin 用户命令
# /usr/sbin 用户系统管理命令
# /usr/local/bin 用户安装的命令
# /var/log 日志目录
# /var/lib/mysql mysql 数据目录
# /var/lib/nginx nginx 数据目录
# /mnt 挂载目录
# /tmp 临时目录
# /proc 进程目录
# /dev 设备目录
# /sys 系统目录
```

