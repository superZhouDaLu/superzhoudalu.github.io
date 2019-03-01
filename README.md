![](http://ww1.sinaimg.cn/large/005yqb1Zly1g0n18e6qehj31jo0v8wj0.jpg)

[![Build Status](https://travis-ci.org/superZhouDaLu/superzhoudalu.github.io.svg?branch=master)](https://travis-ci.org/superZhouDaLu/superzhoudalu.github.io)
[![GitHub issues](https://img.shields.io/github/issues/superZhouDaLu/superzhoudalu.github.io.svg?style=flat)](https://github.com/superZhouDaLu/superzhoudalu.github.io/issues)
[![License MIT](https://img.shields.io/badge/license-MIT-blue.svg?style=flat)](https://github.com/superZhouDaLu/superzhoudalu.github.io/blob/master/LICENSE)
[![](https://img.shields.io/github/stars/superZhouDaLu/superzhoudalu.github.io.svg?style=social&label=Star)](https://github.com/superZhouDaLu/superzhoudalu.github.io)
[![](https://img.shields.io/github/forks/superZhouDaLu/superzhoudalu.github.io.svg?style=social&label=Fork)](https://github.com/superZhouDaLu/superzhoudalu.github.io)

博客的搭建教程修改自 [qiubaiying](https://github.com/qiubaiying/qiubaiying.github.io)

>
### [查看博客戳这里 👆](https://aigq.me)

>
### 支持
* 你可以自由的fork。如果你能将主题作者和 github 的地址保留在你的页面底部，我将非常感谢你。
* 如果你喜欢我的这个博客模板，请在这个repository点个赞——右上角 ***star*** 一下。

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

博客使用 [GitHub Pages](https://pages.github.com/) + [jkeyll](http://jekyllcn.com/) 搭建，配置极其简单，搭建完成仅需不到半小时。首先点击右上角 **fork** 按钮将此项目拉取到你的仓库下。

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

主要通过修改`_config.yml`文件配置博客内容：

```
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
```
将 `_config.yml` 文件中 `url` 修改为 `https://"你的GitHub用户名" + .github.io`, 清空CNAME文件内容并提交，再将项目名称修改为 `你的GitHub用户名 .github.io` ，如下图

![](http://ww1.sinaimg.cn/large/005yqb1Zly1g0n17uz8d8j31jo0v842k.jpg)

点击 `Rename` 按钮后，你就可以在网页输入 `https://"你的GitHub用户名".github.io`  查看效果了。至此已经完成了一半啦，剩余的就是一些你专属的配置了。

**[:arrow_up: 返回导航](#使用)**

### 撰写文章

要发表的文章一般以 **Markdown** 的格式放在这里 `_posts/`，如果你还不了解 **Markdown** 语法，可以点击[这里](https://markdown-zh.readthedocs.io/en/latest/)进行学习。每篇博客的标头是固定的，以下是的配置内容：

```
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
```
**[:arrow_up: 返回导航](#使用)**

### 侧边栏

看右边：

![](http://ww1.sinaimg.cn/large/005yqb1Zly1g0n18koc6hj31jo0v8n1y.jpg)

关于侧边栏的设置是在 `_config.yml` 中：

```
## 侧边栏设置
# 是否开启侧边栏 true 开始 false 关闭
sidebar: true
# 侧边栏描述语句
sidebar-about-description: "知识就是力量。"
# 侧边栏头像
sidebar-avatar: /img/sidebar-avatar.jpg
```

侧边栏是响应式布局的，当屏幕尺寸小于992px的时候，侧边栏就会移动到底部。具体请见bootstrap[栅格系统](http://v3.bootcss.com/css/)。

**[:arrow_up: 返回导航](#使用)**

### 推荐标签

推荐标签位于侧边栏首部，针对博客的tags进行分类。相关配置在 `_config.yml` 中：

```
## 标签设置
# 是否使用首页标签
featured-tags: true
# 相同标签数量大于这个数，才会出现在首页
featured-condition-size: 0
```
唯一需要注意的是`featured-condition-size`: 如果一个标签的 SIZE，也就是使用该标签的文章数大于上面设定的条件值，这个标签就会在首页上被推荐。
内部有一个条件模板 `{% if tag[1].size > {{site.featured-condition-size}} %}` 是用来做筛选过滤的。

**[:arrow_up: 返回导航](#使用)**

### 社交账号

![](http://ww1.sinaimg.cn/large/005yqb1Zly1g0n18vvg9ej307s01t0sl.jpg)

目前支持`微博`、`知乎`、`GitHub`、`Facebook`、`简书`、`Twitter`社交账号链接，未罗列的暂不支持，可以自己手动集成。相关配置在 `_config.yml` 中：

```
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
```
**[:arrow_up: 返回导航](#使用)**

### 好友链接

好友链接部分会在所以页面展示，相关配置在 `_config.yml` 中：

```
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
```
**[:arrow_up: 返回导航](#使用)**

### 评论

博客目前支持 [Disqus](http://disqus.com)和[Gitalk](https://gitalk.github.io/) 评论系统。

#### Disqus

优点：配置简单，国际比较流行，界面也很大气、简洁，如果有人评论，还能实时通知，直接回复通知的邮件就行了。

缺点：评论必须要去注册一个disqus账号，分享一般只有Facebook和Twitter，并且在国内被墙了。

**使用：**

1. 前往[disqus官网](https://disqus.com/)注册一个属于自己的账号。
2. 进入[设置页面](https://disqus.com/home/settings/profile/)配置个人信息：
 ![](http://ww1.sinaimg.cn/large/005yqb1Zly1g0n19onbuhj31jo0v8tdk.jpg)
3. 在左侧菜单栏选择 `Account` ，并找到 `Username` 。
 ![](http://ww1.sinaimg.cn/large/005yqb1Zly1g0n19yzb04j31jo0v8dju.jpg)
`Username`  对应着 `_config.yml` 中  `disqus_username` ：
```
# Disqus（https://disqus.com/）
disqus_username: superZhoudalu
```

#### Gitalk

优点：界面干净简洁，利用 Github issue API 做的评论插件，使用 Github 帐号进行登录和评论，最喜欢的支持 Markdown 语法，对于程序员来说真是太 cool 了。

缺点：配置比较繁琐，每篇文章的评论都需要初始化。

**使用：**

1. Gitalk 需要一个 Github Application，[点击这里申请](https://github.com/settings/applications/new)。填写以下参数：
 ![](http://ww1.sinaimg.cn/large/005yqb1Zly1g0n1a9u9c8j31jo0v8jw0.jpg)
2.  点击创建，会生成 `Client ID` 和 `Client Secret`，填入 `_config.yml` 下列的参数内
```
## Gitalk
gitalk:  
    #是否开启Gitalk评论  
    enable: true  
    #生成的clientID 
    clientID: `Github Application clientID`
    #生成的clientSecret 
    clientSecret: `Github Application clientSecret`
    #仓库名称  
    repo: `GitHub仓库名`
    #github用户名  
    owner: `GitHub用户名`  
    admin: `GitHub用户名`  
    #是否启用类似FB的阴影遮罩  
    distractionFreeMode: true
```
3. 点开任意一篇博客就会显示聊天框啦，随意输入内容进行讨论吧。

**[:arrow_up: 返回导航](#使用)**

### 网站分析

统计目前集成了 百度统计 和 Google Analytics 两种方式，在相应官网绑定自己的博客网站信息后可以拿到 `track_id`，然后填写到对应的  `_config.yml`  中：

```
## 统计
# Baidu Analytics
ba_track_id: b50bf2b12b5338a1845e33832976fd68

# Google Analytics
ga_track_id: 'UA-135281137-1'
# 默认的是 auto, 这里我是自定义了的域名，你如果没有自己的域名，需要改成auto
ga_domain: https://aigq.me
```
**[:arrow_up: 返回导航](#使用)**

## 致谢

1. 这个模板是从这里 [qiubaiying](https://github.com/qiubaiying/qiubaiying.github.io) fork 的, 感谢这个作者。
2. 感谢 Jekyll、Github Pages 和 Bootstrap!
3. 转载请注明出处，喜欢的话帮忙点个 **Star** 再走呗。

## License

遵循 MIT 许可证。有关详细,请参阅 [LICENSE](https://github.com/superZhouDaLu/superzhoudalu.github.io/blob/master/LICENSE)。
