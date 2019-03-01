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

## 快速搭建个人博客

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

主要通过修改`_config.yml`文件配置博客内容：

	## 网站设置
	# 标题
	title: Blog
	# 选项卡标题
	SEOTitle: 周大路的博客 | SuperZhouDalu‘s Blog
	# 首页背景图片
	header-img: img/post-bg-debug.png
	# 邮箱设置
	email: zhoujianlu666@gmail.com
	# 网站介绍
	description: "I guess it comes down to a simple choice:get busy living or get busy dying."
	~~~ ~~~ （内容较多，不适合全部展示，关键配置均有中文注释）

将 `_config.yml` 文件中 `url` 修改为 `https://"你的GitHub用户名" + .github.io`, 清空CNAME文件内容并提交，再将项目名称修改为 `你的GitHub用户名 .github.io` ，如下图

![](http://ww1.sinaimg.cn/large/005yqb1Zly1g0n17uz8d8j31jo0v842k.jpg)

点击 `Rename` 按钮后，你就可以在网页输入 `https://"你的GitHub用户名".github.io`  查看效果了。至此已经完成了一半啦，剩余的就是一些你专属的配置了。

### 撰写文章

要发表的文章一般以 **Markdown** 的格式放在这里 `_posts/`，如果你还不了解 **Markdown** 语法，可以点击[这里](https://markdown-zh.readthedocs.io/en/latest/)进行学习。每篇博客的标头是固定的，以下是的配置内容：


	---
	layout:     post
	title:      这是标题
	subtitle:   这是子标题
	date:       2019-02-26
	author:     SuperZhouDalu
	header-img: img/post-bg-coffee.jpeg
	catalog: true
	tags:    
	        - 标签
	---
    
	## 标题
	### 内容

### 侧边栏

看右边：

![](http://ww1.sinaimg.cn/large/005yqb1Zly1g0n18koc6hj31jo0v8n1y.jpg)

关于侧边栏的设置是在 `_config.yml` 中：

	## 侧边栏设置
	# 是否开启侧边栏 true 开始 false 关闭
	sidebar: true
	# 侧边栏描述语句
	sidebar-about-description: "知识就是力量。"
	# 侧边栏头像
	sidebar-avatar: /img/sidebar-avatar.jpg

侧边栏是响应式布局的，当屏幕尺寸小于992px的时候，侧边栏就会移动到底部。具体请见bootstrap[栅格系统](http://v3.bootcss.com/css/)。

### 推荐标签

推荐标签位于侧边栏首部，针对博客的tags进行分类。相关配置在 `_config.yml` 中：

	## 标签设置
	# 是否使用首页标签
	featured-tags: true
	# 相同标签数量大于这个数，才会出现在首页
	featured-condition-size: 0
    
唯一需要注意的是`featured-condition-size`: 如果一个标签的 SIZE，也就是使用该标签的文章数大于上面设定的条件值，这个标签就会在首页上被推荐。
内部有一个条件模板 `{% if tag[1].size > {{site.featured-condition-size}} %}` 是用来做筛选过滤的。

### 社交账号

![](http://ww1.sinaimg.cn/large/005yqb1Zly1g0n18vvg9ej307s01t0sl.jpg)

目前支持`微博`、`知乎`、`GitHub`、`Facebook`、`简书`、`Twitter`社交账号链接，未罗列的暂不支持，可以自己手动集成。相关配置在 `_config.yml` 中：

	## 社交网站设置
	RSS: false
	# 微博 打开个人主页截取用户编号 例如个人主页网址为https://weibo.com/u/5089298519 填写 5089298519
	weibo_username:     5089298519
	# 知乎个人页面 填写用户名
	zhihu_username:     username
	# GitHub个人页面 填写用户名
	github_username:    username
	# facebook个人页面 填写用户名
	facebook_username:  username
	# 简书个人页面截取用户编号 与微博同理
	jianshu_username:   56a2c6b6027c
	# twitter个人页面 填写用户名
	twitter_username:   zhoudalu

### 好友链接

好友链接部分会在所以页面展示，相关配置在 `_config.yml` 中：

	## 友情链接
	friends: [    
  	  {       
   	     title: "帅超",
   	     href: "https://github.com/shuaichaoA" 
  	  },
  	  {        
   	     title: "鸡大婶",        
   	     href: "https://github.com/ruinszero"    
  	  },
  	  {        
  	      title: "Apple",
  	      href: "https://apple.com"   
	    },
	   {        
	       title: "Apple Developer",   
	       href: "https://developer.apple.com/"   
	   }
	]
