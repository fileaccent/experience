### css 的结构和规则
  少使用 id 选择器
  #### 关联选择器
  * 后代选择器
  p em {} 只会确定 p 中的所有元素: 包括直接子元素和间接子元素 em
  * 子元素选择器
  p > em {} 只会确定 p 中的子元素 em 们,不会再选择嵌套再深的 em
  * 相邻兄弟选择器
  ``` css
  h1 + p {margin-top:50px;}
  ```
  这个选择器读作：“选择紧接在 h1 元素后出现的段落，h1 和 p 元素拥有共同的父元素”。
  注意: 只能选择后面的那个元素
  #### 我们假设 class 为 important 的所有元素都是粗体，而 class 为 warning 的所有元素为斜体，class 中同时包含 important 和 warning 的所有元素还有一个银色的背景 。就可以写作：
  ``` css
  .important {font-weight:bold;}
  .warning {font-style:italic;}
  .important.warning {background:silver;}
  ```
  #### 组合
  p,h2,div {} 将 p, h2, div 的相同样式
  #### 伪类和伪元素
  举例:
  ``` css
  A:link { color: red }
  A:active { color: blue; font-size: 125% }
  A:visited { color: green; font-size: 85% }
  ```
### 属性选择器
下面的例子为 title="W3School" 的所有元素设置样式：
``` css
[title=W3School]
{
border:5px solid blue;
}
```
下面的例子为包含指定值的 title 属性的所有元素设置样式。适用于由空格分隔的属性值：
``` css
[title~=hello] { color:red; }
```
下面的例子为带有包含指定值开头的 lang 属性的所有元素设置样式。适用于由连字符分隔的属性值：
``` css
[lang|=en] { color:red; }
```
其他选择器:
[attribute^=value]	匹配属性值以指定值开头的每个元素。
[attribute$=value]	匹配属性值以指定值结尾的每个元素。
[attribute*=value]	匹配属性值中包含指定值的每个元素。
### css 背景
背景定位 background-position 
background-position:center; // 会使背景居中
background-position:50% 50%; // 使背景图片居中
background-attachment // 如果文档比较长,背景会随着文档滚动可设置该属性,防止滚动
background-size // 大小
background-origin // 规定背景图片的所在的位置
背景图片可以放置于 content-box、padding-box 或 border-box 区域。
``` css
body 
  {
  background-image:url(/i/eg_bg_02.gif);
  background-repeat:no-repeat;
  background-attachment:fixed
  }
```
### css 文字

#### text-indent
提供缩进

#### text-align 居中常用

#### letter-spacing 设置字的间隔

#### text-transform 处理文本
* none 什么都不做
* uppercase 大写
* lowercase 小写
* capitalize 首字母大写

#### text-decoration 装饰文字
* none 什么都不做
* underline 下划线
* overline 上划线
* line-through 删除线
* blink 

可以既有上划线,也有下划线

#### white-space 控制空白字符的噶事
* normal 将多个空格合并成一个空格,并忽略回车
* pre 保留原格式
* nowarp 设置文本无法换行
### 表格

#### 属性	             描述
* border-collapse	设置是否把表格边框合并为单一的边框。
* border-spacing	设置分隔单元格边框的距离。
* caption-side	  设置表格标题的位置。
* empty-cells	    设置是否显示表格中的空单元格。
* table-layout	  设置显示单元、行和列的算法。
### padding

#### 可接受四个值,分别为 上, 右, 下, 做

### css 外边距合并

### 伪类

#### 链接的伪类

``` css
a:link {color: #FF0000}		/* 未访问的链接 */
a:visited {color: #00FF00}	/* 已访问的链接 */
a:hover {color: #FF00FF}	/* 鼠标移动到链接上 */
a:active {color: #0000FF}	/* 选定的链接 */
```
提示:
* 在 CSS 定义中，a:hover 必须被置于 a:link 和 a:visited 之后，才是有效的。

* 在 CSS 定义中，a:active 必须被置于 a:hover 之后，才是有效的。

