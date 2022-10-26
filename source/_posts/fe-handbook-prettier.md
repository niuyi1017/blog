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

虽然上面代码格式和 Prettier 要求的格式不一致，但是并没有标志告诉开发者。要想知道哪里的代码不符合代码规范并自动修正代码格式，有两种方法：  

* 方法一：VS Code  Prettier 插件
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




### 5、 ESLint 配置文件解析 
根目录下的`.eslintrc.js`文件是 ESLint 配置的文件，无论是在命令行中执行ESLint命令还是VS Code的ESlint 插件，都是根据这个配置文件来进行代码格式化校验与修复
* 通过 npm eslint --init 生成的配置文件解析
```javascript
module.exports = {
  // env 定义环境，每个环境都定义了一组预定义的全局变量
  env: {     
    browser: true, // 可以使用浏览器环境中的全局变量
    es2021: true, // 可以使用es2021环境中的全局变量
  },
  // 配置文件可以被基础配置中的已启用的规则继承
  extends: [ // 字符串数组：每个配置继承它前面的配置。当前配置文件继承自plugin:vue/vue3-essential和airbnb-base
    'plugin:vue/vue3-essential',  
    'airbnb-base',
  ],
  overrides: [
  ],
  // 指定你想要支持的 JavaScript 语言选项
  parserOptions: {
    ecmaVersion: 'latest', // 使用最新的 ECMAScript 进行语法解析
    sourceType: 'module',   // 默认为script ，可设置为module标明代码是 ECMAScript 模块
  },
  // ESLint 支持使用第三方插件。在使用插件之前，你必须使用 npm 安装它。
  // 在配置文件里配置插件时，可以使用 plugins 关键字来存放插件名字的列表。插件名称可以省略 eslint-plugin- 前缀。
  plugins: [
    'vue',  // 使用了eslint-plugin-vue 插件
  ],
  // 具体校验的规则（后面讲解）
  rules: {},
};
```

* 通过 Vue3 官方初始化命令 npm init vue@latest 生成的配置文件解析
```javascript
/* eslint-env node */
require('@rushstack/eslint-patch/modern-module-resolution');

module.exports = {
  // ESLint 一旦发现配置文件中有 "root": true，它就会停止在父级目录中寻找。
  root: true, 
  // 继承下面的规则
  extends: [
    'plugin:vue/vue3-essential',
    'eslint:recommended',
    '@vue/eslint-config-typescript',
    '@vue/eslint-config-prettier',
  ],
  // 使用使用最新版的 ECMAScript 进行语法解析
  parserOptions: {
    ecmaVersion: 'latest',  
  },
  // 具体校验的规则（后面讲解）
  rules: {},
};

```

### 6、eslint 配置具体规则
ESLint 附带有[大量的规则](https://eslint.bootcss.com/docs/rules/)。可以使用注释或配置文件修改你项目中要使用的规则。要改变一个规则设置，必须将规则 ID 设置为下列值之一：

> "off" 或 0 - 关闭规则  
>"warn" 或 1 - 开启规则，使用警告级别的错误：warn (不会导致程序退出)  
>"error" 或 2 - 开启规则，使用错误级别的错误：error (当被触发的时候，程序会退出)  

使用 rules 连同错误级别和任何想使用的选项，在配置文件中进行规则配置。例如：
```javascript
{
    "rules": {
        "eqeqeq": "off", // 关闭 === 校验
        "quotes": ["error", "double"] // 引号使用
    }
}
```
配置定义在插件中的一个规则的时候，必须使用 插件名/规则ID 的形式。比如：
```javascript
{
    "plugins": [
        "plugin1"
    ],
    "rules": {
        "eqeqeq": "off",
        "curly": "error",
        "quotes": ["error", "double"],
        "plugin1/rule1": "error"
    }
}
```




### References  

[1] [Prettier 官方文档](https://prettier.io/)  
[2] [掘金 Prettier](https://juejin.cn/post/6844903502901166087)  





