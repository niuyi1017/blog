---
title: 代码规范经典方案： ESLint 与 Prettier 配合使用
date: 2022-10-25 09:29:24
photos: 
tags: 前端工作手册
---
在前端工程愈演愈大的情况下，JavaScript 占的比例也很足，需要良好的书写风格，才能在多人协作 code 时提高效率，何况代码还是需要人来读的，所以可读性、可维护性高的代码很多时候有重要意义。即使我们看了大家常说到的 Airbnb 的 JavaScript 的编程风格，但是，不少情况下还是会写出不符合要求的代码，那么就需要工具来约束我们。我们通过配置一些风格，让 IDE 来提醒我们代码的风格是否符合规范，并自动修正代码格式。  

<!--more-->  
## 一、项目初始化
* 新建一个文件夹，在终端执行
```bash
npm init
```
然后一路回车

## 二、引入并配置 ESLint、 Prettier
* 初始化 ESLint ，根据提示选择基础的配置（不用框架和 Typescript ）和选用 airbnb 的代码规范
```bash
npm init @eslint/config
```

* 安装 Prettier 包
```bash
npm install prettier -D
```
* 安装 VS Code ESLint 插件并启用  
* 安装 VS Code Prettier 插件并启用  

## 三、体验一把 ESLint 与 Prettier 的配合
* 创建 index.js, 编写测试代码。   
airbnb 的规范是字符串一律用`单引号`, 但在测试代码中我们使用`双引号`
```javascript
const msg = "hello world";
```
* 在项目根目录创建`.prettierrc.json`，输入以下配置,来要求代码风格为符合 airbnb 规范的的`单引号`

* 在代码编辑区空白处右键选择`使用...格式化文档`选择 `Prettier` ，执行后，代码中的字符串将会自动格式化为`单引号`   

执行完上述步骤，就简单体验了一把 ESLint 与 Prettier 的配合使用。  
在上述示例中，ESLint 用来检查代码是否符合 airbnb 的代码规范，并在代码编辑区用波浪线标注。Prettier 来将代码格式化为符合 airbnb 规范的代码

但这里还有两个问题：  

>（1）需要手动修改 Prettier 的配置文件，来保证 Prettier 的代码格式化规则符合 ESLint 的代码检查规范，否则会`造成冲突`;  
>（2）Prettier 只能修复如`引号、分号`之类的格式错误 ，而ESLint用波浪线标注的还有如`声明的变量未被使用`的语法错误，Prettier无法修复.

后面会深入拆解并解决提出解决方案
## 四、 解决 ESLint 与 Prettier 的规则冲突  

如果 Prettier 的代码格式化规则与 ESLint 的代码检查规范不一致，就会造成冲突。  
比如上述示例中，我们把`.prettierrc.json`文件，让Prettier 在格式化代码时使用双引号：
```json
{
  "singleQuote": false
}
```  
那 Prettier 格式化后的双引号就会和 ESLint 的规范要求的单引号起冲突。

### 方法一：手动修改 Prettier 或 ESLint 配置文件的规则来解决冲突  

适用于冲突项不多的情况，可以像前文示例中一样修改 Prettier 的配置文件，使其格式化的规则符合 ESLint 规范要求的规则。  
也可以修改 ESLint 的配置文件，来使 ESLint 校验规则按照Prettier的规则来。（不建议修改 ESLint 的规则，因为 ESLint 的规则是通用的规范）。   
Prettier 和 ESLint 具体配置文件修改参考[]()
### 方法二：使用 Prettier 官方插件来解决冲突 
Prettier 提供了三个和ESLint相关的官方插件

- [prettier-eslint](https://github.com/prettier/prettier-eslint)  
 Formats your JavaScript using prettier followed by eslint --fix
- [eslint-plugin-prettier](https://github.com/prettier/prettier-eslint)  
 Runs Prettier as an ESLint rule and reports differences as individual ESLint issues.
- [eslint-config-prettier](https://github.com/prettier/prettier-eslint)  
 Turns off all rules that are unnecessary or might conflict with Prettier.


## 五、拆解 Vue 官方项目的代码格式化规范相关配置
## 六、为什么既要 ESlint 又要 Prettier

相比于Prettier，ESlint不仅仅可以格式化代码，更主要的是它可以帮助开发者发现代码中的错误。当一个变量声明之后但是没有使用，它会给出警告。当一个数字类型变量赋值了字符串时，它会给出错误提示。

ESlint会在格式化代码的时候，去修复代码中的错误，而Prettier更多地是去格式化代码而忽略代码中的错误。

Prettier可以定制很多代码格式化的选项，你可以控制代码的宽度，可以控制代码中空格的长度，你可以控制是否使用分号结尾，当然了，这些在ESlint中也可以定制，这么看来，似乎ESlint应该是最佳选择。

但是术业有专攻，Prettier就是专门为了格式化代码而生的。对于代码中的一些问题，ESlint可能无法正确格式化，这个时候，Prettier就可以很好地完成格式化的任务。

一个擅长格式化代码，一个擅长发现代码的错误，那么它们俩可以结合使用吗？答案是肯定的。

在Prettier的官网中，官方已经给出了集成ESLint的解决方案，你可以参照文档将两者合二为一。

如果你的代码还没有使用它们，那么我强烈建议你去尝试使用它们，在团队化的项目中，你会发现使用了它们会让你整个团队的代码看起来整齐划一。












### Prettier 的官方工具






### References  

[1] [前端代码规范工具 eslint vs prettier 哪个更适合你](https://baijiahao.baidu.com/s?id=1718226261291810346&wfr=spider&for=pc)  
[2] [【译】antfu博客：为什么我不用Prettier](https://juejin.cn/post/7149564942633402382#heading-0)  
[3] [eslint的基础使用](https://segmentfault.com/a/1190000011451121)  
[4] [ESLint 的使用和.eslintrc.js配置](http://t.zoukankan.com/Gbeniot-p-10075043.html)  
[5] [ESLint 可组装的JavaScript和JSX检查工具 官网文档](https://eslint.bootcss.com/docs/user-guide/configuring)