* 伪类名称对大小写不敏感。

#### :first-child 伪类

第一个规则将作为某元素第一个子元素的所有 p 元素设置为粗体。

第二个规则将作为某个元素（在 HTML 中，这肯定是 ol 或 ul 元素）第一个子元素的所有 li 元素变成大写。

``` css
p:first-child {font-weight: bold;}
li:first-child {text-transform:uppercase;}
``` 

#### 总结

W3C："W3C" 列指示出该属性在哪个 CSS 版本中定义（CSS1 还是 CSS2）。

属性	                 描述
:active	       向被激活的元素添加样式。
:focus	       向拥有键盘输入焦点的元素添加样式。
:hover	       当鼠标悬浮在元素上方时，向元素添加样式。
:link 	       向未被访问的链接添加样式。
:visited       向已被访问的链接添加样式。
:first-child	 向元素的第一个子元素添加样式。
:lang	         向带有指定 lang 属性的元素添加样式。

### 伪元素

#### :first-line

#### :first-letter

#### :before

#### :after

### css 边框

#### border-radius 为元素添加圆角

如果有四个值,则分别为 左上 右上 右下 左下 的值

### css 2D 转换

#### translate()
左右上下移动
``` css
div
{
transform: translate(50px,100px);
-ms-transform: translate(50px,100px);		/* IE 9 */
-webkit-transform: translate(50px,100px);	/* Safari and Chrome */
-o-transform: translate(50px,100px);		/* Opera */
-moz-transform: translate(50px,100px);		/* Firefox */
}
```
#### rotate() 旋转
``` css
div
{
transform: rotate(30deg);
-ms-transform: rotate(30deg);		/* IE 9 */
-webkit-transform: rotate(30deg);	/* Safari and Chrome */
-o-transform: rotate(30deg);		/* Opera */
-moz-transform: rotate(30deg);		/* Firefox */
}
```
#### scale() 方法
``` css
div
{
transform: scale(2,4);
-ms-transform: scale(2,4);	/* IE 9 */
-webkit-transform: scale(2,4);	/* Safari 和 Chrome */
-o-transform: scale(2,4);	/* Opera */
-moz-transform: scale(2,4);	/* Firefox */
}
```
#### skew()
``` css
div
{
transform: skew(30deg,20deg);
-ms-transform: skew(30deg,20deg);	/* IE 9 */
-webkit-transform: skew(30deg,20deg);	/* Safari and Chrome */
-o-transform: skew(30deg,20deg);	/* Opera */
-moz-transform: skew(30deg,20deg);	/* Firefox */
}
```
### css3 动画
``` css

@keyframes myfirst
{
from {background: red;}
to {background: yellow;}
}
div
{
animation: myfirst 5s;
-moz-animation: myfirst 5s;	/* Firefox */
-webkit-animation: myfirst 5s;	/* Safari 和 Chrome */
-o-animation: myfirst 5s;	/* Opera */
}
```
#### CSS3 动画属性
下面的表格列出了 @keyframes 规则和所有动画属性：

属性	描述	CSS
* @keyframes	规定动画。	3
* animation	所有动画属性的简写属性，除了 animation-play-state 属性。	3
* animation-name	规定 @keyframes 动画的名称。	3
* animation-duration	规定动画完成一个周期所花费的秒或毫秒。默认是 0。	3
* animation-timing-function	规定动画的速度曲线。默认是 "ease"。	3
* animation-delay	规定动画何时开始。默认是 0。	3
* animation-iteration-count	规定动画被播放的次数。默认是 1。	3
* animation-direction	规定动画是否在下一周期逆向地播放。默认是 "normal"。	3
* animation-play-state	规定动画是否正在运行或暂停。默认是 "running"。	3
* animation-fill-mode	规定对象动画时间之外的状态。	3
### 用户界面
#### resize
     规定用户是否可以调整元素尺寸
#### box-sizing
box-sizing:border-box; // 让边框包含在框里面
####  outline-offset
