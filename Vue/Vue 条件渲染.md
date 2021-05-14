## Vue 条件渲染

**v-show 和 v-if 的区别：**

- v-show 的显示与否是通过设置 display: none 来完成的；也就是说，不论 show 的结果如何，其 DOM 结构都进行了加载，只是是否显示的不同。

- v-if 的显示与否在于其是否判断为真，当遇到第一次真值（truthy）时才渲染 DOM 元素。

  当 v-if 为假值时，DOM 直接被删除，而不是通过 display: none 隐藏。

因为这个特性， v-if 在 DOM 切换上性能消耗更大。

所以我们要频繁切换 DOM 结构的时候，使用 v-show。反之则使用 v-if。