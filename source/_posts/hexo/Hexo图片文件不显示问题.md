---
title: Hexo图片文件不展示问题处理
date: 2024-07-02 09:31
#img: http://imgstore.chaochaoke.top/cover.png
categories: hexo
tags:
  - hexo
  - 博客
---

在部署Hexo博客时，发现博客内的图片都无法显示，于是我去检查了是否是gitee图床的问题，发现，单独通过地址打开图片是没问题的，然后打开浏览器调试，发现图片加载都是403，就想到了可能是gitee 的防盗链导致的，于是便在主题的head 中加入了

```html
 <meta name="referrer" content="no-referrer" />
```

即可解决问题