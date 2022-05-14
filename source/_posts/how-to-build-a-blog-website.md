---
title: 怎样搭建个人博客网站
date: 2022-05-10 21:16:38
photos: [[https://niuyi-blog.oss-cn-hangzhou.aliyuncs.com/post-imgs/cover.jpg]] 
tags: blog 
---
通过Hexo快速搭建个人博客网站，并通过 github actions 实现自动部署上线。

<!--more--> 

## 一、了解博客
  博客平台：公众号文章、简书、知乎、小红书、新浪博客、QQ空间、...  
  程序员：掘金、博客园、CSDN、 `自建博客` ...  
  可以作为: 笔记、分享...  
  可以获得：知名度、影响力、流量...   
  推荐: [阮一峰的网络日志](https://www.ruanyifeng.com/blog/)、[Hades X Blog](https://blog.mayuko.cn/)...
## 二、了解相关技术栈
  ### 1、Node.js 
   
  一个JavaScript运行环境，可以在操作系统上运行JavaScript代码（在Node.js之前只能在浏览器里运行JavaScript代码）      
  [百度百科](https://baike.baidu.com/item/node.js/7567977?fr=aladdin)、[官网](http://nodejs.cn/)
 
  ### 2、Hexo
  一个基于Node.js的环境的博客框架(底层的脏活累活它来做，我们专注写博客)  
  [官网](https://hexo.io/zh-cn/)

  ### 3、Git
  一个代码管理工具，可以拉取别人的代码，分享自己代码，团队协作写代码等  
  [百度百科](https://baike.baidu.com/item/GIT/12647237?fr=aladdin)、[官网](https://git-scm.com/)
## 三、装环境
### 安装node 、下一步下一步
```
node -v
npm -v
```
### 安装hexo博客框架
```
 npm install -g hexo-cli
```
### 安装git
### 启动hexo
```
  hexo init <folder>
  cd <folder>
  npm install
  npm run server
```
## 四、第一篇博客
## 五、选主题、配置美化博客
## 六、部署到github pages
## 七、引用gitalk评论
## 八、域名、服务器、ssl证书、CDN、对象存储
## 九、 github actions 自动化部署