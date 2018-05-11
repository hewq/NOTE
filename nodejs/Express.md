# Express

## 安装

```shell
npm install --save express
```

## hello world

```javascript
const express = require('express');
const app = express();

app.get('/', (req, res) => res.send('hello world!'));

app.listen(3000, () => console.log('Example app listening at port 3000!'))
```

## 基本路由

- get

  ```javascript
  // 当以GET方法请求／的时候，执行对应的函数
  app.get('/', function (req, res) {
      res.send('hello world');
  })
  ```

- post

  ```javascript
  // 当以POST方法请求／的时候，执行对应的函数
  app.post('/', function (req, res) {
      res.send('Got a POST request');
  })
  ```

## 静态服务

```javascript
app.use(express.static('public'));
app.use(express.static('files'));

// 当以/public/开头的时候，去./public/目录中找对应的资源
app.use('/public/', express.static('./public/'));

// 可以给／public／起别名
app.user('/static/', express.static('./public/'));

// 当省略第一个参数时，则可以通过省略./public直接访问
app.use(express.static('./public/'));

app.use('/static/', express.static(path.join(__dirname, 'public')));
```

