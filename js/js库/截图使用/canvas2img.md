
## 方式一
let imgQRcode = Canvas2Image.convertToImage(canvas, canva.width, canva.height);

canvas 指的是 需要被转换的 canvas 元素,需要输入,长,宽
imgQRcode是生成的 img dom 元素 直接插入即可,不过会插入两张图片,删除一张即可
``` javascript
document.querySelector('.QRcode').append(imgQRcode);
document.querySelector('.QRcode').removeChild(document.querySelector('.QRcode img'));
```
## 方式二
``` javascript
let imgUrl = canvas.toDataURL('jpg');
```
canvas 为 canvas 元素
toDataURL 返回 图片的base64 地址

直接用于 src 即可