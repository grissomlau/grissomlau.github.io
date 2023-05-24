---
layout: default
title: SSL SSH Login
parent: Security
nav_order: 2
last_modified_date:   2023-05-23 17:09:29 +0800
---

<details  markdown="block">
  <summary>
    TOC
  </summary>

1. [申请免费的ssl证书](#申请免费的ssl证书)
    1. [国内的阿里云、腾讯云、百度云等](#国内的阿里云腾讯云百度云等)
    2. [国外的letsencrypt](#国外的letsencrypt)
    3. [cloudflare](#cloudflare)
    4. [freessl.cn](#freesslcn)
    5. [freessl.org](#freesslorg)
    6. [openssl 工具](#openssl-工具)
2. [github](#github)
    1. [配置代理](#配置代理)
    2. [登录方式](#登录方式)
        1. [使用 personal access token 登录](#使用-personal-access-token-登录)
        2. [SSH](#ssh)
</details>

# 申请免费的ssl证书
## 国内的阿里云、腾讯云、百度云等
都有免费的ssl证书，最长有效期1年，但是需要备案，备案需要花钱和实名制，所以这里不推荐使用。
## 国外的letsencrypt
可以申请免费的ssl证书，有效期3个月，但是可以自动续期，所以这里推荐使用。  
需要安装certbot，将nginx.cnf交给她管理，到期后自动续期。  
也可以手动生成证书，但是需要手动续期。
## cloudflare 
可申请 15 年有效期的免费 ssl 证书，但需要开启 cloudflare 的代理，它的代理免费，也有收费CDN。
## freessl.cn
可申请 1 年有效期的免费 ssl 证书，不用备案但需要实名制。
## freessl.org
可生成 90 天有效期的免费 ssl 证书，不用备案也不用实名制。
## openssl 工具
生成自签名证书，不用备案也不用实名制，但是浏览器会提示不安全。小批量客户使用，可以手动导入CA证书到windows系统，避免提示不安全。

---
# github
## 配置代理
修改 .gitconfig 文件，添加如下内容：
```bash
[http]
    proxy = http://127.0.0.1:1080
```
1080 是你的 http 代理端口，如果是 socks5 代理，修改为：
```bash
[http]
    proxy = socks5://127.0.0.1:1080
```
1080 是你的 socks5 代理端口。

除非你的代理是全局代理，否则需要配置 git 使用代理，否则 git 会直接访问 github，导致无法访问。  
而浏览器之所以可以访问 github，是因为浏览器会自动使用系统代理，所以不需要手动配置。

## 登录方式
### 使用 personal access token 登录
推荐使用 https， 因为它可以绕过防火墙。参考[https://github.com/settings/tokens](https://github.com/settings/tokens)。 
windows credential manager 会保存密码，不用每次都输入密码。如果要删除登录，删除 credential manager 中的 github.com 的密码即可。也可以登录github.com 删除 personal access token。
### SSH
使用 ssh 登录，需要先生成 ssh key，然后将公钥添加到 github.com 的 ssh key 中，参考[https://github.com/settings/keys](https://github.com/settings/keys)。
