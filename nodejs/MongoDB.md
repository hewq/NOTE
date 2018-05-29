# MongoDB

## MongoDB数据库的基本概念

- 可以有多个数据库

- 一个数据库中可以有多个集合（表）
- 一个集合中可以有多个文档（表记录）
- 文档结构很灵活，没有任何限制
- MongoDB不需要像MySQL一样先创建数据库、表、设计表结构，当你需要插入数据的时候，只需要指定往哪个数据库的哪个集合操作就可以了，一切都由MongoDB自动完成。

```javascript
{
    qq: {
        users: [
            {},
            {},
            {}
        ],
        products: [
                
        ]
    },
    taobao: {

    }
}
```



## 关系型数据库和非关系型数据库

> 表，就是关系，
>
> 或者说表与表之间存在关系

- 所有的关系型数据库都需要通过`sql`语言操作。
- 所有的关系型数据库在操作之前都需要设计表结构
- 而且数据表还支持约束
  - 唯一的
  - 主键
  - 默认值
  - 非空
- 非关系型数据库非常灵活
- 有的非关系型数据库就是key-value对
- MongoDB是最像关系型数据库的非关系型数据库
  - sql		MongoDB
  - 数据库      数据库
  - 数据表      集合（数组）
  - 表记录      文档对象
- MongoDB不需要设计表结构，也就是说可以往里面任意存数据，没有结构性一说。

## 启动和关闭数据库

- 启动：

  ```shell
  # mongodb默认使用执行mongodb命令所处盘符根目录下的/data/db作为自己的数据存储目录
  # 所以在第一次执行该命令之前先自己手动创建一个 /data/db
  mongod
  ```

  + 如果想要修改默认的数据存储目录，可以

    ```shell
    mongod --dbpath=数据存储目录路径
    ```

- 停止

  ```shell
  # 直接crtl+c或者关闭控制台
  ```

## 连接和退出数据库

- 连接

  ```shell
  # 该命令默认连接本机的MongoDB数据库
  mongo
  ```

- 退出

  ```shell
  # 在连接状态输入 exit 退出连接
  exit
  ```

## 基本命令

- `show dbs`
  - 查看显示所有数据库
- `db`
  - 查看当前操作的数据库
- `use dbname`
  - 切换到指定的数据库（如果没有会新建）

## 在node中如何操作MongoDB数据库

- 使用官方的`mongodb`包来操作

  > [node-mongodb-native](https://github.com/mongodb/node-mongodb-native)

- 使用第三方`mongoose`来操作MongoDB数据库

  - [mongoose]()

  