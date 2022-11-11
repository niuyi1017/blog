---
title: 代码规范经典方案：Prettier for formatting , ESLint for catching bugs
date: 2022-10-25 09:29:24
photos:
tags: 前端工作手册
---

在前端工程愈演愈大的情况下，JavaScript 占的比例也很足，需要良好的书写风格，才能在多人协作 code 时提高效率，何况代码还是需要人来读的，所以可读性、可维护性高的代码很多时候有重要意义。即使我们看了大家常说到的 Airbnb 的 JavaScript 的编程风格，但是，不少情况下还是会写出不符合要求的代码，那么就需要工具来约束我们。我们通过配置一些风格，让 IDE 来提醒我们代码的风格是否符合规范，并自动修正代码格式。

<!--more-->

## 前言：为什么既要 ESlint 又要 Prettier

相比于 Prettier，ESlint 不仅仅可以格式化代码，更主要的是它可以帮助开发者发现代码中的错误。当一个变量声明之后但是没有使用，它会给出警告。当一个数字类型变量赋值了字符串时，它会给出错误提示。

ESlint 会在格式化代码的时候，去修复代码中的错误，而 Prettier 更多地是去格式化代码而忽略代码中的错误。

Prettier 可以定制很多代码格式化的选项，你可以控制代码的宽度，可以控制代码中空格的长度，你可以控制是否使用分号结尾，当然了，这些在 ESlint 中也可以定制，这么看来，似乎 ESlint 应该是最佳选择。

但是术业有专攻，Prettier 就是专门为了格式化代码而生的。对于代码中的一些问题，ESlint 可能无法正确格式化，这个时候，Prettier 就可以很好地完成格式化的任务。

一个擅长`格式化代码`，一个擅长`发现代码的错误`，那么它们俩可以结合使用吗？答案是肯定的。

在 Prettier 的官网中，官方已经给出了集成 ESLint 的解决方案，你可以参照本文将两者合二为一。

如果你的代码还没有使用它们，那么我强烈建议你去尝试使用它们，在团队化的项目中，你会发现使用了它们会让你整个团队的代码看起来整齐划一。

## 一、项目初始化

- 新建一个文件夹，在终端执行

```bash
npm init
```

然后一路回车

## 二、引入并配置 ESLint、 Prettier

- 初始化 ESLint ，根据提示选择基础的配置（不用框架和 Typescript ）和选用 airbnb 的代码规范

```bash
npm init @eslint/config
```

- 安装 Prettier 包

```bash
npm install prettier -D
```

- 安装 VS Code ESLint 插件并启用
- 安装 VS Code Prettier 插件并启用

## 三、体验一把 ESLint 与 Prettier 的配合

- 创建 index.js, 编写测试代码。  
  airbnb 的规范是字符串一律用`单引号`, 但在测试代码中我们使用`双引号`

```javascript
const msg = "hello world"
```

- 在项目根目录创建 `.prettierrc.json`，输入以下配置,来要求代码风格为符合 airbnb 规范的的`单引号`

- 在代码编辑区空白处右键选择`使用...格式化文档`选择 `Prettier` ，执行后，代码中的字符串将会自动格式化为`单引号`

执行完上述步骤，就简单体验了一把 ESLint 与 Prettier 的配合使用。  
在上述示例中，ESLint 用来检查代码是否符合 airbnb 的代码规范，并在代码编辑区用波浪线标注。Prettier 来将代码格式化为符合 airbnb 规范的代码

但这里还有两个问题：

> （1）需要手动修改 Prettier 的配置文件，来保证 Prettier 的代码格式化规则符合 ESLint 的代码检查规范，否则会`造成冲突`;  
> （2）Prettier 只能修复如`引号、分号`之类的格式错误 ，而 ESLint 用波浪线标注的还有如`声明的变量未被使用`的语法错误，Prettier 无法修复.

后面会深入拆解并解决提出解决方案

## 四、 解决 ESLint 与 Prettier 的规则冲突

如果 Prettier 的代码格式化规则与 ESLint 的代码检查规范不一致，就会造成冲突。  
比如上述示例中，我们修改一下`.prettierrc.json`文件，让 Prettier 在格式化代码时使用双引号：

```json
{
  "singleQuote": false
}
```

那 Prettier 格式化后的双引号就会和 ESLint 的规范要求的单引号起冲突。

### 方法一：手动修改 Prettier 或 ESLint 配置文件的规则来解决冲突

适用于冲突项不多的情况，可以像前文示例中一样修改 Prettier 的配置文件，使其格式化的规则符合 ESLint 规范要求的规则。  
也可以修改 ESLint 的配置文件，来使 ESLint 校验规则按照 Prettier 的规则来。（不建议修改 ESLint 的规则，因为 ESLint 的规则是通用的规范）。  
Prettier 和 ESLint 具体配置文件修改参考[]()

### 方法二：使用 Prettier 官方插件来解决冲突

