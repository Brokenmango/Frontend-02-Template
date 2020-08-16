学习笔记

# CSS 总论

## CSS语法的研究

winter的学习方法特别好，总是着眼于知识体系的骨架的建立，在css这里也不例外。建立的方式是通过从比较权威和具有完备性的源头来开始。

这里是从css 2.1开始整理它的整个语法。

css

- at-rules

  - @charset

  - @import

  - @media

  - @page

- rule

其中at-rules不是那么重要，最重要的都在rule（选择器加申明）中。

## at-规则的研究

除了上面的4个之外，还有几个较重要的

- @counter-style

- @keyframes

- @fontface

- @support

- @namespace

其中，@mediea, @keyframes, @fontface在最重要

## 规则

由选择器，声明构成。其中声明又分key和value。具体参看脑图。

## 收集标准

骚

第一次看到用前端js写的爬虫

# CSS的选择器

这里把css的选择器单拿出来详细介绍。总的来说winter不建议写太复杂的选择器，因为html是归我们控制的，我们可以通过多加一些class或者id来实现简单的元素选择。

## 选择器语法

- 简单选择器

  - *：星号，通用选择器，选中任何的元素

  - div：类型选择器，tagName选择器

  - .cls：class选择器

  - #id：id选择器

  - [attr=value]：属性选择器，可以包括上两种

  - :hover：以冒号开头的伪类选择器，大多来自交互等

  - ::before：伪元素选择器，选中一些原本不存在的元素。伪类和伪元素还会展开讲

- 复合选择器 (combined selector)

几个简单选择器以空格隔开就构成了一个复合选择器，要同时满足所有的简单选择器才能被复合选择器选中。所以它们之间是与的关系。

*或者div必须写在最前面，伪类必须写在最后面

- 复杂选择器

是复合选择器以一定的关系组合成的

  - <复合选择器><sp><复合选择器>：sp这里是space的意思，空格。这个是子孙选择器。即当前元素必须得有空格左边的父级节点或者祖先节点（父级的父级）

  - <复合选择器>">"<复合选择器>：父子选择器，左边元素必须是右边元素的直接父元素

  - <复合选择器>"~"<复合选择器>：邻接关系

  - <复合选择器>"+"<复合选择器>：邻接关系

  - <复合选择器>"||"<复合选择器>：做表格的时候，表示可以选中其中一个列。

## 选择器的优先级

之前讲过，如果作用在相同元素上有不同的选择器，那么按照优先级来确定渲染效果

对于简单选择器是

inline > id > class > tagName

对于复合选择器是把里面的简单选择器按权重计算出来，比如

#id div.a#id {

}

有2个#id，就是两个id选择器，有一个div，就是tagname选择器，一个.a，是class选择器，所以对应的数组是

[0,2,1,1]

s = 0 * n^3 + 2 * n^2 + 1 * n^1 + 1

假设取一个n = 1000000

那么结果 s = 2000001000001

在浏览器的实际工作中，要取一个足够大（体现优先级关系）又不是那么大（节省空间）的数，然后一般是十六进制。比如ie6取了0xff+1，之后的浏览器取了0xffff+1

> 更详细的优先级定义，[在level-3的文档中](https://www.w3.org/TR/selectors-3/#specificity)

A selector's specificity is calculated as follows:

- count the number of ID selectors in the selector (= a)

- count the number of class selectors, attributes selectors, and pseudo-classes in the selector (= b)

- count the number of type selectors and pseudo-elements in the selector (= c)

- ignore the universal selector

## 伪类（pseudo-classes）

和链接，行为相关的伪类，就是给早先的超链接设计出来的

- :any-link：匹配所有的超链接

- :link :visited：一个匹配的是没有访问过的超链接，后面的是匹配访问过的超链接。

- :hover

- :active

- :focus

- :target

树形结构相关的

- :empty：表示这个元素是否有子元素

- :nth-child()：这个元素是父元素的第几个child

- :nth-last-child()

- :first-child :last-child: only-child

逻辑型

- :not

- :where :has

## 伪元素（pseudo-elements）

常用的伪元素

- ::before

- ::after

表示在元素的内容的前或后插入一个伪元素。一旦应用了before和after的属性，declaration里面就可以写一个叫做content的属性。只要写了content属性，就像真正的dom元素一样参与到排版和渲染中。

通过选择器向界面上添加了不存在的元素

- ::first-line

- ::first-letter

用一个不存在的元素把一部分的文本括起来，然后对这部分文本进行格式控制

它们能修改的属性也不同

  - fist line

    - font系列, color系列, background系列, word-spacing, letter-spacing, text-decoration, text-transform, line-height

  - first letter

    - font系列, color系列, background系列, word-spacing, letter-spacing, text-decoration, text-transform, line-height, float, vertical-align, 盒模型系列: margin, padding, border

  - 为什么 first-letter 可以设置 float 之类的，而 first-line 不行呢？

  参考了网上一位同学的答案。说的主要是性能考虑。first-line的确定是根据计算布局之后的实际宽度选中的文字，如果加了float属性之后，每次都要再次计算布局，性能消耗比较大。而first-letter是确定的，可以直接参与到布局计算中，不会触发再次计算布局，性能消耗小。
