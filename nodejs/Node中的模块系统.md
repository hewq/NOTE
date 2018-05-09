# Node中的模块系统

## Node编程主要使用工具：

- EcamsScript语言
  - 和浏览器不一样，Node中没有DOM和BOM
- 核心模块
  - 文件操作的fs
  - http服务的 http
  - url路径操作模块
  - path 路径操作模块
  - os操作系统信息
- 第三方模块
  - art-template
  - 必须通过npm来下载才可以使用
- 自己写的模块
  - 自己创建的文件

## 什么是模块化

- 文件作用域
- 通信规则
  - 加载
  - 导出

## CommonJS模块规范

- 模块作用域
- 使用require方法来加载模块
- 使用exports接口对象来导出模块中的成员

### 加载 `require`

语法：

```javascript
var 变量名 = require('模块名')
```

两个作用：

- 执行被加载模块中的代码
- 得到被加载模块中的exports导出接口对象

### 导出 `exports`

- Node中是模块作用域，默认文件中所有成员只在当前文件模块有效

- 对于需要被其他模块访问的成员，需要把这些公开的成员都挂载到` exports ` 接口对象中

  - 导出多个成员

    ```javascript
    exports.a = 123;
    exports.b = 'hello';
    exports.c = function () {
        console.log('ccc');
    }
    exports.d = {
        foo: 'bar'
    }
    ```

    

  - 导出单个成员

    ```javascript
    module.exports = 'hello'
    
    module.exports = function () {
        console.log('a');
    }
    ```

    也可以这样导出成员

    ```javascript
    module.exports = {
        add: function (x, y) {
            return x + y;
        },
        str: 'hello'
    }
    ```

    

