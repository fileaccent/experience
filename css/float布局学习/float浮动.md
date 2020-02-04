float 用于为页面调整布局等等工作,曾经有过悍马功劳,虽然现在有 flex,grid 布局,但是 float 依然是兼容性最好的布局,现在我们来探究一下,如何更好的使用 float

float 属性,使元素脱离文本流,悬浮与文本流之上

设置 float 会使元素紧跟上一个 设置相同 float 的元素,若前面没有相同元素紧跟在上一个元素的下面,并且下面其他的文本流元素,会忽视 float 元素, 紧跟在上一个文本流元素,仿佛不存在 float 元素一样.

(详见 https://www.cnblogs.com/zhongxinWang/archive/2013/03/27/2984764.html)

若希望元素不跟随, 则设置 clear 属性

注意: clear 只影响元素本身,不能影响其他元素

float 布局参见 float布局学习.html

防止容器塌陷的方法:(从上到下越来越简单)
1. 设置容器的高度
2. 设置最后一个元素为清除浮动
3. 在文档最后添加一个高度为0 的空div清除浮动
4. 设置容器的 after 伪类为清除浮动
5. 设置属性 overflow
6. 设置属性 display: flow-root;