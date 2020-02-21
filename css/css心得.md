# 希望我能多写心得
## 1. 通过transition属性,可以使我们在使用:hover时改变属性的值有动画的感觉
(不过好像只有长度之类的有效,比如border,outline等等时没有效果的)
```css
transition:all 0.5s linear;/* 设置所有的属性变化时,有过渡效果 */
```
## 2.通过box-sizing属性使元素在改变border宽度时,保持总体长度不变
```css
box-sizing:border-box;/* 使border放在元素里面,保持整个元素宽高不变,防止影响整体的css
```
## 3. 如何用纯css修改input的radio样式
```html
<div class="radioBox">
  <input type="radio" id="man" name="sex" v-model="registerData.value" value="男"/>
  <label for="man"></label>
</div>
```
```css
/* 对号 */
.radioBox {
  width:10vw;
  height:10vw;
  margin:0;
  line-height:10vw;
  display: inline-block;
}
input[type="radio"] {
  width:0;
  height:0;
  margin:0;
  opacity:0;
}
input[type="radio"] + label {
  display: inline-block;
  width:40%;
  height:40%;
  border-radius:50%;
  font-size:3vw;
  border:1px solid rgb(139, 182, 207);
  position:relative;
  transition:all 0.3s ease;
  vertical-align: -5%;
}
input[type="radio"]:checked + label {
  background-color: rgb(139, 182, 207);
}
input[type="radio"]:checked + label::after {
  display:inline-block;
  width:40%;
  height:40%;
  content: '√';
  color:white;
  position: absolute;
  top:-70%;
  left:20%;
  z-index:2;
}
/* 加图片 */
.radioBox {
  width:10vw;
  height:10vw;
  margin:0;
  line-height:10vw;
  display: inline-block;
}
.registerItemInputSex:first-child {
  margin-left:4vw;
}
input[type="radio"] {
  width:0;
  height:0;
  margin:0;
  opacity:0;
}
input[type="radio"] + label {
  display: inline-block;
  width:40%;
  height:40%;
  border-radius:50%;
  font-size:3vw;
  border:1px solid rgb(139, 182, 207);
  position:relative;
  transition:all 0.3s ease;
  vertical-align: -5%;
}
/*
input[type="radio"]:checked + label {
  background-color: rgb(139, 182, 207);
}
*/
input[type="radio"] + label:hover {
  border:1px solid rgb(139, 182, 207);
}
input[type="radio"]:checked + label::after {
  content: '';
  display:inline-block;
  background:url('./static/right.svg');
  background-size:cover;
  width:60%;
  height:60%;
  position: absolute;
  top:20%;
  left:19%;
  z-index:2;
}
```
## 4. 使div中的文本在第三行有多的时候,采用省略号省略后面的文本
```css
display: -webkit-box;
-webkit-box-orient: vertical;
-webkit-line-clamp: 3;
overflow: hidden;

```
实现单行文本的溢出显示省略号
```css
overflow: hidden;
text-overflow:ellipsis;
white-space: nowrap;
```

## 5.设置英文换行

```css
word-break:break-all;
```

## 6. 如何居中多行的文字

```css
  设置父元素的属性为 display:table;
  子元素的属性为    display:table-cell;
  便可使用
  text-align:center;和Vertical-align:center;居中
```
## 7. marign 的 四个是 从上到右到下到坐
              两个是 上下到左右
## 8. 如果一个容器,他的高度已经小于元素的高度和margin之和,那么增加一个元素的margin的会把所有的元素往上顶.

## 9.scroll-view使用横向滑动,必须添加属性 white-spacing:nowarp;
## 10. 裁剪 

  clip 需要设置 position 为 absolute, fixed 等等

## 11. input 垂直居中,使用 flex 居中

    ```  css
    input-box {
        display:flex;
        justify-content:center;
        align-content:center;
    }
    ```
## 12. 如果 在 flex 布局的元素中,有纯文字的项目,那么不需要设置任何关于宽高,行高之类的样式. 要调整相对距离,加上 padding 即可
    

## 13.在做手机端开发时。遇到问题：input输入框安卓手机可以输入和点击，但是到苹果手机上input输入框就不能点了也不能输入了，原因就是下面这几行css代码的影响，删掉就行了。
``` css
-moz-user-select: none;  //css 让文字不被选中

-webkit-user-select: none; //禁止移动端用户用鼠标在页面上选中文字

user-select: none; //禁止用户用鼠标在页面上选中文字
```

## 14. 使用width:100%;height:100%; 父元素要设置 position:relative;

## 15. 如果绝对定位, 留下空白,可以通过一个框,占住,下面的位置,保证布局完整.
  position:relative;
  margin:auto;
  padding-top:100px;
## 16. 页面初始布局
``` css
* {
  margin:0;
  padding:0;
  box-sizing:border-box;
  -webkit-tap-highlight-color:raba(0, 0, 0, 0);
    /* transparent 属性有些浏览器会失效 */
}
.container {
  width:100vw;
  height:100vh;
}
```

## 17. 有些去除样式,必须使用
  -webkit-appearance:none;
  appearance:none;
  无效

## 18. poiner-events:none; 点击穿透,使上面的内容,成为影子,点击事件不能使用
    但是下面的元素不要设置为 z-index:-1; 这样下面的点击事件无法使用