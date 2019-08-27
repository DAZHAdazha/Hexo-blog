# Hexo blog 的搭建 以及主题 yilia 的应用

## Hexo 简介

> * Hexo 是基于Node.js的个人博客框架，可以方便的部署到Github等网站上，且支持markdown格式书写，以及更换主题等功能

## Hexo 搭建

>1. 安装Node.js
>   [下载地址](nodejs.org) 选择LTS长期支持版
>
>2. 打开Git Bash（推荐）或cmd 切换至root 用户 并输入`npm -v`查看包管理器版本号
>
>3. 安装cnpm（淘宝的源，国内用npm的国外源太慢）
>
>   输入`npm install -g cnpm --registry=https://registry.npm.taobao.org`指令
>
>4. 安装hexo框架
>
>   输入`cnpm install -g hexo-cli`
>
>5. 查看hexo版本
>
>   输入`hexo -v`
>
>6. 建立blog文件夹并进入目录
>
>   输入`mkdir blog`+`cd blog`
>
>7. 生成hexo 博客
>
>   输入`sudo hexo init`
>
>8. 启动hexo博客本地服务器
>
>   输入`hexo s`(hexo server的简写)
>
>   并用浏览器进入 localhost:4000 网页
>
>9. 新建hexo 文章
>
>   输入`hexo n '文章名字'`
>
>10. 重新部署
>
>    输入`hexo clean`+`hexo g`(hexo generate)+ `hexo s`

## 部署到Github

> 1. 在Github上创建仓库，命名为`GithubID.github.io`(GithubID是你账号的名称)非常重要，名称必须按照规范
>
> 2. 打开Git Bash(cmd)
>
>    输入`cnpm install  hexo-deployer-git--save`
>
> 3. 打开blog根目录，找到_config.yml文件并打开
>
>    找到底端 #Deployment 行进行配置
>
>    type: git
>
>    repo: https://github.com/GithubID/GithubID.github.io.git (自己Github仓库的地址)
>
>    branch: master
>
>    **注： type repo branch 冒号后面一定要加空格！**
>
> 4. 部署到远端服务器
>
>    输入`hexo d`(hexo deploy)

## 应用yilia主题

>1. 输入`git clone https://github.com/litten/hexo-themo-yilia.git themes/yilia`(需要进入blog 根目录)
>
>2. 找到 yilia文件夹中_config.yml文件并打开进行配置
>
>   找到 #Extensions 中theme一行 并改为theme: yilia（**注意空格！**）
>
>3. 执行重新部署 `hexo clean | hexo g | hexo d`

## 个性化设置

> 1. 更改默认字体
>
>    找到yilia/source文件夹中的`main.0c68a.css`文件 找到header-author 对font-family的行进行更改即可
>
> 2. 在左侧边栏显示总文章数
>
>    找到themes\yilia\layout_partial\left-col.ejs
>
>    在
>
>    ```html
>    <nav class="header-menu">
>        <ul>
>        <% for (var i in theme.menu){ %>
>            <li><a href="<%- url_for(theme.menu[i]) %>"><%= i %></a></li>
>        <%}%>
>        </ul>
>    </nav>
>    ```
>
>    后面加入
>
>    ```html
>    <nav>
>        总文章数: <%=site.posts.length%>
>    </nav>
>    ```
>
>    **注意编码模式要将ANSI改为utf-8，否则无法使用中文！**
>
> 3.  添加字数统计功能
>
>    首先需要安装 hexo-wordcount
>
>    使用命令`cnpm i --save hexo-wordcount`
>
>    找到themes\yilia\layout_partial\article.ejs
>
>    在header下添加
>
>    ``` html
>    <div align="center" class="post-count">
>        字数：<%= wordcount(post.content) %>字 | 预计阅读时长：<%= min2read(post.content) %>分钟
>    </div>
>    ```
>
>    （**同样改成utf-8编码**）
>
> 4. 去除网页右下角powered by hexo等字样
>
>    找到themes/next/layout/_partials/footer.swig文件，并使用<--! 注释 -->注释掉即可