---
title: typora+picgo+gitee 搭建免费图床
date: 2024-07-01 22:28:13
#img: http://imgstore.chaochaoke.top/cover.png
categories: picgo
tags:
  - typora
  - picgo
  - gitee
---

## 破解安装Typora

请看[Typora 1.8.10.0 破解方法](https://blog.chaochaoke.top/2024/04/17/TyporaCracking/)

## 安装PicGo

1. [下载PicGo](https://github.com/Molunerfinn/PicGo/releases)

2. 正常安装即可

3. 下载gitee插件（注意：PicGo的插件都依赖于nodejs，所以在此之前要先确保[nodejs环境]()已经配置好了）

   1. 在插件设置中搜索 gitee 并安装

      ![39a504fc-b6dc-4eb5-8c08-8518c2abab71](https://gitee.com/wc2017/blog-img/raw/master/20240628/125948271-125632667-39a504fc-b6dc-4eb5-8c08-8518c2abab71-e5618-bd70e.jpeg)

   2. 安装图片压缩插件

      搜索 `tinyping `并安装，打开 [tinyping](https://tinypng.com/),复制 `API KEY` 点击 配置，并将key 粘贴进去即可，后续上传图片到gitee 时就会先使用t inyping压缩

      ![efc5e10e-ace8-498a-ba78-03271ab3568e](https://gitee.com/wc2017/blog-img/raw/master/20240701/124423132-efc5e10e-ace8-498a-ba78-03271ab3568e-84d91.jpeg)
   
      ![截屏2024-07-01 12.45.46](https://gitee.com/wc2017/blog-img/raw/master/20240701/124626993-截屏2024-07-01 12.45.46-01d3c.png)
   
      ​	![20240701-125431](https://gitee.com/wc2017/blog-img/raw/master/20240701/125456289-20240701-125431-02234.png)
   
   3. 安装修改上传名称插件
   
      搜索[rename-file](https://github.com/liuwave/picgo-plugin-rename-file#readme)并安装， 并修改想要的名称的格式即可，不过，这里需要关闭`PicGo` 的重命名才可以
   
   ### 说明
   
   如果插件直接安装失败，我们可以选择导入本地插件，选择下载的源码（源码要执行 `npm install`下载对应的插件）
   
   []: 
   
   ![20240701-130348](https://gitee.com/wc2017/blog-img/raw/master/20240701/130404775-20240701-130348-d5465.png)

## Typora配置PicGo

找到`Typora` 的设置，并配置上传服务选择PicGo.app 即可 

![4372024c-f62e-46b0-8617-d4b21a289531](https://gitee.com/wc2017/blog-img/raw/master/20240701/125833355-4372024c-f62e-46b0-8617-d4b21a289531-f05af.jpeg)
