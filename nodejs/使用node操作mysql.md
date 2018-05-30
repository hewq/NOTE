# 使用node操作mysql

- 安装

  ```shell
  npm install mysql
  ```

- 使用

  ```javascript
  var mysql      = require('mysql');
  
  // 1.创建连接
  var connection = mysql.createConnection({
    host     : 'localhost',
    user     : 'root',
    password : '12345678',
    database : 'test'
  });
   
  // 2.连接数据库
  connection.connect();
   
  // 3.执行数据库操作
  connection.query('SELECT * FROM `users`', function (error, results, fields) {
    if (error) throw error;
    console.log('The solution is: ', results[0].solution);
  });
   
  // 关闭连接
  connection.end();
  ```

  ## [Demo](https://github.com/hewq/Front-end/tree/master/apps/JavaScript/nodeJS/_2018/mysql-demo)

