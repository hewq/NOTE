# mongoose

- [官网](http://mongoosejs.com/)
- [官方指南](http://mongoosejs.com/docs/guide.html)
- [官方API文档](http://mongoosejs.com/docs/api.html)

## 起步

- 安装：

  ```shell
  npm i mongoose
  ```

- hello world:

  ```javascript
  const mongoose = require('mongoose');
  mongoose.connect('mongodb://localhost/test');
  
  const Cat = mongoose.model('Cat', { name: String });
  
  const kitty = new Cat({ name: 'Zildjian' });
  kitty.save().then(() => console.log('meow'));
  ```

## [Demo](https://github.com/hewq/Front-end/blob/master/apps/JavaScript/nodeJS/_2018/mongoose-demo/demo1.js)