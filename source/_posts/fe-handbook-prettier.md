---
title: Prettier 基本配置与使用
date: 2022-10-25 09:29:24
photos: 
tags: [前端工作手册, 团队协作及开发规范, 代码风格统一]
---
Prettier将自己介绍描述为“一个固执己见的代码格式化工具( Prettier is an opinionated code formatter)”。它可以将代码格式化为风格规范的代码，支持很多编程语言，可以在编辑器保存时运行，在提交前的钩子中运行，或者在CI环境中运行，以确保代码库具有一致的风格。

<!--more-->  

### 1、安装与配置
* 初始化一个新项目
创建一个新文件夹，执行下面命令，然后一路回车
```bash
npm init
```
* 安装 Prettier 包
```bash
npm intall prettier 
```
* 创建index.js, 编写测试代码。代码中使用双引号和分号
```javascript
const msg = "hello world";
```
* 在项目根目录创建`.prettierrc.json`，输入以下配置,来要求代码风格为单引号和不允许分号
```json
{
  "singleQuote": true,
  "semi": false
}

```
  
### 2、使用 Prettier 检查代码风格并修正

上面代码格式和 Prettier 要求的格式不一致，要想自动修正代码格式，有两种方法：  

* 方法一：VS Code Prettier 插件
安装完Prettier插件，在代码编辑区右键选择`使用...格式化文档`选择 Prettier ，执行后，代码将会自动格式化为符合规范的代码
* 方法二：命令行执行 Prettier 命令
在package.json 的 scripts 字段里添加一行脚本
```json
"scripts": {
    ...
    "format": "prettier --write . "
  }
```
然后执行
```bash
npm run format
```
执行后，代码将会自动格式化为符合规范的代码


### 3、Prettier 配置文件解析  

Prettier 配置文件比较简单直接写[配置规则]()就行
```json
{
  "trailingComma": "es5",
  "tabWidth": 4,
  "semi": false,
  "singleQuote": true
}
```

### 4、针对特定文件覆盖配置
把官方的例子搬了过来。这样就能针对不同文件进行配置了。
```json
{
  "semi": false,
  "overrides": [
    {
      "files": "*.test.js",
      "options": {
        "semi": true
      }
    },
    {
      "files": ["*.html", "legacy/**/*.js"],
      "options": {
        "tabWidth": 4
      }
    }
  ]
}
```
### 5、忽略不想格式化的文件
创建 .prettierignore忽略你不希望格式化的文件，node_modules是默认会被忽略的目录。
他的用法就类似于.gitignore，下面是官方给的例子
```bash
# Ignore artifacts:
build
coverage
```




### References  

[1] [Prettier 官方文档](https://prettier.io/)  
[2] [掘金 Prettier](https://juejin.cn/post/6844903502901166087)  
[3] [prettier使用指南（包含所有配置项）](http://events.jianshu.io/p/18999f6e1668)





