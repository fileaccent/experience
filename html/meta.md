# meta 元素

## 一. 设置编码 charset
``` html
<meta charset="utf-8">
```
## 二. http-equiv content

语法: <meta http-equiv="参数" content="参数变量值">

### 1. expires(期限)

设置网页过期的期限
``` html
<meta http-equiv="expires" content="Wed, 20 Jun 2007 22:33:00 GMT">  
```
### 2. pragma(cache模式)
``` html
<meta http-equiv="Pragma" content="no-cache">  
```
注意：这样设定，访问者将无法脱机浏览。 

### 3. refresh 刷新
``` html
<meta http-equiv="Refresh" content="2；URL=http://www.net.cn/">  
```
2 指的是 2 秒后跳转到新网页

### 4. set-cookie

网页过期,cookie被删除

``` html
<meta http-equiv="Set-Cookie" content="cookievalue=xxx;expires=Wednesday, 20-Jun-2007 22:33:00 GMT； path=/">  
```

### 5. window-target (重要)

禁止使用 iframe 显示

``` html
<meta http-equiv="Window-target" content="_top">  
```

### 6. Page_Enter、Page_Exit 

设定进入页面时的特殊效果

``` html
<meta http-equiv="Page-Enter"    contect="revealTrans(duration=1.0,transtion=    12)">    
```

设定离开页面时的特殊效果

``` html
<meta http-equiv="Page-Exit"    contect="revealTrans(duration=1.0,transtion=    12)">    
```

Duration的值为网页动态过渡的时间，单位为秒。

Transition是过渡方式，它的值为0到23，分别对应24种过渡方式。如下表：
 
|属性值|效果|属性值|效果| 
|:-:|:-:|:-:|:-:|:-:|
|0      |盒状收缩|          1|            盒状放射|
|2      |圆形收缩|          3|            圆形放射|  
|4      |由下往上|          5|            由上往下|  
|6      |从左至右|          7|            从右至左|  
|8      |垂直百叶窗|        9|          水平百叶窗|  
|10    |水平格状百叶窗|     11|      垂直格状百叶窗|  
|12    |随意溶解|           13|从左右两端向中间展开|  
|14    |从中间向左右两端展开|15|从上下两端向中间展开| 
|16    |从中间向上下两端展开|17|从右上角向左下角展开|  
|18    |从右下角向左上角展开|19|从左上角向右下角展开| 
|20    |从左下角向右上角展开|21|      水平线状展开 |
|22    |垂直线状展开       |23|随机产生一种过渡方式|  

### 7. 清除缓存(重要)
``` html
<meta http-equiv="cache-control" content="no-cache"> 
```
### 8. keywords 给搜索引擎使用

``` html
<meta http-equiv="keywords" content="keywords">
```

### 9. 页面描述

<meta http-equiv="description" content="This is my page">  


## 三. name

### 1. referrer  控制所有从该文档发出的 HTTP 请求中HTTP Referer 首部的内容：
 
 <meta name="referrer"> content 属性可取的值：
  * no-referrer	不要发送 HTTP Referer 首部。
  * origin	发送当前文档的 origin。
  * no-referrer-when-downgrade	当目的地是先验安全的(https->https)则发送  
  
  * origin 作为 referrer ，但是当目的地是较不安全的 (https->http)时则不发送 referrer 。这个是默认的行为。

  * origin-when-crossorigin	在同源请求下，发送完整的URL (不含查询参数) ，其他情况下则仅发送当前文档的 origin。
  * unsafe-URL	在同源请求下，发送完整的URL (不含查询参数)。
### 2.  viewport

  关于窗口的设置
  |属性值|值|作用|
  |:-:|:-:|:-:|
  |width	        |一个正整数或者字符串 device-width|	以pixels（像素）为单位， 定义viewport（视口）的宽度。|
  |height	        |一个正整数或者字符串 device-height|	以pixels（像素）为单位， 定义viewport（视口）的高度。|
  |initial-scale	|一个0.0 到10.0之间的正数|	          定义设备宽度（纵向模式下的设备宽度或横向模式下的设备高度）与视口大小之间的缩放比率。|
  |maximum-scale	|一个0.0 到10.0之间的正数|	          定义缩放的最大值；|它必须大于或等于minimum-scale的值，不然会导致不确定的行为发生。|
  |minimum-scale	|一个0.0 到10.0之间的正数|	          定义缩放的最小值；它必须小于或等于maximum-scale的值，不然会导致不确定的行为发生。|
  |user-scalable	|一个布尔值（yes 或者no）|	          如果设置为 no，用户将不能放大或缩小网页。默认值为 yes。|

  移动端常用
  ``` html 
  <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, minimum-scale=1.0, user-scalable=no, minimal-ui">
  ```
### 3. 用于搜索

<meta name="author" content="fileaccent">

<meta name="description" content="practice">

### 4. 其他网站元数据

参考每个网站的内容

### 5. 为网站添加小图标

``` html
<meta rel="shortcut icon" href="favicon.ico" type="image/x-icon">
```

最好使用 .ico 格式的图片,这在所有浏览器都适用


## 常用示例:

### 移动端适配:
``` html
  <meta name="viewport" content="width=device-width, initial-scale=1.0,  maximum-scale=1.0, minimum-scale=1.0, user-scalable=no, minimal-ui">
```
### 忽略页面中的数字识别为电话，忽略email识别 -->(ios常用)

``` html
<meta name="format-detection" content="telphone=no, email=no" />
```
### 禁止使用 iframe 显示

``` html
<meta http-equiv="Window-target" content="_top">  
```

### 清除缓存

``` html
<meta http-equiv="cache-control" content="no-cache"> 
```

### 删除苹果默认的工具栏和菜单栏

``` html
<meta name="apple-mobile-web-app-capable" content="yes" />
```

### 设置苹果工具栏颜色

``` html
<meta name="apple-mobile-web-app-status-bar-style" content="black" />
```

### 启用360浏览器的极速模式(webkit)

``` html
<meta name="renderer" content="webkit">
```

