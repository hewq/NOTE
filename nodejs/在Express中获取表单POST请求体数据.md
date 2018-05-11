# 在Express中获取表单post请求体数据

> 在express中没有内置获取表单POST请求体的api，这里我们需要使用一个第三方包： `body-parser`

- 安装

  ```shell
  npm install --save body-parser
  ```

- 配置

  ```javascript
  var express = require('express');
  var bodyParser = require('body-parser');
  
  var app = express();
  
  app.use(bodyParser.urlencoded({ extended: false }));
  
  app.use(bodyParser.json());
  
  app.use(function (req, res) {
      res.setHeader('Content-Type', 'text/plain');
      res.write('you posted:\n');
      res.end(JSON.stringify(req.body, null, 2));
  })
  ```

- 使用

  ```javascript
  app.use(function (req, res) {
      res.setHeader('Content-Type', 'text/plain');
      res.write('you posted:\n');
      // req.body来获取请求体数据
      res.end(JSON.stringify(req.body, null, 2));
  })
  ```

  