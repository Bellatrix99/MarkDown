## 认识 SCSS

SCSS是一种 CSS 预处理器，语法和 CSS 相似，但加入了变量、逻辑、等编程元素

```scss
$blue: #1875e7;　
div {
  color: $blue;
}
```

> SCSS 又叫 SASS，区别在于 SASS 语法类似 Ruby，而 SCSS 语法类似 CSS，对于熟悉 CSS 的前端工程师来说会更喜欢 SCSS

```bash
npm i -g node-sass
```

再执行编译命令：

```bash
# 把 main.scss 源文件编译成 main.css
node-sass main.scss main.css
```

你就能在源码同目录下看到编译后的 `main.css` 文件。

## 接入 Webpack

```js
module.exports = {
  module: {
    rules: [
      {
        // 增加对 SCSS 文件的支持
        test: /\.scss$/,
        // SCSS 文件的处理顺序为先 sass-loader 再 css-loader 再 style-loader
        use: ['style-loader', 'css-loader', 'sass-loader'],
      },
    ]
  },
};
```

1. 通过 sass-loader 把 SCSS 源码转换为 CSS 代码，再把 CSS 代码交给 css-loader 去处理。
2. css-loader 会找出 CSS 代码中的 `@import` 和 `url()` 这样的导入语句，告诉 Webpack 依赖这些资源。同时还支持 CSS Modules、压缩 CSS 等功能。处理完后再把结果交给 style-loader 去处理。
3. style-loader 会把 CSS 代码转换成字符串后，注入到 JavaScript 代码中去，通过 JavaScript 去给 DOM 增加样式。如果你想把 CSS 代码提取到一个单独的文件而不是和 JavaScript 混在一起，可以使用[1-5 使用Plugin](https://webpack.wuhaolin.cn/1入门/1-5使用Plugin.html) 中介绍过的 ExtractTextPlugin。

由于接入 sass-loader，项目需要安装这些新的依赖：

```bash
# 安装 Webpack Loader 依赖
npm i -D  sass-loader css-loader style-loader
# sass-loader 依赖 node-sass
npm i -D node-sass
```