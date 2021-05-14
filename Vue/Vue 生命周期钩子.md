## Vue 生命周期钩子

- beforeCreate: 此时数据 data 和事件 methods 还未绑定到 app 对象上

> => 绑定数据和方法到应用对象上

- create: 数据 data 和方法 methods 已经绑定到应用对象 app 上（但未放置到模板/视图上）

> => 将 template 编译到 render 函数中

- beforeMount: 渲染/挂载之前，根据数据生成的 DOM 对象是获取不到的

> => 渲染 DOM

- mounted: 渲染/挂载之后，可以获取数据生成的 DOM 对象
- beforeUpdate: 数据更改,但内容未更改之前
- updated: 内容已更新完毕
- beforeDestroy: 应用销毁之前
- destroyed: 应用销毁之后

**每当一次如 v-if 操作时，都会有重新渲染和删除的过程**

**v-show 时，就到更新操作就结束了**