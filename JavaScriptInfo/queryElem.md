# 遍历 **DOM**

# <img src="C:%5CUsers%5C12922%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5Cimage-20210203104029709.png" alt="image-20210203104029709" style="zoom: 80%;" />

## [在最顶层：documentElement 和 body](https://zh.javascript.info/dom-navigation#zai-zui-ding-ceng-documentelement-he-body)

最顶层的树节点可以直接作为 `document` 的属性来使用：

- `<html>` = `document.documentElement`

  最顶层的 document 节点是 `document.documentElement`。这是对应 `<html>` 标签的 DOM 节点。

- `<body>` = `document.body`

  另一个被广泛使用的 DOM 节点是 `<body>` 元素 — `document.body`。

- `<head>` = `document.head`

  `<head>` 标签可以通过 `document.head` 访问。

> **在 DOM 的世界中，`null` 就意味着“不存在”**
>
> 在 DOM 中，`null` 值就意味着“不存在”或者“没有这个节点”。

> **DOM 集合是实时的**
>
> 除小部分例外，几乎所有的 DOM 集合都是 **实时** 的。换句话说，它们反映了 DOM 的当前状态。
>
> 如果我们保留一个对 `elem.childNodes` 的引用，然后向 DOM 中添加/移除节点，那么这些节点的更新会自动出现在集合中。

> **不要使用 `for..in` 来遍历集合**
>
> 可以使用 `for..of` 对集合进行迭代。但有时候人们会尝试使用 `for..in` 来迭代集合。
>
> 请不要这么做。`for..in` 循环遍历的是所有可枚举的（enumerable）属性。集合还有一些“额外的”很少被用到的属性，通常这些属性也是我们不期望得到的

## [纯元素导航](https://zh.javascript.info/dom-navigation#chun-yuan-su-dao-hang)

<img src="C:%5CUsers%5C12922%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5Cimage-20210203104238726.png" alt="image-20210203104238726" style="zoom: 80%;" />

这些链接和我们在上面提到过的类似，只是在词中间加了 `Element`：

- `children` — 仅那些作为元素节点的子代的节点。
- `firstElementChild`，`lastElementChild` — 第一个和最后一个子元素。
- `previousElementSibling`，`nextElementSibling` — 兄弟元素。
- `parentElement` — 父元素。

## [更多链接：表格](https://zh.javascript.info/dom-navigation#dom-navigation-tables)

<table> 元素支持 (除了上面给出的，之外) 以下这些属性:
table.rows — <tr> 元素的集合。table.caption/tHead/tFoot — 引用元素 <caption>，<thead>，<tfoot>。table.tBodies — <tbody> 元素的集合（根据标准还有很多元素，但是这里至少会有一个 — 即使没有被写在 HTML 源文件中，浏览器也会将其放入 DOM 中）。
<thead>，<tfoot>，<tbody> 元素提供了 rows 属性：
tbody.rows — 表格内部 <tr> 元素的集合。

<tr>：
tr.cells — 在给定 <tr> 中的 <td> 和 <th> 单元格的集合。tr.sectionRowIndex — 给定的 <tr> 在封闭的 <thead>/<tbody>/<tfoot> 中的位置（索引）。tr.rowIndex — 在整个表格中 <tr> 的编号（包括表格的所有行）。

<td> 和 <th>：
td.cellIndex — 在封闭的 <tr> 中单元格的编号。

> **`id` 必须是唯一的**
>
> `id` 必须是唯一的。在文档中，只能有一个元素带有给定的 `id`。
>
> 如果有多个元素都带有同一个 `id`，那么使用它的方法的行为是不可预测的，例如 `document.getElementById` 可能会随机返回其中一个元素。因此，请遵守规则，保持 `id` 的唯一性。

> **只有 `document.getElementById`，没有 `anyElem.getElementById`**
>
> `getElementById` 方法只能被在 `document` 对象上调用。它会在整个文档中查找给定的 `id`。

> **不要忘记字母 `"s"`！**
>
> 新手开发者有时会忘记字符 `"s"`。也就是说，他们会调用 `getElementByTagName` 而不是 `getElement**s**ByTagName`。
>
> `getElementById` 中没有字母 `"s"`，是因为它只返回单个元素。但是 `getElementsByTagName` 返回的是元素的集合，所以里面有 `"s"`。

## [总结](https://zh.javascript.info/dom-navigation#zong-jie)

给定一个 DOM 节点，我们可以使用导航（navigation）属性访问其直接的邻居。

这些属性主要分为两组：

- 对于所有节点：`parentNode`，`childNodes`，`firstChild`，`lastChild`，`previousSibling`，`nextSibling`。
- 仅对于元素节点：`parentElement`，`children`，`firstElementChild`，`lastElementChild`，`previousElementSibling`，`nextElementSibling`。

某些类型的 DOM 元素，例如 table，提供了用于访问其内容的其他属性和集合。



有 6 种主要的方法，可以在 DOM 中搜素节点：

| Method                   | Searches by... | Can call on an element? | Live? |
| ------------------------ | -------------- | ----------------------- | ----- |
| `querySelector`          | CSS-selector   | ✔                       | -     |
| `querySelectorAll`       | CSS-selector   | ✔                       | -     |
| `getElementById`         | `id`           | -                       | -     |
| `getElementsByName`      | `name`         | -                       | ✔     |
| `getElementsByTagName`   | tag or `'*'`   | ✔                       | ✔     |
| `getElementsByClassName` | class          | ✔                       | ✔     |

目前为止，最常用的是 `querySelector` 和 `querySelectorAll`，但是 `getElement(s)By*` 可能会偶尔有用，或者可以在旧脚本中找到。

此外：

- `elem.matches(css)` 用于检查 `elem` 与给定的 CSS 选择器是否匹配。
- `elem.closest(css)` 用于查找与给定 CSS 选择器相匹配的最近的祖先。`elem` 本身也会被检查。

让我们在这里提一下另一种用来检查子级与父级之间关系的方法，因为它有时很有用：

- 如果 `elemB` 在 `elemA` 内（`elemA` 的后代）或者 `elemA==elemB`，`elemA.contains(elemB)` 将返回 true。