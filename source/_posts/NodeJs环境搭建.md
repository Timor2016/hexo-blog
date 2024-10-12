---
title: NodeJS 多版本切换
categories: nodejs
tags:
  - nodejs
abbrlink: 8a7ba599
date: 2024-07-01 22:28:13
---

在项目开发中，不同的项目我们可能需要用到不同版本的node做支持，并且需要根据项目需要切换，以下就是常用的node版本切换命令行。

1. 安装 `n`

   ```
   npm install -g n
   ```

2. 查看`n`模块的版本

   ```
   	n --version
   ```

3. 展示当前安装的node 的版本

   ```
   n list
   ```

4. 安装制定node

   ```Dart
   n 14.17.4 
   ```

5. 安装最新node版本

   ```Dart
   n latest
   ```

6. 安装稳定版本

   ```Dart
   n stable
   ```

7. 删除版本

   ```Dart
   n rm 14.17.4 
   ```

8. 查看帮助

   ```Dart
   n help
   ```

9. 切换node 版本

   1. 输入 n 会列出所安装的node 版本
   2. 切换要选择的版本即可

10. 查看当前版本

    node -v