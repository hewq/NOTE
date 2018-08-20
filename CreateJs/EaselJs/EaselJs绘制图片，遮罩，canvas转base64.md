## EaselJs绘制图片，遮罩，canvas转base64

1. EaselJs绘制图片，使用Bitmap

   ```js
   var bg = new createjs.Bitmap( img );
   var bg2 = new createjs.Bitmap( img );

   bg.setTransform( 0, 0, 0.25, 0.25 );
   bg2.setTransform( canvas.width / 2, 0, 0.25, 0.25 );

   stage.addChild( bg );
   stage.addChild( bg2 );
   ```

   [Bitmap](http://www.createjs.cc/src/docs/easeljs/classes/Bitmap.html)

2. 遮罩

   ```js
   var shape = new createjs.Shape();
   shape.graphics.beginFill('#000').drawCircle(canvas.width / 2 - 30, 100,35);
   shape.x = 20;
   shape.y = 20;
   bitmapHeadPortrait.mask = shape; // bitmap添加遮罩

   stage.addChild( shape );
   stage.addChild( bitmapHeadPortrait );
   stage.update();		
   ```

   ​

3. canvas转base64

   ```js
   canvas.toDataURL("image/png");
   ```

   ​

[Demo](https://github.com/hewq/Front-end/tree/master/apps/JavaScript/CreateJs/EaselJs/EaselJs%E7%BB%98%E5%88%B6%E5%9B%BE%E7%89%87/assets/index.html)

