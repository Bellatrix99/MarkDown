## 认识 TypeScript

TypeScript 官方提供了能把 TypeScript 转换成 JavaScript 的编译器。 你需要在当前项目根目录下新建一个用于配置编译选项的 `tsconfig.json` 文件

```json
{
  "compilerOptions": {
    "module": "commonjs", // 编译出的代码采用的模块规范
    "target": "es5", // 编译出的代码采用 ES 的哪个版本
    "sourceMap": true // 输出 Source Map 方便调试
  },
  "exclude": [ // 不编译这些目录里的文件
    "node_modules"
  ]
}
```

通过 `npm install -g typescript` 安装编译器到全局后，你可以通过 `tsc hello.ts` 命令编译出 `hello.js` 和 `hello.js.map` 文件

## 减少代码冗余

为了不让同样的辅助函数重复的出现在多个文件中，可以开启 TypeScript 编译器的 `importHelpers` 选项，修改 `tsconfig.json` 文件如下：

```json
{
  "compilerOptions": {
    "importHelpers": true
  }
}
```

## 集成 Webpack

1. 通过 Loader 把 TypeScript 转换成 JavaScript。
2. Webpack 在寻找模块对应的文件时需要尝试 `ts` 后缀。

> 推荐速度更快的 `awesome-typescript-loader`

相关 Webpack 配置如下：

```js
const path = require('path');

module.exports = {
  // 执行入口文件
  entry: './main',
  output: {
    filename: 'bundle.js',
    path: path.resolve(__dirname, './dist'),
  },
  resolve: {
    // 先尝试 ts 后缀的 TypeScript 源码文件
    extensions: ['.ts', '.js']
  },
  module: {
    rules: [
      {
        test: /\.ts$/,
        loader: 'awesome-typescript-loader'
      }
    ]
  },
  devtool: 'source-map',// 输出 Source Map 方便在浏览器里调试 TypeScript 代码
};
```

在运行构建前需要安装上面用到的依赖：

```bash
npm i -D typescript awesome-typescript-loader
```

安装成功后重新执行构建，你将会在 `dist` 目录看到输出的 JavaScript 文件 `bundle.js`，和对应的 Source Map 文件 `bundle.js.map`。 在浏览器里打开 `index.html` 页面后，来开发工具里可以看到和调试用 TypeScript 编写的源码。

