---
# 博客题目
title: 创建自己的WIKI
# 博客写作日期
date: 2024-10-11
categories: stellar
tag: [hexo,wiki]
---

`Stellar`拥有`wiki`系统，我们可以使用它构建自己的知识体系。下面来说说如何在`Staller`主题下搭建`Wiki`。
## 介绍
`Stellar` 的Wiki 文档系统，可以自动找到一个项目的所有文档分页，生成一个目录树，还可以手动指定顺序、标题、分组，而非依赖文件路径、文件名来排序和显示。
## 创建步骤
### 创建项目描述文件
在`blog/source/_data/` 文件夹中创建一个`wiki`文件夹，创建文档系统主题的`yml`文件：
![](https://gitee.com/wc2017/blog-img/raw/master/20241010/170626602-image-20241010170615933-eebad.png)
`yml`文件中的内容

```
name: Android # 项目名称前缀  
title: Android UI篇 # 项目名称  
subtitle: '我去前面探探路 | 要迅捷！' # 头像右边文案  
tags: Android # 项目所属TAG ,也可以设置多个 tags 值：[TAG1,TAG2] 
icon: https://gitee.com/wc2017/blog-img/raw/master/20241010/123902752-android_icon-3f5b6.jpeg  # 列表图标  
cover: https://gitee.com/wc2017/blog-img/raw/master/20241010/124033380-android_icon封面-c9bd6.jpg # 封面图标  
coverpage: true #是否显示全屏封面  
description: 本系列是Android的View篇，包括自定义View，画笔，路径，事件分发，View的绘制原理等，完成本系列，就再也不怕Android的View了 # 项目描述  
search:  # 设置项目搜素范围  
  filter: /wiki/androidui/  
  placeholder: 在 Android 中搜索...  
leftbar: # 侧边栏配置  
  - tree  
  - timeline_stellar_releases  
  - related  
comment_id: 10000 # 评论id  
  
# 这里可以单独配置wiki使用的评论系统  
#comments:  
#  service: giscus  
#  giscus:  
#    data-repo: Timor2016/gid-commen  
#    data-mapping: pathname  
#    data-term: 226  
  
base_dir: /wiki/android/ # 项目所在文件夹  
  
# 项目文档树  
tree:  
  '快速开始':  
    - index  
    - examples  
    - releases  
  '基本使用':  
    - theme-settings  
    - pages  
    - sidebar  
    - tag-plugins  
    - tag-plugins/express  
    - tag-plugins/data  
    - tag-plugins/container  
    - comments  
  '文档系统':  
    - wiki-settings  
  '进阶玩法':  
    - widgets  
    - advanced-settings  
    - notes  
    - fcircle  
  '技术支持':  
    - articles  
    - todo  
    - contributors
```
各个的说明很详细了。
### 设置布局和项目名称
创建项目文档的文件夹，并创建`.md`文件,
![](https://gitee.com/wc2017/blog-img/raw/master/20241010/171856891-image-20241010171852019-39ed6.png)在此文档项目的`md`文件的`front-matter`部分指定所属的项目`id`（即上一步创建的文件名`id.yml`）

```
---  
wiki: androidUi # 这是项目id，对应 /data/wiki/handroidUi.yml  
title: 这是分页标题  
---
```
### 上架项目
在`blog/source/_data/`文件夹中创建一个`wiki.yml`文件，在其中写入需要显示的项目`id`：

```
- androidUi  
- 其它项目
```

### 项目的Github仓库信息
在项目的描述文件`.yml`中配置
设置了`repo`值就会在右上角显示项目仓库的相关链接：
```
repo: xaoxuu/hexo-theme-stellar
```
### 在目录树中隐藏某篇文件
可以在文章的`.md`文件中设置`front-matter`中不设置`title`标题，或者将`title`改为`seo_title`

这样你就拥有了一个自己的文档系统