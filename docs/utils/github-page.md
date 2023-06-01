---
layout: default
title: Github Page
parent: Utils
last_modified_date:   2023-05-26 14:56:29 +0800
---
<details  markdown="block">
  <summary>
    TOC
  </summary>

<!-- TOC -->

- [Github Page](#github-page)
    - [优点](#优点)
    - [缺点](#缺点)
    - [注意事项](#注意事项)

<!-- /TOC -->

  </details>

# Github Page
---
Github Page 是把托管在 github 仓库的个人网站发布到 github.io 上的服务。
## 优点
1. 免费
2. 支持 markdown
3. 支持自定义域名
4. 支持 devops  
5. 永久有效（随着github灭忙）
6. 支持 jekyll 模板
7. 很多theme 可选

## 缺点
1. 只能是静态网站， 不能使用后端语言，不能使用数据库
2. 免费仓库必须是公开的，不能是私有的
3. github.io 有被墙的风险
4. 不利于推广


## 注意事项

1. 仓库名必须是：[username].github.io
2. 可以在 .github/workflows 文件夹配置 github actions
3. 仓库默认有一个 build and deploy 的 github actions，可以在 settings 中关闭
4. 如果使用 github 自带的action, 注意在 _config.yml 中配置 remote_theme 而不是 theme










