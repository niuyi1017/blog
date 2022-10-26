---
title: ESLint 基本配置与使用
date: 2022-10-25 09:29:24
photos: 
tags: [前端工作手册, 团队协作及开发规范, 代码风格统一]
---
ESLint是JavaScript代码检查工具。它可以配和VS Code的ESLint插件来提示代并修复码格式错误，也可以用于命令行，比如执行 `eslint . --fix`来检查并修复代码格式。ESLint也可通过插件来配置对其他语言（HTML、CSS等）进行代码检查。

<!--more-->  

### 1、安装与配置
* 初始化一个新项目
创建一个新文件夹，执行下面命令，然后一路回车
```bash
npm init
```
* 安装ESLint包
```bash
npm intall eslint 
```
* 创建index.js, 编写测试代码。代码中使用双引号和分号
```javascript
const msg = "hello world";
```
* 在项目根目录创建`.eslintrc.js`，输入以下配置,来要求代码风格为单引号和不允许分号
```javascript
module.exports = {
  root: true,
  parserOptions: {
    ecmaVersion: 'latest',
  },
  rules: {
    quotes: [2, 'single'],
    semi: [2, 'never'],
  },
}
``` 
  
### 2、使用 ESLint 检查代码风格

虽然上面代码格式和ESLint要求的格式不一致，但是并没有标志告诉开发者。要想知道哪里的代码不符合代码规范，有两种方法：  

* 方法一：VS Code 安装启用ESLint插件
安装完ESLint插件，VS Code 会用波浪线标出不符合代码风格的地方，鼠标移入会显示详细信息。
* 方法二：在命令行执行eslint 命令
在package.json 的 scripts 字段里添加一行脚本
```json
"scripts": {
    ...
    "lint": "eslint . "
  }
```
然后执行
```bash
npm run lint
```
此时，会在控制台打印出不符合代码风格的错误信息  

### 3、使用 ESLint 修正代码风格使其符合规范
虽然上一步知道了代码不符合规范的地方，但是要手动修正太累了。使用ESLint自动修复代码格式，有两种方法：

* 方法一：设置VS Code代码格式化程序为ESLint  
在安装并启用了ESLint插件后，在代码编辑区右键选择`使用...格式化文档`选择ESLint，执行后，代码将会自动格式化为符合规范的代码。  
> 将ESLint设置为VS Code的默认格式化程序，并设置Format On Save ，可实现保存文件自动整理代码格式  

* 方法二：在命令行执行eslint 的fix 命令
修改package.json 的 scripts 字段里的lint脚本
```json
"scripts": {
    ...
    "lint": "eslint . --fix"
  }
```
然后执行
```bash
npm run lint
```
此时，代码也会自动格式化为符合规范的


### 4、更优雅的引入 ESLint 到前端项目 
经过上面的步骤，我们已经体验到了使用ESLint进行代码风格检查和修复代码风格。要想使用ESLint来应对更复杂的场景就需要一种更优雅的方式来引入ESLint
* ESLint 初始化  

```bash
npm eslint --init
``` 


根据提示，可进行个性化定制ESLint的初始功能，比如选择将ESLint只用来检查代码语法还是语法和风格、是否应用于typescript、是否选用流行代码规范还是根据问题自己定义规范。执行完后，会有根据刚才的选择安装对应的eslint插件包和生成对应的配置文件。  


### 5、ESLint 配置文件解析 
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

[1] [前端代码规范工具 eslint vs prettier 哪个更适合你](https://baijiahao.baidu.com/s?id=1718226261291810346&wfr=spider&for=pc)  
[2] [【译】antfu博客：为什么我不用Prettier](https://juejin.cn/post/7149564942633402382#heading-0)  
[3] [eslint的基础使用](https://segmentfault.com/a/1190000011451121)  
[4] [ESLint 的使用和.eslintrc.js配置](http://t.zoukankan.com/Gbeniot-p-10075043.html)  
[5] [ESLint 可组装的JavaScript和JSX检查工具 官网文档](https://eslint.bootcss.com/docs/user-guide/configuring)




