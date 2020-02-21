# link 标签

## rel 属性

### 引入css

href 属性用于指定 文件的目录

``` html
<link href="main.css" rel="stylesheet">
```

当然你可以添加条件,来限制 css 的加载

``` html
<link href="mobile.css" rel="stylesheet" media="screen and (max-width: 600px)">
```

上述表达式,表示屏幕宽度小于 600px ,才加载mobile.css
### 引用网站图标

`` html
<link rel="icon" href="favicon.ico">
```

### 预加载

通过 将 rel 设置为 preload 来告诉浏览器, 在进行生命周期的同时加载这些元素,而不是随着文档流逐步被加载.

``` html
<link rel="preload" as="image">
```
#### as 属性

指定加载元素的类型,如果类型错误,浏览器仍会加载, 但是会进去文档流进行加载,基本上算没写.

as 可能是以下值

* script

* style

* image

* media

* document

* font

当然还有其他的,这里就不列举了

#### crossorigin

此属性指定在加载相关图片时是否必须使用 CORS. 启用 CORS 的图片 可以在 <canvas> 元素中使用, 并避免其被污染.
 
常见于 截图, 图片转canvas 中

可取的值如下:

* anonymous (注意不设置这个,canvas不能使用跨域图片)


会发起一个跨域请求(即包含 Origin: HTTP 头). 但不会发送任何认证信息 (即不发送 cookie, X.509 证书和 HTTP 基本认证信息). 如果服务器没有给出源站凭证 (不设置 Access-Control-Allow-Origin: HTTP 头), 这张图片就会被污染并限制使用.

一般用这个,访问跨域的图片,然后绘制在canvas,再本地使用

* use-credentials

会发起一个带有认证信息 (发送 cookie, X.509 证书和 HTTP 基本认证信息) 的跨域请求 (即包含 Origin: HTTP 头). 如果服务器没有给出源站凭证 (不设置 Access-Control-Allow-Origin: HTTP 头), 这张图片就会被污染并限制使用.

### 选择样式

用户可以在浏览器菜单 "查看>页面样式" 来选择网页的样式。通过这一办法，可以用多种样式浏览网页。

``` html
<link href="default.css" rel="stylesheet" title="Default Style">
<link href="fancy.css" rel="alternate stylesheet" title="Fancy">
<link href="basic.css" rel="alternate stylesheet" title="Basic">
```
## 其他属性


### 样式表加载事件

你能够通过监听发生在样式表上的事件知道什么时候样式表加载完毕。同样的，你能够通过监听error事件检测到是否在加载样式表的过程中出现错误。
``` javascript
<script>
function sheetLoaded() {
  // Do something interesting; the sheet has been loaded
}

function sheetError() {
  alert("An error occurred loading the stylesheet!");
}
</script>

<link rel="stylesheet" href="mystylesheet.css" onload="sheetLoaded()" onerror="sheetError()">
```
### importance

设置资源的重要性

auto: 一般

high: 优先级搞

low: 优先级低

### sizes 属性

用于指定 icon 的大小

一般只包含一个值

### type

最常用的就是 text/css
