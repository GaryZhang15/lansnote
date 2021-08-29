---
title: "Hugo"
date: 2021-08-28T13:28:11+08:00
draft: false
---

hugo静态网站生成器，如果单纯是想用来写点东西还是蛮合适的。我用下来，初步感受是，单纯写点东西，还算比较好上手。但是，如果自定义的东西多一点的话，学习成本还是不少的，hugo有自己的一套体系和设计逻辑。

总之，适合专注内容创作。如果对节目的动态特性需求较多，那么不太适合，毕竟也不是hugo的设计初衷。


> - 本文适用于 ubuntu 20.04，需要有Linux操作基础，基本的网络技术，有Azure的账号
> - 第一部分 - 快速入门
> - 第二部分 - 如何部署到Azure Static Web Site
> - 第三部分 - 如何在第二台电脑上同步编辑

### 第一部分 - 快速入门
1. 如何安装
    ```bash
    sudo apt-get install hugo
    ```
2. 创建新站点
    ```bash
    hugo new site mysite
    ```
3. 添加主题
    ```bash
    cd mysite
    git init
    git submodule add https://github.com/theNewDynamic/gohugo-theme-ananke.git themes/ananke
    echo theme=\"ananke\" >> config.toml
    ```
4. 添加第一篇文章
   ```bash
   hugo new posts/mypost.md
   ```
5. 启动网站
    ```bash
    hugo server -D
    ```
6. 修改主题参数
    ```bash
    baseURL = "https://example.com"
    languageCode = "en-us"
    title = "My Site"
    theme = "ananke"
    ```
7. 生成静态网页
    ```bash
    hugo -D
    ```

### 第二部分 - 如何部署到Azure Static Web Site
// TO DO
![B2B](/azure_b2b_auth_flow.jpg "Azure B2B auth flow")


### 第三部分 - 如何在第二台电脑上同步编辑
1. 第二台电脑确保安装好 Git
2. 执行下面git命令clone你的代码库, **注意**要加上`recursive`参数，这样你的主题模块也会被同步下来 
    ```bash
    git clone https://github.com/GaryZhang15/lansnote --recursive
    ```
3. 接下来就可以编辑文章
4. 需要同步文章的时候执行下面命令
    ```bash
    git add .
    git commit -m 'my change is ***' // 记录你的变更
    git push // 将你的变更推向github代码仓库
    ```
5. 新的文章就发布到github了，Azure Static Site会自动重新下载新的内容。其他的电脑需要使用`git pull`来拉取这些变更
