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

    也可以这样导出多个成员

    ```javascript
    module.exports = {
        add: function (x, y) {
            return x + y;
        },
        str: 'hello'
    }
    ```

### 原理解析

`exports`是`module.exports`的一个引用

```javascript
var module = {
    exports: {
        
    }
}
var exports = module.exports

console.log( exports === module.exports )	// true

// 两者等价
exports.foo = 'bar'
module.exports.foo = 'bar'

return module.exports
```

### require加载规则

- 核心模块
  - 模块名	
    - 核心模块的本质也是文件
    - 核心模块文件已经被编译到二进制文件中，只需要按照名字来加载即可
- 第三方模块
  - 模块名
    - 凡是第三方模块都必须通过npm来下载
    - 使用的时候就可以通过require('包名')的方式来进行加载才可以使用
    - 不可能有任何一个第三方的包和核心模块的名字是一样的
    - 既不是核心模块也不是路径形式的模块
    - 加载方式
      - 先找到当前文件所属目录的node_modules目录
      - node_modules/第三方模块名
      - node_modules/第三方模块名/package.json文件
      - node_modules/第三方模块名/package.json文件的main属性
      - main属性中就记录了第三方模块的入口模块
      - 如果package.json文件不存在或者main指定的入口模块不存在，node会自动找该目录下的index.js,也就是说index.js文件会作为一个默认备选项。
      - 如果以上条件都不成立，则会进入上一级目录中的node_modules目录查找，如果上一级还没有，则会继续往上上一级查找。如果直到当前磁盘根目录都没有找到，则最后报错：can not find module xxx
      - 注意⚠️：一个项目有且只有一个node_modules目录，放在项目根目录中。
- 用户自定义
  - 路径

### 模块查找机制

- 优先从缓存加载
- 判断模块标示
  - 核心模块
  - 路径形式的文件模块
  - 第三方模块