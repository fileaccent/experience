# 用法:

引入库之后

html 中 建立一个存放二维码的盒子
``` html
<div class="QRcode"> 
</div>
```
在 js 中创建QRcode对象

QRCode 第一个参数是要存放二维码的盒子,第二个参数是一个对二维码进行配置的对象
示例如下:
``` javascript
let QRcode =  new QRCode(document.querySelector(".QRcode"),
{
  text: window.location.href.split('?')[0].replace('share.html', 'index.html'),// text 填写要生成的url
  colorDark: '#000000', // 这些属性默认即可
  colorLight: '#ffffff',
  correctLevel: QRCode.CorrectLevel.H
});
```
这样就生成了一个二维码;

注意:

生成的二维码为 canvas
不能进行缩放,如果要进行缩放请转换成图片
参考 canvas2img