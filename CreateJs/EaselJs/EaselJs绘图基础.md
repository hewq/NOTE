## EaselJs 绘图流程

> 大致流程： 创建显示对象 >> 设置参数 >> 调用绘制方法 >> 添加到舞台 >> 刷新舞台

#### 1. 创建舞台

var stage = new createjs.Stage(canvas);

#### 2. 创建Shape对象，也可以创建文字Text或者图片bitmap

Var rect = new creates.Shape();

#### 3. 设置参数

rect.graphics.beginFill('#000').drawRect( 0, 0, 100, 100 );

#### 4. 添加到舞台

stage.addChild( rect );

#### 5. 刷新舞台

stage.update();

[demo](https://github.com/hewq/Front-end/blob/master/JavaScript/CreateJs/EaselJs/EaselJs%E7%BB%98%E5%9B%BE%E5%9F%BA%E7%A1%80/assets/index.html)

