## Babel

在 Babel 执行编译的过程中，会从项目根目录下的 `.babelrc` 文件读取配置。`.babelrc` 是一个 JSON 格式的文件，内容大致如下：

```json
{
  "plugins": [
    [
      "transform-runtime",
      {
        "polyfill": false
      }
    ]
   ],
  "presets": [
    [
      "es2015",
      {
        "modules": false
      }
    ],
    "stage-2",
    "react"
  ]
}
```

### Plugins

使用插件

transform-runtime` 对应的插件全名叫做 `babel-plugin-transform-runtime

即在前面加上了 **`babel-plugin-`**

```bash
npm i -D babel-plugin-transform-runtime
```

**`babel-plugin-transform-runtime` 是 Babel 官方提供的一个插件，作用是减少冗余代码，当转换时需要注入辅助函数时，不把辅助函数内容注入到文件里，而是注入一条导入语句：**

```js
var _extent = require('babel-runtime/helpers/_extent');
```

这样可以大大减少 Babel 编译出来的代码文件大小

### Presets

`presets` 属性告诉 Babel 要转换的源码使用了哪些新的语法特性，一个 Presets 对一组新语法特性提供支持，多个 Presets 可以叠加。

Presets 其实是一组 Plugins 的集合，每一个 Plugin 完成一个新语法的转换工作。

在前面加上了 **`babel-preset-`**

- [es2015](https://babeljs.io/docs/plugins/preset-es2015/) 包含在2015里加入的新特性；
- [es2016](https://babeljs.io/docs/plugins/preset-es2016/) 包含在2016里加入的新特性；
- [es2017](https://babeljs.io/docs/plugins/preset-es2017/) 包含在2017里加入的新特性；
- [env](https://babeljs.io/docs/plugins/preset-env/) 包含当前所有 ECMAScript 标准里的最新特性。

![图3.1.1 ECMAScript 标准里的特性关系图](https://webpack.wuhaolin.cn/3实战/img/3-1presets-es.png)

- [stage0](https://babeljs.io/docs/plugins/preset-stage-0/) 只是一个美好激进的想法，有 Babel 插件实现了对这些特性的支持，但是不确定是否会被定为标准；
- [stage1](https://babeljs.io/docs/plugins/preset-stage-1/) 值得被纳入标准的特性；
- [stage2](https://babeljs.io/docs/plugins/preset-stage-2/) 该特性规范已经被起草，将会被纳入标准里；
- [stage3](https://babeljs.io/docs/plugins/preset-stage-3/) 该特性规范已经定稿，各大浏览器厂商和 Node.js 社区开始着手实现；
- stage4 在接下来的一年将会加入到标准里去。

![图3.1.2 stage 关系图](https://i.loli.net/2021/05/10/eI4Gu8fNlkqtWjs.png)