## 1. 构造函数 [#](https://wangdoc.com/javascript/stdlib/array.html#构造函数)

`Array`是 JavaScript 的原生对象，同时也是一个构造函数，可以用它生成新的数组。

```javascript
var arr = new Array(2);
arr.length // 2
arr // [ empty x 2 ]
```

上面代码中，`Array()`构造函数的参数`2`，表示生成一个两个成员的数组，每个位置都是空值。

如果没有使用`new`关键字，运行结果也是一样的。

```javascript
var arr = new Array(2);
// 等同于
var arr = Array(2);
```

考虑到语义性，以及与其他构造函数用户保持一致，建议总是加上`new`。

`Array()`构造函数有一个很大的缺陷，不同的参数会导致行为不一致。

```javascript
// 无参数时，返回一个空数组
new Array() // []

// 单个正整数参数，表示返回的新数组的长度
new Array(1) // [ empty ]
new Array(2) // [ empty x 2 ]

// 非正整数的数值作为参数，会报错
new Array(3.2) // RangeError: Invalid array length
new Array(-3) // RangeError: Invalid array length

// 单个非数值（比如字符串、布尔值、对象等）作为参数，
// 则该参数是返回的新数组的成员
new Array('abc') // ['abc']
new Array([1]) // [Array[1]]

// 多参数时，所有参数都是返回的新数组的成员
new Array(1, 2) // [1, 2]
new Array('a', 'b', 'c') // ['a', 'b', 'c']
```

可以看到，`Array()`作为构造函数，行为很不一致。因此，不建议使用它生成新数组，直接使用数组字面量是更好的做法。

```javascript
// bad
var arr = new Array(1, 2);

// good
var arr = [1, 2];
```

注意，如果参数是一个正整数，返回数组的成员都是空位。虽然读取的时候返回`undefined`，但实际上该位置没有任何值。虽然这时可以读取到`length`属性，但是取不到键名。

```javascript
var a = new Array(3);
var b = [undefined, undefined, undefined];

a.length // 3
b.length // 3

a[0] // undefined
b[0] // undefined

0 in a // false
0 in b // true
```

上面代码中，`a`是`Array()`生成的一个长度为3的空数组，`b`是一个三个成员都是`undefined`的数组，这两个数组是不一样的。读取键值的时候，`a`和`b`都返回`undefined`，但是`a`的键名（成员的序号）都是空的，`b`的键名是有值的。

## 2. 静态方法

### 2.1 Array.isArray()

`Array.isArray`方法返回一个布尔值，表示参数是否为数组。它可以弥补`typeof`运算符的不足。

```javascript
var arr = [1, 2, 3];

typeof arr // "object"
Array.isArray(arr) // true
```

上面代码中，`typeof`运算符只能显示数组的类型是`Object`，而`Array.isArray`方法可以识别数组。

## 3. 实例方法

### 3.1 valueOf()，toString()

`valueOf`方法是一个所有对象都拥有的方法，表示对该对象求值。不同对象的`valueOf`方法不尽一致，数组的`valueOf`方法返回数组本身。

```javascript
var arr = [1, 2, 3];
arr.valueOf() // [1, 2, 3]
```

`toString`方法也是对象的通用方法，数组的`toString`方法返回数组的字符串形式。

```javascript
var arr = [1, 2, 3];
arr.toString() // "1,2,3"

var arr = [1, 2, 3, [4, 5, 6]];
arr.toString() // "1,2,3,4,5,6"
```

### 3.2 push()，pop()

`push`方法用于在数组的末端添加一个或多个元素，并返回添加新元素后的数组长度。注意，该方法会改变原数组。

```javascript
var arr = [];

arr.push(1) // 1
arr.push('a') // 2
arr.push(true, {}) // 4
arr // [1, 'a', true, {}]
```

上面代码使用`push`方法，往数组中添加了四个成员。

`pop`方法用于删除数组的最后一个元素，并返回该元素。注意，该方法会改变原数组。

