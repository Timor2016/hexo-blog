---
title: Typora 1.8.10.0 破解方法
date: 2024-04-17 22:28:13
img: http://imgstore.chaochaoke.top/cover.png
summary: 自认为 Typora 是最好用的 Markdown 编辑器，没有之一，本文提供了 Typora 的破解方法之一，亲测可用，如果大家有能力还是建议支持正版。
categories: 破解
tags:
 - typora
 - Markdow
---
  
# 支持正版
[Typora官网](https://typora.ymzhxing.cn/index.html?bd_vid=12344903545967331511)

# Typora 1.8.10.0 破解方法

## 下载 Typora 的1.8.10.0版本

[下载地址](https://www.123pan.com/s/gKaeVv-fq6EH.html)

## 激活Typora

1. 激活 

   找到你安装 `Typora`  的目录，依次找到以下文件

   ``` bash
   resources\page-dist\static\js\LicenseIndex.**********.********.chunk.js 
   ```

   用记事本打开这个文件，查找到 `[e.hasActivated="true"==e.hasActivated,]`  这一段，并替换成 `[e.hasActivated="true"=="true",]` 然后保存，如果提示不能保存可以先把文件复制出来，修改完后在替换原来的文件

2. 关件已激活弹框

   找到你安装 `Typora`  的目录，依次找到以下文件

   ``` bash
   resources\page-dist\license.html
   ```

   同样用记事本打开，在最后可以看到 `[</body></html>]` ，可以替换为

   ``` bash
   </body><script>window.onload=function(){setTimeout(()=>{window.close();},10);}</script></html>
   ```

   注意，这里的 `10` 可以根据 自己的情况适当调整，如果出现以下错误，可以适当将`10` 调大点

   ![1713362074279](http://imgstore.chaochaoke.top/1713362074279.png)

3. 去除未激活小提示

   找到你安装 `Typora`  的目录，依次找到以下文件

   ``` bash
   resources\locales\zh-Hans.lproj\Panel.json 
   ```

   查找 `["UNREGISTERED":"未激活",]` 替换为  `["UNREGISTERED":" ",]`  这里的 `" "`内可填写自己喜欢的文案。不影响实际使用

   到这里就可以正常使用Typora 了

   
   
   
