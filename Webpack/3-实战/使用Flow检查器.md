## 认识 Flow

```js
// @flow

// 静态类型检查
function square1(n: number): number {
  return n * n;
}
square1('2'); // Error: square1 需要传入 number 作为参数

// 类型推断检查
function square2(n) {
  return n * n; // Error: 传入的 string 类型不能做乘法运算
}
square2('2');
```

> 需要注意的时代码中的第一行 `// @flow` 告诉 Flow 检查器这个文件需要被检查。

## 使用 Flow

```bash
npm i -D flow-bin
```

安装，安装完成后通过先配置 Npm Script

```json
"scripts": {
   "flow": "flow"
}
```

通过 `npm run flow` 去调用 Flow 执行代码检查。

也可以：

```bash
npm i -g flow-bin
```

把 Flow 安装到全局后，再直接通过 `flow` 命令去执行代码检查。



采用了 Flow 静态类型语法的 JavaScript 是无法直接在目前已有的 JavaScript 引擎中运行的，要让代码可以运行需要把这些静态类型语法去掉。 例如：

```js
// 采用 Flow 的源代码
function foo(one: any, two: number, three?): string {}

// 去掉静态类型语法后输出代码
function foo(one, two, three) {}
```

有两种方式可以做到这点：

1. [flow-remove-types](https://github.com/flowtype/flow-remove-types) 可单独使用，速度快。
2. [babel-preset-flow](https://babeljs.io/docs/plugins/preset-flow/) 与 Babel 集成。

## 集成 Webpack

1. 安装 `npm i -D babel-preset-flow` 依赖到项目。

2. 修改 .babelrc 配置文件，加入 Flow Preset：

   ```js
   "presets": [
   ...[],
   "flow"
   ]
   ```

往源码里加入静态类型后重新构建项目，你会发现采用了 Flow 的源码还是能正常在浏览器中运行。