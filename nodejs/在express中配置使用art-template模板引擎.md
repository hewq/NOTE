# 在Express中配置使用art-template模板引擎

- 安装

  ```shell
  npm install --save art-template
  npm install --save express-art-template
  ```

- 配置

  ```Javascript
  app.engine('art', require('express-art-template'));
  ```

- 使用

   ```javascript
  app.get('/', function (req, res) {
      // express会默认去项目中的views目录找index.html
      res.render('index.html', {
  		title: 'hello world'
      });
  });
  
  // 如果希望修改默认的views视图渲染目录，则可以
  app.set('views', 目录路径);
   ```

  