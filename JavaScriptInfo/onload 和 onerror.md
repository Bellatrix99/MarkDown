## onload 和 onerror

**注意事项：**

- 大多数资源在被添加到文档中后，便开始加载。但是 `<img>` 是个例外。它要等到获得 src `(*)` 后才开始加载。
- 对于 `<iframe>` 来说，iframe 加载完成时会触发 `iframe.onload` 事件，无论是成功加载还是出现 error。

> 这是出于历史原因

### 跨源策略（CORS）

源（域/端口/协议）无法获取另一个源（origin）的内容

**要允许跨源访问，`<script>` 标签需要具有 `crossorigin` 特性（attribute），并且远程服务器必须提供特殊的 header。**

这里有三个级别的跨源访问：

1. **无 `crossorigin` 特性** —— 禁止访问。
2. **`crossorigin="anonymous"`** —— 如果服务器的响应带有包含 `*` 或我们的源（origin）的 header `Access-Control-Allow-Origin`，则允许访问。浏览器不会将授权信息和 cookie 发送到远程服务器。
3. **`crossorigin="use-credentials"`** —— 如果服务器发送回带有我们的源的 header `Access-Control-Allow-Origin` 和 `Access-Control-Allow-Credentials: true`，则允许访问。浏览器会将授权信息和 cookie 发送到远程服务器。

### 选择 Selection


<p id="p">Select me: <i>italic</i> and <b>bold</b></p>
<script>
  // 从 <p> 的第 0 个子节点选择到最后一个子节点
  document.getSelection().setBaseAndExtent(p, 0, p, p.childNodes.length);
</script>

<p id="p">Select me: <i>italic</i> and <b>bold</b></p>  <script>   // 从 <p> 的第 0 个子节点选择到最后一个子节点   document.getSelection().setBaseAndExtent(p, 0, p, p.childNodes.length); </script>
<p id="p">Select me: <i>italic</i> and <b>bold</b></p>  <script>   let range = new Range();   range.selectNodeContents(p); // 或者也可以使用 selectNode(p) 来选择 <p> 标签    document.getSelection().removeAllRanges(); // 清除现有选择（如果有的话）   document.getSelection().addRange(range); </script>

> **如要选择，请先移除现有的选择**
>
> 如果选择已存在，则首先使用 `removeAllRanges()` 将其清空。然后添加范围。否则，除 Firefox 外的所有浏览器都将忽略新范围。
>
> 某些选择方法例外，它们会替换现有的选择，例如 `setBaseAndExtent`。