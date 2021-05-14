关于这句 call语句我有几个问题：

1. fn.call(prev, curr, index, arr) 时， call的 this指向哪里？
2. fn.call(this, curr, index, arr) 时， call的 this指向哪里？
3. fn.call(this, curr)且this为''/ null/ 0/ undefined 时，call的 this指向哪里？
4. fn.call(curr) 不指定this时，call的this指向哪里?  
5. 在3和4中，this为什么不一样（为什么不都是windows）？
6. 如果写fn.call(this, prev, curr, index, arr)是什么情况？

