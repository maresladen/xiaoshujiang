---
title: Appveyor构建指南
tags: 新建,模板
date: 2017-09-11
grammar_cjkRuby: true
---



## 前言
上篇 [博客搭建指南][1] 讲述了如果通过Hexo搭建博客，在文章最后给出了大神的blog链接，用于自动化构建主题和html。由于参考大神的文章需要不少自行操作，现在这篇文章是更简化的操作~~展示Ctrl+V的力量~~。

## 为什么要自动构建

 1. 只关注markdown的编写
 2. 好一点markdown编辑器，基本都有绑定Github的功能，保存markdown到Github，实现自动发布博客

## Appveyor是什么
Appveyor是一个CI Service，后面我就不详细解释了。请原凉我的懒惰，不了解这个你也不会看到这里了。

## 干货

+ 在[Github][4]建立博客仓库，这个仓库就是通过Hexo搭建的博客的内容
+ 在Appveyor[注册][3]
+ 将Github[绑定][2]到Appveyor上，这步操作，将建立一个Project
	+ 在Project的setting选项中的General中，找到`Webhook URL`项目，记录下这个钩子的路径，待会儿需要在github的设置中需要使用
	+ 在Project的setting选项中的Environment上设置下图的四个变量(`GIT_USER_EMAIL`，`GIT_USER_NAME`，`STATIC_SITE_REPO`，`TARGET_BRANCH`)，这四个变量的意思如果不懂可以用翻译软件，照抄(如果修改则要修改后续我这里提供的yml的编码)，需要详细说明的是`STATIC_SITE_REPO`这个值是用于做博客的仓库，也可以是源码的那个仓库，只需要把BRANCH区分开就可以了。

![环境设置](http://or8fufrdd.bkt.clouddn.com/20170911230240_l4XndR_Screenshot.jpeg)

+ 在Github的源码仓库配置CI钩子，即上方记录下的钩子，具体目录在Setting - Webhooks 中拷贝进去即可
+ 请下载这个[配置文件][5]，打开并修改其中的`secure`配置项，这里的值是你Github的token，需要在[这里][6]生成，这份文件生成完毕之后，拷贝到自己的Hexo项目根目录中，就是和_config.yml同级的目录

+ 通过命令行或者SourceTree或者其他Git工具push你的源文件代码，这时你就可以登录Appveyor看到构建过程，当然你也可以自行增加Hexo插件，修改Appveyor.yml的代码自行增减NPM包

## 给我一首歌的时间


<div class="aplayer" data-id="185821" data-server="netease" data-type="song"></div>

++代码是这样的++
```javascript

<div class="aplayer" data-id="185821" data-server="netease" data-type="song"></div>

```

这是我加的一个音乐的插件，出于尊敬给出源博客的[地址][7]，下载[Aplay.js][8]和[Player.js][9]，放的具体位置和用的主题有关，像我的NexT主题是放在layout的`_script`下的`vendor.swig`的最后，形式如下
```javascript
  <script type="text/javascript" src="/myblog/js/src/APlayer.min.js"></script>
  <script type="text/javascript" src="/myblog/js/src/player.js"></script>
```

具体情况各有不同，这个就要靠自己了


## 最后

再推一波[小书匠][10]，虽然因为更新4.0，他把我所有的草稿全冲没了...但是好东西仍然值得推广。好用的markdown编辑器很多，我用下来这个是功能最齐全的。











[1]:https://maresladen.github.io/myblog/2017/09/01/%E5%8D%9A%E5%AE%A2%E6%90%AD%E5%BB%BA%E6%8C%87%E5%8D%97/
[2]:https://ci.appveyor.com/projects/new
[3]:https://ci.appveyor.com/signup
[4]:https://github.com/
[5]:http://or8fufrdd.bkt.clouddn.com/appveyor.yml
[6]:https://github.com/settings/tokens
[7]:https://www.tiexo.cn/aplayer/
[8]:https://cdn.bootcss.com/aplayer/1.6.0/APlayer.min.js
[9]:https://api.i-meto.com/music/player.js
[10]:http://soft.xiaoshujiang.com/