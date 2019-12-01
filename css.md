希望我能多写心得
1. 通过transition属性,可以使我们在使用:hover时改变属性的值有动画的感觉
(不过好像只有长度之类的有效,比如border,outline等等时没有效果的)
```css
  transition:all 0.5s linear;/* 设置所有的属性变化时,有过渡效果 */
```
2.通过box-sizing属性使元素在改变border宽度时,保持总体长度不变
```css
  box-sizing:border-box;/* 使border放在元素里面,保持整个元素宽高不变,防止影响整体的css
```
3. 如何用纯css修改input的radio样式
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
  4. 使div中的文本在第三行有多的时候,采用省略号省略后面的文本
  ```css
  display: -webkit-box;
  -webkit-box-orient: vertical;
  -webkit-line-clamp: 3;
  overflow: hidden;

  ```

   5.设置英文换行

  ```css
  word-break:break-all;
  ```

  6. 如何居中多行的文字

  ```css
    设置父元素的属性为 display:table;
    子元素的属性为    display:table-cell;
    便可使用
    text-align:center;和Vertical-align:center;居中
  ```

   