---
title: 前端常用命令
date: 2022-05-10 16:49:20
tags: 
  - cli
photos: https://niuyi-blog.oss-cn-hangzhou.aliyuncs.com/post-imgs/common-cli.png
---
收集整理前端常用的命令，涉及git、nginx、node、docker、linux等  

<!--more-->  
## 一、 git 篇
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
3、查看git远端地址
```bash
  git remote -v
```
4、更换git远端地址
```bash
  git remote set-url origin https://xxxx.git
```

## 二、 Node 篇
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
5、使用`pm2`启动 xxx 的任务
```bash
  pm2 start src/app.js --name xxx
```

## 三、Linux 篇  
1、查看端口占用
```
netstat -tnlp | grep 80
```
2、查看进程详情
```
 ps -aux | grep nginx
```
3、查看进程详情
```
 ps -aux | grep nginx
```
3、查看服务状态详情
```
 service xxx status
 或
 systemctl status xxx
```

## 四、Nginx 篇  
1、nginx 检查语法是否正确
```
sudo nginx -t
```
2、nginx 重载配置文件以生效
```
sudo nginx -s reload
```