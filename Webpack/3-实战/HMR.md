## HMR 热模块替换

- 作用：一个模块发生变化，只会重新打包这一个模块；极大提升构建速度

- 样式文件：可以使用 HMR 功能，因为 style-loader 内部实现了

- js 文件：默认不能使用 HMR 功能 --> 需要修改 js 代码，添加支持 HMR 功能的代码
  - 注意: HMR 功能对 js 的处理, 只能处理非入口 js 文件

- html 文件：默认不能使用 HMR 功能，同时会导致问题--html 文件不能热更新了。
  - 解决：修改 entry 入口，将 html 文件引入
  - 但仍然不能使用 HMR 功能
  - html 文件只有一个，不需要 HMR 功能

```JavaScript
if (module.hot) {
    // 一旦 module.hot 为true, 说明开启了 HMR 功能.
    module.hot.accept('./print.js', function() {
        // 方法会监听 print.js 文件的变化,其他模块不会重新打包
        print();
    })
}
```

