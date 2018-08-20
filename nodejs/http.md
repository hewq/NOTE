### http

1. 加载http核心模块

    `var http = require('http')`

2. 使用http.createServer方法创建一个web服务器，返回一个server实例

   `var server = http.createServer();`

3. 服务器

   * 接收请求

   * 处理请求

   * 发送响应

   * 注册request请求事件

   * 当客户端发请求过来，就会自动触发服务器的request请求事件，然后执行第二个参数回调

     `server.on('request', function(request, response){})`

     * Request请求对象
       * 请求对象可以用来获取请求信息
     * Response请求对象
       * 响应对象可以用来给客户端发送响应消息
       * response对象的write()方法可以用来给客户端发送响应数据
       * write()方法可以使用多次，但是最后一定要用end()方法来结束响应，否则客户端会一直等待

4. 绑定端口号，启动服务器

   ``` javascript
   server.listen(3000, function(){
       console.log('服务器启动成功');
   })
   ```

   [Demo](https://github.com/hewq/Front-end/blob/master/apps/JavaScript/nodeJS/_2018/http/http.js)

   ​