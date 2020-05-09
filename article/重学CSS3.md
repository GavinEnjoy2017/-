# CSS选择器
## 浏览器前缀
- Chrome和safari **-webkit**
- firefox **-moz**
- IE **-ms**
- opera **-o**

## 选择器
- 通配符选择器 *
- 标签选择器
- 类选择器
- ID选择器
- 属性选择器

属性选择器 | 属性描述
---|---
[att] | 所有带att属性的元素
[att = value] |属性为value的元素
[att~=value] | 包含value的元素
[att^=value] | 以value开头的元素
[att$=value] | 以value结尾的元素
[att*=value] | 包含value中的每个字符
[att|=value] | 以value开头的元素
- 文档结构选择器
 
结构选择器 | 描述
---|---
ul li | 后代选择器
ul > li | 子选择器
ul + li | 相邻兄弟选择器
ul ~ li | 一般兄弟选择器
ul > li | 子选择器
- 伪类选择器

伪类选择器 | 描述
---|---
:root | 文档根元素伪类
:nth-child(n) | 孩子选择器
:nth-of-type(n) | 同类型的第N个元素
:first-child | 第一个子元素
:last-child | 最后一个子元素
:first-of-type | 同类型的第一个元素
:last-of-type | 同类型得到最后一个元素
:only-child | 唯一一个子元素
:empty | 没有子元素
:nth-last-child(n) | 倒数第几个元素
:nth-last-of-type(n) | 倒数同类型的第几个元素
:only-of-type | 同类型唯一一个子元素
a:link | 没有访问过的状态
a:active | 正在访问过的状态
a:hover | 鼠标位于其上的链接
a:visited | 所有已经被访问的状态
a:enabled/disabled | 选择被启用或者禁用的状态
:checked | 选择被选中的元素
:not() | 选择非selector元素的元素
- 伪元素选择器

伪元素选择器 | 描述
---|---
::first-line | 第一行的状态
::first-letter | 第一个字母的状态
::before | 元素之前的内容
::selection | 元素被选中的内容


## 样式的继承
- CSS的某些样式是可以继承的， 例如： P标签下的Color，但是border不可以继承

## 选择器的优先级
### 优先级
!important > 内联样式 > ID选择器 > 类选择器 > 标签选择器 > 通配符选择器

### 权重
**! important 不管权重如何都会取important的值**

选择器 | 权重
---|---
1，0，0，0 | 内联样式
0，1，0，0 | ID选择器
0，0，1，0 | 类选择器，伪类选择器， 属性选择器
0，0，0，1 | 标签， 伪元素选择器
0，0，0，0 | 通配，子选择器，相邻选择器，兄弟选择器


---
# 样式
## 字体样式
- font-family 字体类型
- font-size 字体大小
- font-weight 字体粗细
- font-style 字体样式
- color 字体颜色
- font样式的简写，空格分隔，size/height用/分开 例如：font:italic  bold  12px/1.5em  "宋体",sans-serif

## 文本样式

- text-decoration

> - none，标准的文本
> - underline， 定义文本下一条线
> - overline，定义文本上的一条线
> - line-through，定义文本中的一条线，类似于删除线

- text-indent,为文本添加首行缩进
- line-height，为文本设置行间据
- letter-spacing, 增加字符间的空白
- text-align, 设置文本的对齐方式

## 块级元素和行内元素
##### 块级元素
单独占据一行， div, P
##### 行内元素
会在一行显示， span, a 
##### 转换
- display：block, 转换为块级元素
- display: inline, 转换为行内元素
- display: inline-block, 同时具备块级元素和行内元素的特征，同在一行，并且具备高度和宽度等
- display: none,隐藏元素

##### 小技巧
-  text-align：center，水平居中，仅对行内元素有用
-  margin-left:auto;margin-right:auto; 块级元素水平居中
-  定宽高垂直水平居中， 父元素relative, 子元素absolute， left top各自50%
-  不定长居中

