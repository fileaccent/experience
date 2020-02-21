### flex 布局
局限对于一行的横向元素排列非常有用,多行就有些乏力

#### 总述:

采用Flex布局的元素，称为Flex容器（flex container），简称”容器”。

它的所有子元素自动成为容器成员，称为Flex项目（flex item），简称”项目”。

![](http://www.runoob.com/wp-content/uploads/2015/07/3791e575c48b3698be6a94ae1dbff79d.png)

main axis 为水平的主轴

main start 为主轴开始

main end 为主轴结束

cross axis 为垂直的主轴

cross start 为垂直轴开始

cross end 为垂直轴结束

### 容器的属性:

flex-direction

flex-wrap

flex-flow

justify-content

align-items

align-content

#### flex-direction 属性

row（默认值）：主轴为水平方向，起点在左端。
row-reverse：主轴为水平方向，起点在右端。
column：主轴为垂直方向，起点在上沿。
column-reverse：主轴为垂直方向，起点在下沿。

#### flex-wrap 属性

nowrap（默认值）：不换行。
wrap：换行，第一行在上方。
wrap-reverse：换行，第一行在下方。

#### flex-flow 属性 (为上述两种的结合)

默认值为 row nowrap

#### justify-content 属性

flex-start（默认值）：左对齐

flex-end：右对齐

center： 居中

space-between：两端对齐，项目之间的间隔都相等。

space-around：每个项目两侧的间隔相等。所以，项目之间的间隔比项目与边框的间隔大一倍。

#### align-items 属性 (如果是单行的话,用这个)

flex-start：交叉轴的起点对齐。

flex-end：交叉轴的终点对齐。

center：交叉轴的中点对齐。

baseline: 项目的第一行文字的基线对齐。

stretch（默认值）：如果项目未设置高度或设为auto，将占满整个容器的高度。

![](http://www.runoob.com/wp-content/uploads/2015/07/2b0c39c7e7a80d5a784c8c2ca63cde17.png)

#### align-content 属性(多行用这个)

align-content属性定义了多根轴线的对齐方式。如果项目只有一根轴线，该属性不起作用。

flex-start：与交叉轴的起点对齐。

flex-end：与交叉轴的终点对齐。

center：与交叉轴的中点对齐。

space-between：与交叉轴两端对齐，轴线之间的间隔平均分布。

space-around：每根轴线两侧的间隔都相等。所以，轴线之间的间隔比轴线与边框的间隔大一倍。

stretch（默认值）：轴线占满整个交叉轴。

![](http://www.runoob.com/wp-content/uploads/2015/07/f10918ccb8a13247c9d47715a2bd2c33.png)

### 项目的属性

#### order 属性

order属性定义项目的排列顺序。数值越小，排列越靠前，默认为0。

#### flex-grow 属性

flex-grow属性定义项目的放大比例，默认为0，即如果存在剩余空间，也不放大。

如果所有项目的flex-grow属性都为1，则它们将等分剩余空间（如果有的话）。　　

如果一个项目的flex-grow属性为2，其他项目都为1，则前者占据的剩余空间将比其他项多一倍。

#### flex-shrink 属性

flex-shrink属性定义了项目的缩小比例，默认为1，即如果空间不足，该项目将缩小。

如果所有项目的flex-shrink属性都为1，当空间不足时，都将等比例缩小。

如果一个项目的flex-shrink属性为0，其他项目都为1，则空间不足时，前者不缩小。

　　负值对该属性无效.

#### flex-basis 属性

flex-basis属性定义了在分配多余空间之前，项目占据的主轴空间（main size）。

浏览器根据这个属性，计算主轴是否有多余空间。它的默认值为auto，即项目的本来大小。

它可以设为跟width或height属性一样的值（比如350px），则项目将占据固定空间。

#### flex 属性 (上述三种的结合)

默认值有两个:

auto(1 1 auto)

none(0 0 auto)

#### align-self 属性

align-self属性允许单个项目有与其他项目不一样的对齐方式，可覆盖align-items属性。

默认值为auto，表示继承父元素的align-items属性，如果没有父元素，则等同于stretch。

flex-start：交叉轴的起点对齐。

flex-end：交叉轴的终点对齐。

center：交叉轴的中点对齐。

baseline: 项目的第一行文字的基线对齐。

stretch（默认值）：如果项目未设置高度或设为auto，将占满整个容器的高度。


![](http://www.runoob.com/wp-content/uploads/2015/07/55b19171b8b6b9487d717bf2ecbba6de.png)