ESLint 和 Prettier 的冲突的在于两者都有格式化代码的能力和规则，解决冲突的原则是 use Prettier for formatting and linters for catching bugs! 也就是说用 Prettier 去调整代码格式，ESLint 来检查语法错误和捕获潜在的代码问题。

Prettier 提供了三个和 ESLint 相关的官方插件

- [eslint-config-prettier](https://github.com/prettier/prettier-eslint) Turns off all rules that are unnecessary or might conflict with Prettier.  
  关闭所有不必要的或可能与 prettier 发生冲突的 ESlint 规则规则。
- [eslint-plugin-prettier](https://github.com/prettier/prettier-eslint) Runs Prettier as an ESLint rule and reports differences as individual ESLint issues.  
  将 prettier 的规则作为 ESLint 的规则，并通过 ESLint 报告问题。
- [prettier-eslint](https://github.com/prettier/prettier-eslint) Formats your JavaScript using prettier followed by eslint --fix  
  使用 prettier 和 eslint --fix 格式化你的 JavaScript 代码。

#### 步骤 1：安装 eslint-config-prettier

```bash
npm install --save-dev eslint-config-prettier
```

使用 eslint-config-prettier 来关掉所有和 Prettier 冲突的 ESLint 的配置（关掉的都是格式问题的配置），方法就是在 .eslintrc 里面将 prettier 设为最后一个 extends

```javascript
// .eslintrc
{
    "extends": ["prettier"] // prettier 一定要是最后一个，才能确保覆盖
}
```

#### 步骤 2： 安装 eslint-plugin-prettier

```bash
npm install --save-dev eslint-plugin-prettier
```

启用 eslint-plugin-prettier ，将 prettier 的 rules 以插件的形式加入到 ESLint 里面。因为 disable ESLint 之后，格式的问题已经全部由 prettier 接手了。但我们期望报错的来源依旧是 ESLint ，所以使用这个插件，相当于把 Prettier 推荐的格式问题的配置以 ESLint rules 的方式写入，这样相当于可以统一代码问题的来源。

```javascript
// .eslintrc
{
    "plugins": ["prettier"],
    "rules": {
        "prettier/prettier": "error"
    }
}
```

#### 步骤 3：

将上面两个步骤合在一起就是下面的配置，也是官方的推荐配置。

```JavaScript
// .eslintrc.js
{
  "extends": ["plugin:prettier/recommended"]
}
```

`plugin:prettier/recommended` 具体做了什么? 它展开如下:

```javascript
{
  "extends": ["prettier"],
  "plugins": ["prettier"],
  "rules": {
    "prettier/prettier": "error",
    "arrow-body-style": "off",
    "prefer-arrow-callback": "off"
  }
}
```

- `"extends": ["prettier"]` 开启来自 eslint-config-prettier 的配置，它将关闭一些与 Prettier 冲突的 ESLint 规则。
- `"plugins": ["prettier"]` 注册这个插件。
- `"prettier/prettier": "error"` 打开这个插件提供的规则，它把 Prettier 做为一个 ESLint 的插件来运行
- `"arrow-body-style": "off"` 和 `"prefer-arrow-callback": "off"` 关闭这两个 ESLint 的核心规则，因为这两个规则和这个插件之间有点问题

然后在代码编辑区空白处右键选择`使用...格式化文档`选择 `ESLint`，默认格式化程序也设置为`ESLint`，因为 Prettier 已经做为 ESLint 的插件来运行了

至此,代码规范经典方案已经配置完毕：Prettier 用来修正代码格式， ESLint 用来检查语法错误。

这样，如果要调整代码规范，只需要修改 `.eslintrc.js` 文件就可以了

```js
// .eslintrc.js
{
  "extends": ["plugin:prettier/recommended"]
   "rules": {
    "prettier/prettier": [    // 配置 Prettier 的规则
      "error",
      {
        singleQuote: false,
      },
    ],
    ...   // 配置其他的 ESLint 规则
  },
}

```

## 五、拆解 Vue 官方项目的代码格式化规范相关配置

### References

[1] [prettier 官方文档](https://prettier.io/docs/en/index.html)  
[2] [eslint-config-prettier](https://github.com/prettier/eslint-config-prettier)  
[3] [eslint-plugin-prettier](https://github.com/prettier/eslint-plugin-prettier)  
[4] [搞懂 ESLint 和 Prettier](https://zhuanlan.zhihu.com/p/80574300)  
[5] [前端代码规范工具 eslint vs prettier 哪个更适合你](https://baijiahao.baidu.com/s?id=1718226261291810346&wfr=spider&for=pc)  
[6] [【译】antfu 博客：为什么我不用 Prettier](https://juejin.cn/post/7149564942633402382#heading-0)  
[7] [eslint 的基础使用](https://segmentfault.com/a/1190000011451121)  
[8] [ESLint 的使用和.eslintrc.js 配置](http://t.zoukankan.com/Gbeniot-p-10075043.html)  
[9] [ESLint 可组装的 JavaScript 和 JSX 检查工具 官网文档](https://eslint.bootcss.com/docs/user-guide/configuring)
