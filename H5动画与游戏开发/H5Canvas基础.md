# H5 Canvas 基础

##  Canvas 简单案例

- 获得 Canvas 元素节点

  ```JavaScript
  var theCanvas = document.getElementById('canvas');
  theCanvas.width = 300;
  theCanvas.height = 150
  ```

- 获得和设置 Canvas 的图形上下文

  ```javascript
  var context = theCanvas.getContext('2d'); // 返回 CanvasRenderingContext2D 对象
  context.fillStyle = "#ff0000";
  ```

- 通过 Canvas API 绘制图形图像

  ```javascript
  context.fillRect(0, 0, 100, 100); // context.strokeRect(0, 0, 100, 100); 注意顺序的影响
  context.clearRect(25, 25, 50, 50);
  ```

## Canvas 的尺寸大小（元素大小、绘画表面大小）

- Canvas `元素样式`的大小（若不设置，则大小同绘图表面大小）

  ```html
  <style>
      #CanvasOne {	/*通过 css 样式设置 Canvas 元素大小*/
  		width: 200px;
          height: 200px;
      }
  </style>
  <canvas id="CanvasOne"></canvas>
  ```

- Canvas 绘图表面的大小（默认宽度为300，高为150）

  ```html
  <canvas id="CanvasOne"></canvas>
  <canvas id="CanvasTwo" width="200" height="100"></canvas>
  ```

- Canvas 元素大小和绘制表面大小不一致时，会产生`拉伸现象`。

[demo](https://github.com/hewq/course-H5-Animation-and-Game-Development/blob/master/ch02/LS02/LS02_01.html)

## Canvas 图形上下文（context）

- Canvas 区别与 Flash、SVG，Canvas 不是对绘制对象进行操作，而是`基于状态`的绘制。
- Canvas 状态存储在图形上下文 context 中
  - 上下文属性（描边样式、填充样式、全局透明度、线宽、线连接方式等）
  - 变换矩阵信息（平移、旋转、缩放）
  - 剪贴区域：通过clip()方法创建的
- context 原型链及继承关系
  - context 的构造器（constructor）为 CanvasRenderingContext2D
  - context 对象的原型为 CanvasRenderingContext2D.prototype

[demo](https://github.com/hewq/course-H5-Animation-and-Game-Development/blob/master/ch02/LS02/LS02_02.html)

## Canvas 图形上下文的状态存储

- context 保存与恢复绘图上下文状态（Save、Restore）

  - 保存上下文状态到栈中，save 之后，可调用平移、缩放、旋转、裁剪等操作
  - 恢复上下文之前保存的状态，防止 save 后对 Canvas 执行的操作对后续的绘制有影响

- context 状态保存及恢复案例，理解状态堆栈

  ```javascript
  context.fillStyle = 'red';
  context.save();
  context.fillStyle = 'blue';
  context.fillRect(0, 0, 200, 200);
  context.restore();
  context.fillRect(100, 100, 100, 100);
  ```

[demo](https://github.com/hewq/course-H5-Animation-and-Game-Development/blob/master/ch02/LS02/LS02_03.html)

## Canvas 图形及路径

- Canvas 直线相关绘制

  > 状态设置
  >
  > > ```javascript
  > > context.moveTo(100, 100);
  > > context.lineTo(200, 200);
  > > context.lineWidth = 10;
  > > context.strokeStyle = '#058';
  > > ```
  >
  > 绘制
  >
  > >context.stroke()

- 也可以通过 Path2D 构造函数创建路径对象

-  理解 beginPath 的作用（绘制多条直线时可能遇到的问题）

  - canvas 中的绘制方法（如 stroke， fill），都会以“上次 beginPath“之后的所有路径为基础进行绘制，不管你用 moveTo 把画笔移动到哪里，只要不 beginPath，都是在画一条路径，fillRect 与 strokeRect 这种直接画出独立区域的函数，也不会打断当前的 path

- 理解 closePath 的作用

  - closePath 的意思不是结束路径，而是关闭路径，它会试图从（moveTo点之后）当前路径的终点连一条路径到起点，让整个路径闭合起来。但是，这并不意味着它之后的路径就是新路径了

- beginPath 和 closePath 的作用不同，并不是必须成对出现

[demo](https://github.com/hewq/course-H5-Animation-and-Game-Development/blob/master/ch02/LS02/LS02_04.html)

- 线宽及颜色样式
  - lineWidth、strokeStyle、fillStyle
  - stroke()、fill()
- 线端点样式（lineCap)
  - butt(default)、round、square
- 连接点样式（lineJoin)
  - miter(default)、 bevel、round
- 样式与上下文状态（context status）

[demo](https://github.com/hewq/course-H5-Animation-and-Game-Development/blob/master/ch02/LS02/LS02_05.html)

- Canvas 曲线相关绘制（绘制弧）

  - context.arc(centerx, centery, radius, startingAngle, endingAngle, anticlockwise = false)

    ![](./arc.png)

[demo](https://github.com/hewq/course-H5-Animation-and-Game-Development/blob/master/ch02/LS02/LS02_06.html)

- Canvas 曲线相关绘制（绘制二次曲线）

  context.moveTo(x0, y0);

  context.quadraticCurveTo(x1, y1, x2, y2);  // x1, y1: 控制点；x2, y2: 结束点

- Canvas 曲线相关绘制（绘制贝塞尔曲线）

  context.moveTo(x0, y0);

  context.bezierCurveTo(x1, y1, x2, y2, x3, y3);  // x1, y1: 控制点；x2, y2: 控制点； x3, y3: 结束点

[demo](https://github.com/hewq/course-H5-Animation-and-Game-Development/blob/master/ch02/LS02/LS02_07.html)

## Canvas 绘制基本形状

- Canvas 绘制矩形相关

  > > ctx.moveTo(x, y);
  > > ctx.lineTo(x + width, y);
  > > ctx.lineTo(x +width, y + height);
  > > ctx.lienTo(x, y + height);
  >
  > ctx.rect(x, y, width, height);

- 手动绘制的区别在于能够控制绘图方向（对填充的影响）

- 其他相关方法（fillRect()、 strokeRect()、 clearRect()）

- Canvas 绘制椭圆形相关

  ```javascript
  var canvas = document.getElementById('canvas');
  var ctx = canvas.getContext('2d');
  ctx.beginPath();
  // x, y, radiusX, radiusY, rotation, startAngle, endAngle, anticlockwise(默认为false)
  ctx.ellipse(100, 100, 50, 75, 45 * Math.PI / 180, 0, 2 * Math.PI); // 倾斜45度角
  ctx.stroke();
  ```

- 扩展 context

  ```javascript
  CanvasRenderingContext2D.prototype.triangle = function (x1, y1, x2, y2, x3, y3) {
      this.moveTo(x1, y1);
      this.lineTo(x2, y2);
      this.lineTo(x3, y3);
      this.closePath();
      this.stroke();
  }
  ```

[demo](https://github.com/hewq/course-H5-Animation-and-Game-Development/blob/master/ch02/LS02/LS02_08.html)