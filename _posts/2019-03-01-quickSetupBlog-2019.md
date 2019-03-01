---
layout:     post
title:      快速搭建个人博客
subtitle:   极其简单的搭建教程
date:       2019-03-01
author:     SuperZhouDaLu
header-img: img/post-github-cup.jpg
catalog: true
tags:                              
    - 笔记
---


![](http://ww1.sinaimg.cn/large/005yqb1Zly1g0n18e6qehj31jo0v8wj0.jpg)

>
### 前言

博客使用 [GitHub Pages](https://pages.github.com/) + [jkeyll](http://jekyllcn.com/) 搭建，配置极其简单，搭建完成仅需不到半小时。

>
### 支持
* 你可以自由的转载。如果你能将主题作者和博客的地址保留在你的页面底部，我将非常感谢你。
* 如果你喜欢我的这个博客模板，请在 [这个repository](https://github.com/superZhouDaLu/superzhoudalu.github.io) 点个赞——右上角 ***star*** 一下。

>
## 使用
* 开始
    * [起步](#起步)
    * [开始](#开始)
    * [撰写文章](#撰写文章)
 * 组件
    * [侧边栏](#侧边栏)
    * [推荐标签](#推荐标签)
    * [社交账号](#社交账号)
    * [好友链接](#好友链接)
 * 评论与 Google/Baidu Analytics
    * [评论](#评论)
    * [网站分析](#网站分析)
    
### 起步
![](http://ww1.sinaimg.cn/large/005yqb1Zly1g0n1697dd8j31jo0v80we.jpg)

首先你需要点击跳转到 [我的仓库](https://github.com/superZhouDaLu/superzhoudalu.github.io)，点击右上角 **fork** 按钮将此项目拉取到你的仓库下。

**[:arrow_up: 返回导航](#使用)**

### 开始

``` shell
├── _includes                 // 公共页面
│   ├── footer.html           // 底部页面 
│   ├── head.html             // 头部页面
│   ├── nav.html              // 导航栏页面
├── _layouts                  // 页面布局
├── _posts                    // 存放博客（仅支持markdown格式）
├── css                       // css样式
├── fonts                     // 引入字体
├── img                       // 图片资源
├── js                        // js函数
├── less                      // less样式
├── pwa                       // pwa配置
├── .gitignore                // git忽略文件
├── .travis.yml               // Travis CI配置文件
├── 404.html                  // 404页面
├── CNAME                     // 域名解析文件
├── Gruntfile.js              // Gruntfile插件构建
├── LICENSE                   // 许可文件
├── README.md                 // 项目简介
├── _config.yml               // 主配置文件
├── about.html                // '关于我'页面
├── feed.xml                  // jekyll相关
├── index.html                // 主页面
├── offline.xml               // 网络离线页面
├── package.json              // package依赖
├── sw.js                     // scoket相关
└── tags.html                 // '关键字'页面
```  