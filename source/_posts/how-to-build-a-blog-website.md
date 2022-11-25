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
   
  一个JavaScript运行环境，可以在操作系统上运行JavaScript代码  
  [百度百科](https://baike.baidu.com/item/node.js/7567977?fr=aladdin)、[官网](http://nodejs.cn/)
 
  ### 2、Hexo
  一个基于Node.js的环境的博客框架    
  [官网](https://hexo.io/zh-cn/)

  ### 3、Git
  一个代码管理工具，可以拉取别人的代码，分享自己代码，团队协作写代码等  
  [百度百科](https://baike.baidu.com/item/GIT/12647237?fr=aladdin)、[官网](https://git-scm.com/)
## 三、装环境
### 1、安装node
  [官网下载](http://nodejs.cn/download/)对应系统的node安装包，安装时直接双击运行，然后下一步下一步   
  安装后打开命令行工具，依次执行下面的命令，如果能打印出对应的版本号，就证明安装成功了 
```
node -v
npm -v
```

### 2、安装hexo博客框架  
  在命令行执行:
```
 npm install -g hexo-cli
```

然后执行:  

```
 hexo version
```
 
  如果能打印出对应的版本号，就证明安装成功了


### 3、安装git
[官网下载](https://git-scm.com/)对应安装包，安装时直接双击运行，然后下一步下一步   
  安装后打开命令行工具，执行下面的命令，如果能打印出对应的版本号，就证明安装成功了
```
  git --version
```

### 4、启动hexo
基础环境装好后，就可以启动hexo服务了  
执行下面四行命令，然后在浏览器打开`http://localhost:4000`, 就可以看到hexo默认的博客站了
```bash
  # 用hexo初始化一个文件夹，用来做完hexo项目
  hexo init <folder>  
  # 进入到这个文件夹 
  cd <folder>  
  # 安装依赖       
  npm install   
  # 启动服务      
  npm run server      
```
## 四、第一篇博客
## 五、选主题、配置美化博客
## 六、部署到github pages
## 七、引用gitalk评论
## 八、域名、服务器、ssl证书、CDN、对象存储
## 九、 github actions 自动化部署