---
title: "Hugo"
date: 2021-08-28T13:28:11+08:00
draft: false
---

hugo静态网站生成器

> 本文适用于 ubuntu 20.04

1. 如何安装
    `sudo apt-get install hugo`
2. 创建新站点
    `hugo new site mysite`
3. 添加主题
    ```
    cd mysite
    git init
    git submodule add https://github.com/theNewDynamic/gohugo-theme-ananke.git themes/ananke
    echo theme=\"ananke\" >> config.toml
    ```
4. 添加第一篇文章
   `hugo new posts/mypost.md`
5. 启动网站
    `hugo server -D`
6. 修改主题参数
    ```
    baseURL = "https://example.com"
    languageCode = "en-us"
    title = "My Site"
    theme = "ananke"
    ```
7. 生成静态网页
    `hugo -D`
