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

  