```javascript
var arr = ['a', 'b', 'c'];

arr.pop() // 'c'
arr // ['a', 'b']
```

**对空数组使用`pop`方法，不会报错，而是返回`undefined`。**

```javascript
[].pop() // undefined
```

**`push`和`pop`结合使用，就构成了“后进先出”的栈结构（stack）。**

```javascript
var arr = [];
arr.push(1, 2);
arr.push(3);
arr.pop();
arr // [1, 2]
```

上面代码中，`3`是最后进入数组的，但是最早离开数组。

### 3.3 shift()，unshift()

`shift()`方法用于删除数组的第一个元素，并返回该元素。注意，该方法会改变原数组。

```javascript
var a = ['a', 'b', 'c'];

a.shift() // 'a'
a // ['b', 'c']
```

上面代码中，使用`shift()`方法以后，原数组就变了。

`shift()`方法可以遍历并清空一个数组。

```javascript
var list = [1, 2, 3, 4];
var item;

while (item = list.shift()) {
  console.log(item);
}

list // []
```

上面代码通过`list.shift()`方法每次取出一个元素，从而遍历数组。它的前提是数组元素不能是`0`或任何布尔值等于`false`的元素，因此这样的遍历不是很可靠。

**`push()`和`shift()`结合使用，就构成了“先进先出”的队列结构（queue）。**

`unshift()`方法用于在数组的第一个位置添加元素，并返回添加新元素后的数组长度。注意，该方法会改变原数组。

```javascript
var a = ['a', 'b', 'c'];

a.unshift('x'); // 4
a // ['x', 'a', 'b', 'c']
```

`unshift()`方法可以接受多个参数，这些参数都会添加到目标数组头部。

```javascript
var arr = [ 'c', 'd' ];
arr.unshift('a', 'b') // 4
arr // [ 'a', 'b', 'c', 'd' ]
```

### 3.4 join()

`join()`方法以指定参数作为分隔符，将所有数组成员连接为一个字符串返回。如果不提供参数，默认用逗号分隔。

```javascript
var a = [1, 2, 3, 4];

a.join(' ') // '1 2 3 4'
a.join(' | ') // "1 | 2 | 3 | 4"
a.join() // "1,2,3,4"
```

如果数组成员是`undefined`或`null`或空位，会被转成空字符串。

通过`call`方法，这个方法也可以用于字符串或类似数组的对象。

```javascript
Array.prototype.join.call('hello', '-')
// "h-e-l-l-o"

var obj = { 0: 'a', 1: 'b', length: 2 };
Array.prototype.join.call(obj, '-')
// 'a-b'
```

### 3.5 concat()

`concat`方法用于多个数组的合并。它将新数组的成员，添加到原数组成员的后部，然后返回一个新数组，原数组不变。

```javascript
['hello'].concat(['world'])
// ["hello", "world"]

['hello'].concat(['world'], ['!'])
// ["hello", "world", "!"]

[].concat({a: 1}, {b: 2})
// [{ a: 1 }, { b: 2 }]

[2].concat({a: 1})
// [2, {a: 1}]
```

除了数组作为参数，`concat`也接受其他类型的值作为参数，添加到目标数组尾部。

```javascript
[1, 2, 3].concat(4, 5, 6)
// [1, 2, 3, 4, 5, 6]
```

如果数组成员包括对象，`concat`方法返回当前数组的一个浅拷贝。所谓“浅拷贝”，指的是新数组拷贝的是对象的引用。

```javascript
var obj = { a: 1 };
var oldArray = [obj];

var newArray = oldArray.concat();

obj.a = 2;
newArray[0].a // 2
```

上面代码中，原数组包含一个对象，`concat`方法生成的新数组包含这个对象的引用。所以，改变原对象以后，新数组跟着改变。

### 3.6 reverse() 

`reverse`方法用于颠倒排列数组元素，返回改变后的数组。注意，该方法将改变原数组。

```javascript
var a = ['a', 'b', 'c'];

a.reverse() // ["c", "b", "a"]
a // ["c", "b", "a"]
```