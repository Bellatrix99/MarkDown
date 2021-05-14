## 认识 Vue

`App.vue` 文件代表一个单文件组件，它是项目唯一的组件，也是根组件：

```html
<!--渲染模版-->
<template>
  <h1>{{ msg }}</h1>
</template>

<!--样式描述-->
<style scoped>
  h1 {
    color: red;
  }
</style>

<!--组件逻辑-->
<script>
  export default {
    data() {
      return {
        msg: 'Hello,Webpack'
      }
    }
  }
</script>
```

`main.js` 入口文件：

```js
import Vue from 'vue'
import App from './App.vue'

new Vue({
  el: '#app',
  render: h => h(App)
});
```

## 接入 Webpack

修改 Webpack 相关配置如下：

```js
module: {
  rules: [
    {
      test: /\.vue$/,
      use: ['vue-loader'],
    },
  ]
}
```

安装新引入的依赖：

```bash
# Vue 框架运行需要的库
npm i -S vue
# 构建所需的依赖
npm i -D vue-loader css-loader vue-template-compiler
```

在这些依赖中，它们的作用分别是：

- `vue-loader`：解析和转换 `.vue` 文件，提取出其中的逻辑代码 `script`、样式代码 `style`、以及 HTML 模版 `template`，再分别把它们交给对应的 Loader 去处理。
- `css-loader`：加载由 `vue-loader` 提取出的 CSS 代码。
- `vue-template-compiler`：把 `vue-loader` 提取出的 HTML 模版编译成对应的可执行的 JavaScript 代码，这和 React 中的 JSX 语法被编译成 JavaScript 代码类似。预先编译好 HTML 模版相对于在浏览器中再去编译 HTML 模版的好处在于性能更好。

重新启动构建你就能看到由 Vue 渲染出的 `Hello,Webpack` 了。

## 使用 TypeScript 编写 Vue 应用

新增 `tsconfig.json` 配置文件，内容如下：

```json
{
  "compilerOptions": {
    // 构建出 ES5 版本的 JavaScript，与 Vue 的浏览器支持保持一致
    "target": "es5",
    // 开启严格模式，这可以对 `this` 上的数据属性进行更严格的推断
    "strict": true,
    // TypeScript 编译器输出的 JavaScript 采用 es2015 模块化，使 Tree Shaking 生效
    "module": "es2015",
    "moduleResolution": "node"
  }
}
```

以上代码中的 `"module": "es2015"` 是为了 Tree Shaking 优化生效

修改 `App.vue` 脚本部分内容如下：

```html
<!--组件逻辑-->
<script lang="ts">
  import Vue from "vue";

  // 通过 Vue.extend 启用 TypeScript 类型推断
  export default Vue.extend({
    data() {
      return {
        msg: 'Hello,Webpack',
      }
    },
  });
</script>
```

注意 script 标签中的 `lang="ts"` 是为了指明代码的语法是 TypeScript。

修改 `main.ts` 执行入口文件为如下：

```typescript
import Vue from 'vue'
import App from './App.vue'

new Vue({
  el: '#app',
  render: h => h(App)
});
```

由于 TypeScript 不认识 `.vue` 结尾的文件，为了让其支持 `import App from './App.vue'` 导入语句，还需要以下文件 `vue-shims.d.ts` 去定义 `.vue` 的类型：

```typescript
// 告诉 TypeScript 编译器 .vue 文件其实是一个 Vue
declare module "*.vue" {
  import Vue from "vue";
  export default Vue;
}
```

Webpack 配置需要修改两个地方，如下：

```js
const path = require('path');

module.exports = {
  resolve: {
    // 增加对 TypeScript 的 .ts 和 .vue 文件的支持
    extensions: ['.ts', '.js', '.vue', '.json'],
  },
  module: {
    rules: [
      // 加载 .ts 文件
      {
        test: /\.ts$/,
        loader: 'ts-loader',
        exclude: /node_modules/,
        options: {
          // 让 tsc 把 vue 文件当成一个 TypeScript 模块去处理，以解决 moudle not found 的问题，tsc 本身不会处理 .vue 结尾的文件
          appendTsSuffixTo: [/\.vue$/],
        }
      },
    ]
  },
};
```