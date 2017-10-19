---
title: github上搭建个人主页
date: 2017-08-23 15:53:39
tags: 随笔
---
1. 在github上创建并设置远程库，名字：chenfengjuan.github.io,（名字必须是这个）
2. 本地建立chenfengjuan.github.io文件夹，这个文件夹，必须为空
3. 在chenfengjuan.github.io目录下执行hero init
4. 安装相关依赖
`npm install hexo —save`
`nam install`
5. 运行  `hero g`
这行命令是加载`hexo`基础`html`、`css`、`js`等文件。
在这完成后等于已经在本地创建了一个网页，想查看的话，输入`hexo s`，相当于在本地起了个服务器，在浏览器输入 `http://localhost:4000/`，就会看到默认的页面了，证明本地`hexo`默认模板配置成功
6. 修改站点配置文件，在根目录`_config.yml`文件中 
```
# Site
title: 网站标题
subtitle: 副标题
description: 个人签名
author: 姓名
language: zh-Hans
timezone:
# 同时还有
deploy:
  type: git
  repo: https://github.com/chenfengjuan/chenfengjuan.github.io.git
  branch: master
  ```
7. 接下来就可以提交项目部署了，继续在chenfengjuan.github.io目录下执行下面的命令，安装部署工具（方便以后更新）
`npm install hexo-deployer-git —save`
8. 初始化本地仓库：
`git init`
9. 发布hexo到github page
`hexo clean && hexo g && hero d`
这一步执行后hexo会自动在你的这个`chenfengjuan.github.io`仓库的`master`分支下生成你的主页的静态html文件。
这个时候其实你只要在浏览器里访问`chenfengjuan.github.io`，就可以看到你的主页了
10. 为了保存我们的文章不因为换电脑等原因丢失，也就是本地的这个`chenfengjuan.github.io`文件夹的内容不丢失,我们可以在`https://github.com/username/username.github.io.git`,这个仓库下创建的`hexo`的分支
创建并切换到新建分支：
`git checkout -b hexo`
将分支推送到远程仓库：
`git push origin hero`
这个分支保存了我们的文章的原始文件等。
11. 新建文章,请用下面的命令
`hexo new "new article"`
之后在本地的`chenfengjuan.github.io`文件夹下的`source/_posts`目录下面，多了一个new-article.md的文件。打开之后就会开到自动生成的标题等内容，你只要在下面编写正文就可以了，正文支持markdown格式，建议你先学习一下它的语法。markdown不像html似的一大堆标签，很简单，只有几个符号。
12. 新建文章后，发布到你的github page就可以了
`hexo clean && hexo g && hexo d`