```
 .box {
    border: 1px solid #00ee00;
    height: 300px;
    position: relative;
}

.box1 {
    border: 1px solid red;
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
}
```


## 背景色
background-color

## 盒子模型

##### content
对于非替换元素如div,其content就是div内部的元素

##### padding
内边距，参与高度的计算

##### border
边框
> border-bottom,设置底部边框
> border-radius,设置边框圆角

##### margin
外边距，不会参与高度的计算

---
# 布局模型
## 流动模型
默认得到网页布局模式，块级元素自上而下布局，内联元素自左向右排列

## 浮动模型
float:left, 块级元素浮动排列

## 层模型
- 绝对定位 position: absolute
> 将元素从文档流中脱离出来， 使用left, right, bottom, top进行定位，相对于其最接近的一个具有定位属性的父包含块进行绝对定位，如果不存在这样的包含块，则相对于body元素，即相对于浏览器窗口

- 相对定位 position: relative
> 通过left、right、top、bottom属性确定元素在正常文档流中的偏移位置。相对定位完成的过程是首先按static(float)方式生成一个元素(并且元素像层一样浮动了起来)，然后相对于以前的位置移动，移动的方向和幅度由left、right、top、bottom属性确定，偏移前的位置保留不动

- 固定定位 position: fixed
> absolute定位类型类似，但它的相对移动的坐标是视图（屏幕内的网页窗口）本身。由于视图本身是固定的，它不会随浏览器窗口的滚动条滚动而变化，除非你在屏幕中移动浏览器窗口的屏幕位置，或改变浏览器窗口的显示大小，因此固定定位的元素会始终位于浏览器窗口内视图的某个位置，不会受文档流动影响，这与background-attachment:fixed;属性功能相同。以下代码可以实现相对于浏览器视图向右移动100px，向下移动50px。并且拖动滚动条时位置固定不变

- Relative与Absolute组合使用
> absolute相对于浏览器窗口定位，如果父元素定位为relative，则会相对于父元素定位

