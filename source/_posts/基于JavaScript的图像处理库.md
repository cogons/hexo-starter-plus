---
title: 基于JavaScript的图像处理库
tags: []
number: 10
date: 2017-06-14 07:38:30
---

# Browser

### 0. HTML5 Canvas

```js
var c=document.getElementById("myCanvas");
var ctx=c.getContext("2d");
ctx.moveTo(0,0);
ctx.lineTo(200,100);
ctx.stroke();
```

### 1. Caman JS

http://camanjs.com/

**Orientation:** Canvas Enhancement

(ca)nvas (man)ipulation

work on both browser and node

```js
// browser

Caman("#canvas-id", "path/to/image.jpg", function () {
  this.brightness(5).render();
});

// data-attribute
 <img 
    data-caman="brightness(10) contrast(30) sepia(60) saturation(-30)"
    data-caman-hidpi="/path/to/image@2x.jpg"
    src="path/to/image.jpg"
  >

// node

Caman("/path/to/file.png", function () {
  this.brightness(5);
  this.render(function () {
    this.save("/path/to/output.png");
  });
});
```


### 2. glfx.js

https://github.com/evanw/glfx.js

**Orientation:** Image Effects

canvas

```js
var canvas = fx.canvas();
// convert the image to a texture
var image = document.getElementById('image');
var texture = canvas.texture(image);
// apply the ink filter
canvas.draw(texture).ink(0.25).update();
// replace the image with the canvas
image.parentNode.insertBefore(canvas, image);
image.parentNode.removeChild(image);
```

### 3.  Filtrr2

https://github.com/alexmic/filtrr

**Orientation:** Image Effects

**Dependency:** jQuery

canvas

```js
Filtrr2("#my-img", function() {
    this.brighten(50)
        .saturate(-50)
        .render();       //lazily apply
});
```

### 4. AlloyImage

https://github.com/AlloyTeam/AlloyImage

**Orientation:** image effects

**Feature:** photoshop-like, layer

```js
var img = new Image();
img.src = "pic.jpg";
img.onload = function(){//素描效果
      AlloyImage(this)
      .act("灰度处理")
      .add(//添加一个图层上去
            AlloyImage(this)
            .act("灰度处理")
            .act("反色")
            .act("高斯模糊",5) , "颜色减淡"  
      )
      .act("锐化")
      .show();
};
```

### 5. Fabric.js

https://github.com/kangax/fabric.js/

**Orientation:** Canvas Enhancement

**Feature:** svg-canvas parser




```js
// image
fabric.Image.fromURL('my_image.png', function(oImg) {
  oImg.scale(0.5).setFlipX(true);
  canvas.add(oImg);
});

//shape
var rect = new fabric.Rect({
  left: 100, top: 100, fill: 'red', width: 20, height: 20});

canvas.add(rect);
```
---

# Node

### 1. node-opencv

https://github.com/peterbraden/node-opencv

**Dependency:** opencv

**API style:** callback

```js
cv.readImage("./examples/files/mona.png", function(err, im){
  im.detectObject(cv.FACE_CASCADE, {}, function(err, faces){
    for (var i=0;i<faces.length; i++){
      var x = faces[i]
      im.ellipse(x.x + x.width/2, x.y + x.height/2, x.width/2, x.height/2);
    }
    im.save('./out.jpg');
  });
})
```

### 2. gm

https://github.com/aheckmann/gm

**Dependency:** GraphicsMagick and ImageMagick

**API style:** chaining

```js
var fs = require('fs')
  , gm = require('gm');
gm('/path/to/my/img.jpg')
    .stroke("#ffffff")
    .drawCircle(10, 10, 20, 10)
    .font("Helvetica.ttf", 12)
    .drawText(30, 20, "GMagick!")
    .write("/path/to/drawing.png", function (err) {
      if (!err) console.log('done');
    });
```

### 3. jimp

https://github.com/oliver-moran/jimp

**No Dependency / pure JS**

**API style:** chaining & callback

```js
var Jimp = require("jimp");
Jimp.read("lenna.png", function (err, image) {
    this.greyscale().scale(0.5).write("lena-half-bw.png");
});
```

### 4. sharp

https://github.com/lovell/sharp

**Dependency:** libvips (lightweight)

**API style:** chaining & promise

```js
sharp('input.jpg')
  .rotate()
  .resize(200)
  .toBuffer()
  .then( data => ... )
  .catch( err => ... );
```

### 5. node-images

https://github.com/zhangyuanwei/node-images

**No dependency / C++**

**API style:** chaining API

```js
var images = require("images");
images("input.jpg")
.size(400)
.draw(images("logo.png"), 10, 10)
.save("output.jpg", {quality : 50});
```