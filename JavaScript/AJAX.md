## AJAX

### AJAX 是什么？

- web 开发的一种技术

- 异步发送&请求数据
- 不需要重新刷新页面

### AJAX 的作用？

- 提高用户体验，减少网络数据的传输量

### AJAX 原理？

1. 浏览器让 xhr(XMLHttpRequest) 去服务器要数据
2. 浏览器这时继续干别的事情
3. xhr 去向服务器请求数据
4. 服务器返回数据给 xhr
5. xhr 告诉浏览器数据已经请求到
6. 浏览器接收到 xhr 返回的数据后渲染页面

### 使用 AJAX

1. 创建 ajax 核心对象 xhr --- 注意考虑浏览器兼容性
2. 向服务器发送请求
   - GET --- 请求数据拼接在 URL 中
   - POST
     - **一定要设置请求头的格式内容**
     - 请求数据放在请求体（send）中
3. 服务器响应处理
   - 同步（false）
   - 异步（true）
     - readyState == 4
     - status == 200

## readyState？

- 0：未初始化 —— 尚未调用 .open()方法;
- 1：启动 —— 已经调用 .open() 方法
- 2：发送 —— 已经调用 .send() 方法
- 3：接受 —— 已经接收到部分响应数据
- 4：完成 —— 已经接收到全部响应数据并已可使用在客户端

## status？

- `1XX`（临时响应）
- `2XX`（成功）
- `3XX`（重定向）
- `4XX`（请求错误）
- `5XX`（服务器错误）

### 常用状态码

- `200` 表示从客户端发来的请求在服务端被正常处理了
- `204` 表示请求成功，但没有资源返回
- `301` 表示永久性重定向。该状态码表示请求的资源已被分配了新的 URI，以后应使用资源现在所指的 URI
- `302` 表示临时性重定向
- `304` modified，服务器子资源未改变，可直接使用客户端未过期的缓存
- `400` 表示请求报文中存在语法错误。当错误发生时，需修改请求的内容后再次发送请求
- `401` 表示未授权，当前请求需要用户验证
- `403` 表示对请求资源的访问被服务器拒绝了
- `404` 表示服务器上无法找到请求的资源。除此之外，也可以在服务器端拒绝请求且不想说明理由时使用。
- `500` 表示服务器端在执行请求时发生了错误。
- `503` 表示服务器暂时处于超负荷或正在进行停机维护，现在无法处理请求。

## GET 和 POST 请求数据的区别

1. `GET` 在浏览器回退时是无害的, 而 `POST` 会再次提交请求
2. `GET` 产生的 URL 地址可以被 Bookmark, 而 `POST` 不可以
3. `GET` 请求会被浏览器主动 cache, 而 `POST` 不会, 除非手动设置
4. `GET` 请求只能进行 url 编码, 而 `POST` 支持多种编码方式
5. `GET` 请求参数会被完整保留在浏览器历史记录里, 而 `POST` 中的参数不会被保留
6. `GET` 请求在 URL 中传送的参数是有长度限制的, 而 `POST` 没有
7. `GET` 只接受 ASCII 字符, 而 `POST` 没有限制
8. `GET` 比 `POST` 更不安全, 因为 `GET` 的参数直接暴露在 URL 上
9. `GET` 参数通过 URL 传递, `POST` 放在 Request body 中

### GET 和 POST 使用场景:

若符合以下任一情况, 则推荐使用 `POST` 方法:

- 请求的结果有持续性的副作用, 例如数据库内添加新的数据行
- 若使用 `GET` 方法, 则表单上收集的收据可能让 URL 过长
- 要传送的数据不是采用 7 位的ASCII 编码

若符合以下任一情况, 则推荐用 `GET` 方法:

- 请求时为了查找资源, HTML 表单数据仅用来帮助搜索
- 请求结果无持续性的副作用
- 收集的数据及 HTML 表单内的输入字段名称的总长不超过 1024 个字符