## 弹性盒子模型
[30 分钟学会 Flex 布局](https://zhuanlan.zhihu.com/p/25303493)
- flex容器

> display: flex | inline-flex, 如果你使用块元素如 div，你就可以使用 flex，而如果你使用行内元素，你可以使用 inline-flex，**需要注意的是：当时设置 flex 布局之后，子元素的 float、clear、vertical-align 的属性将会失效**

- flex-direction: 决定主轴的方向

> row | row-reverse | column | column-reverse, row，主轴为水平方向，起点在左端

> row-reverse：主轴为水平方向，起点在右端

> column：主轴为垂直方向，起点在上沿

> column-reverse：主轴为垂直方向，起点在下沿

- flex-wrap: 决定容器内项目是否可换行

> flex-wrap: nowrap | wrap | wrap-reverse;

> 默认值：nowrap 不换行，即当主轴尺寸固定时，当空间不足时，项目尺寸会随之调整而并不会挤到下一行

> wrap：项目主轴总尺寸超出容器时换行，第一行在上方

> wrap-reverse：换行，第一行在下方

- flex-flow: flex-direction 和 flex-wrap 的简写形式

> 默认值为: row nowrap

- justify-content：定义了项目在主轴的对齐方式

> justify-content: flex-start | flex-end | center | space-between | space-around

> 默认值: flex-start 左对齐

> flex-end：右对齐

> center：居中

> space-between：两端对齐，项目之间的间隔相等，即剩余空间等分成间隙

> space-around：每个项目两侧的间隔相等，所以项目之间的间隔比项目与边缘的间隔大一倍

- align-items: 定义了项目在交叉轴上的对齐方式

>  align-items: flex-start | flex-end | center | baseline | stretch;

> 默认值为 stretch 即如果项目未设置高度或者设为 auto，将占满整个容器的高度, 假设容器高度设置为 100px，而项目都没有设置高度的情况下，则项目的高度也为 100px

> flex-start：交叉轴的起点对齐

> flex-end：交叉轴的终点对齐

> center：交叉轴的中点对齐

> baseline: 项目的第一行文字的基线对齐

- align-content: 定义了多根轴线的对齐方式，如果项目只有一根轴线，那么该属性将不起作用

>  align-content: flex-start | flex-end | center | space-between | space-around | stretch;

> 默认值为 stretch, 占满整个容器的高度

> flex-start：轴线全部在交叉轴上的起点对齐

> flex-end：轴线全部在交叉轴上的终点对齐

> center：轴线全部在交叉轴上的中间对齐

> space-between：轴线两端对齐，之间的间隔相等，即剩余空间等分成间隙

> space-around：每个轴线两侧的间隔相等，所以轴线之间的间隔比轴线与边缘的间隔大一倍

- order: 定义项目在容器中的排列顺序，数值越小，排列越靠前，默认值为 0
- flex-basis: 定义了在分配多余空间之前，项目占据的主轴空间，浏览器根据这个属性，计算主轴是否有多余空间

> 默认值：auto，即项目本来的大小, 这时候 item 的宽高取决于 width 或 height 的值, **当主轴为水平方向的时候，当设置了 flex-basis，项目的宽度设置值会失效，flex-basis 需要跟 flex-grow 和 flex-shrink 配合使用才能发挥效果**
- flex-grow: 定义项目的放大比例

>  当所有的项目都以 flex-basis 的值进行排列后，仍有剩余空间，那么这时候 flex-grow 就会发挥作用了。
如果所有项目的 flex-grow 属性都为 1，则它们将等分剩余空间。(如果有的话)

> 如果一个项目的 flex-grow 属性为 2，其他项目都为 1，则前者占据的剩余空间将比其他项多一倍。

> 当然如果当所有项目以 flex-basis 的值排列完后发现空间不够了，且 flex-wrap：nowrap 时，此时 flex-grow 则不起作用了，这时候就需要接下来的这个属性

- flex-shrink: 定义了项目的缩小比例

> 默认值: 1，即如果空间不足，该项目将缩小，负值对该属性无效

> 如果所有项目的 flex-shrink 属性都为 1，当空间不足时，都将等比例缩小。

> 如果一个项目的 flex-shrink 属性为 0，其他项目都为 1，则空间不足时，前者不缩小

- flex: flex-grow, flex-shrink 和 flex-basis的简写

> auto (1 1 auto) 和 none (0 0 auto)

> 当 flex 取值为一个非负数字，则该数字为 flex-grow 值，flex-shrink 取 1，flex-basis 取 0%

> 当 flex 取值为 0 时，对应的三个值分别为 0 1 0%

> 当 flex 取值为一个长度或百分比，则视为 flex-basis 值，flex-grow 取 1，flex-shrink 取 1，有如下等同情况（注意 0% 是一个百分比而不是一个非负数字）

> 当 flex 取值为两个非负数字，则分别视为 flex-grow 和 flex-shrink 的值，flex-basis 取 0%，如下是等同的

> 当 flex 取值为一个非负数字和一个长度或百分比，则分别视为 flex-grow 和 flex-basis 的值，flex-shrink 取 1，如下是等同的

> grow 和 shrink 是一对双胞胎，grow 表示伸张因子，shrink 表示是收缩因子

- align-self: 允许单个项目有与其他项目不一样的对齐方式

> 默认值为 auto，表示继承父元素的 align-items 属性，如果没有父元素，则等同于 stretch

> 这个跟 align-items 属性时一样的，只不过 align-self 是对单个项目生效的，而 align-items 则是对容器下的所有项目生效的

**[CSS经典布局](https://juejin.im/post/5bbcd7ff5188255c80668028)**

**[CSS经典三栏布局](https://github.com/ljianshu/Blog/issues/14)**









