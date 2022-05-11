---
title: 前端常用命令
date: 2022-05-10 16:49:20
tags: 
  - cli
photos: https://www.wangbase.com/blogimg/asset/201904/bg2019042609.jpg
---
收集整理前端常用的命令，涉及git、nginx、node、docker、linux等  

<!--more-->  
## git 篇
1、修改 `.gitignore` 文件后使其生效
```bash
  git rm -r --cached .
  git add .
  git commit -m "update .gitignore"
```
2、查看git用户名信息 (设置用户信息后面跟`用户信息`；查看/更改全局用户信息加 `--global`)
```bash
  git config user.name
  git config user.email
```
## node 篇
1、清除 `node_modules` 缓存
```bash
  # npm version < 7.0.0
  $ npm cache clean -f
```
2、查看`pm2`进程 
```bash
  pm2 ls -a
```
3、查看`pm2`某个进程详情 
```bash
  pm2 show id
```
4、查看`pm2`监控 
```bash
  pm2 monit
```