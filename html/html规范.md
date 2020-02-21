
## 规范
### 头部要求:
#### PC 端
``` html
<meta charset="utf-8">
<meta name="keywords" content="your keywords">
<meta name="description" content="your description">
<meta name="author" content="author,email address">
<meta http-equiv="X-UA-Compatible" content="IE=Edge,chrome=1">
```
#### 移动端
``` html
<meta charset="utf-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=no">
<meta name="format-detection" content="telephone=no">
```
### 标签

* 自定义标签必须包含 - 
* 标签必须闭合

### 嵌套

* 块元素可以包含内联元素或某些块元素，但内联元素却不能包含块元素，它只能包含其它的内联元素

* 标题和段落中不能包含块，如：h1、h2、h3、h4、h5、h6、p、dt

* 块与内联不能并列，块级元素与块级元素并列、内嵌元素与内嵌元素并列

* 有些标签是固定的嵌套规则，比如 ul 包含 li、ol 包含 li、dl 包含 dt 和 dd 等等。

### 注释

请另起一行放在模块的上面

### 语义化

尽量多使用语义化标签, 不要全部用 div 构成
