# H5 Canvas 动画

## 循环动画

- 循环动画方法

  ```javascript
  window.setTimeOut(); // 缺点：不准确，不适合用于动画
  window.setInterval(); // 同上
  window.requestAnimationFrame(); // 适合动画实现
  ```

- requestAnimationFrame 兼容性问题

  ```javascript
  window.webktRequestAnimationFrame()
  window.mozRequestAnimationFrame()
  window.oRequestAnimationFrame()
  window.msRequestAnimationFrame()
  ```

- 启动动画循环

  ```javascript
  var anim = function () {
      requesAnimationFrame(anim);
  };
  
  var animHandle = requestAnimationFrame(anim);
  ```

- 停止动画循环

  ```javascript
  cancelAnimationFrame(animHandle);
  ```

[demo1](https://github.com/hewq/course-H5-Animation-and-Game-Development/blob/master/apps/ch04/LS04/LS04_01.html)

[demo2](https://github.com/hewq/course-H5-Animation-and-Game-Development/blob/master/apps/ch04/LS04/LS04_02.html)

- [帧动画](https://github.com/hewq/course-H5-Animation-and-Game-Development/blob/master/apps/ch04/LS04/LS04_03.html)

## 重力与碰撞

- 实现重力加速度
  - F = ma = mg
  - 标准重力加速度：9.80665 m/s^2

[demo1](https://github.com/hewq/course-H5-Animation-and-Game-Development/blob/master/apps/ch04/LS04/LS04_04.html)

[demo2](https://github.com/hewq/course-H5-Animation-and-Game-Development/blob/master/apps/ch04/LS04/LS04_05.html)

- 物体碰撞的实现
  - 平面碰撞（角度、速度）
  - 物理引擎（box2d）

[demo1](https://github.com/hewq/course-H5-Animation-and-Game-Development/blob/master/apps/ch04/LS04/LS04_06.html)

[demo2](https://github.com/hewq/course-H5-Animation-and-Game-Development/blob/master/apps/ch04/LS04/LS04_07.html)