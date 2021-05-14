parseInt()

parseFloat()

返回一个整数/浮点数，截取字符串前面的整数/浮点数。

```javascript
alert( parseInt('100px') ); // 100 
alert( parseFloat('12.5em') ); // 12.5 
alert( parseInt('12.3') ); // 12，只有整数部分被返回了 
alert( parseFloat('12.3.4') ); // 12.3，在第二个点出停止了读取

alert( parseInt('a123') ); // NaN，第一个符号停止了读取

alert( parseInt('0xff', 16) ); // 255
alert( parseInt('ff', 16) ); // 255，没有 0x 仍然有效

alert( parseInt('2n9c', 36) ); // 123456
```



使用 `str[]` 和 `str.charAt()` 唯一的区别就是他们的返回值；

`[]` 返回 `undefined`，而 `charAt` 返回一个空字符串



isFinite()括号中如果是数字的字符串类型也可以自动转换并成功判断