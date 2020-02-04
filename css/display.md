从大的分类上讲，display的32种写法可以分为6个大类，再加上一个全局类，一共是7个大类：

1 外部值

2 内部值

3 列表值

4 属性值

5 显示值

6 混合值

7 全局值

一. 外部值

只会影响外在的表现, 不影响里面的子元素

display:block;

display:inline; 行内元素,例如 p,h1

display:flow-root;
可用于撑开设置完 float  的容器

display:table;
表单盒子,重点学习

display:flex;
flex布局,重点学习

display:grid;
grid布局,重点学习

属性值

属性值一般是附属于主值的，比如主值里设置了 display:table;，就可以在子元素里使用 display:table-row-group;等等属性，不过并不绝对。关于它们的作用，主要参考主值就够了。

display: table-row-group;

详情参考display: table;。

display: table-header-group;

详情参考display: table;。

display: table-footer-group;

详情参考display: table;。

display: table-row;

详情参考display: table;。

display: table-cell;

详情参考display: table;。这个属性有必要详细说说，因为它完全可以单独应用，用在高度不固定元素的垂直居中上 
 
display: table-column-group;

详情参考display: table;。

display: table-column;

详情参考display: table;。

display: table-caption;

详情参考display: table;。

display: ruby-base;

详情参考display: ruby;。

display: ruby-text;

详情参考display: ruby;。

display: ruby-base-container;

详情参考display: ruby;。

display: ruby-text-container;

详情参考display: ruby;。 

显示值

display: contents;

让子元素拥有与父元素一样的布局

display:none;

display:inline-block;

display:inline-table;

 display: inline-flex;

这个就不用多说了吧？跟上面一样，在行内进行弹性布局，参考display: flex;。

display: inline-grid;

同上，在行内进行网格布局，参考display: grid;。