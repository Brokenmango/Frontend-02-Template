学习笔记

# css中文字与排版相关属性

## 盒模型（box）

### 盒的由来

首先介绍三个概念，由此来介绍盒的由来

标签：标签存在于源代码，有开始标签，结束标签，自封闭标签。一对起止标签表示一个元素

元素：元素是语义概念，是不存在于源代码中的。dom树中最主要的就是元素（element），当然准确的说dom树中包含的是节点（node），节点包括有元素（element）和其他节点，如文本节点（text）等。css选择器选中了一个元素，在排版是可能产生多个盒。

盒：盒是个表现的概念。是排版和渲染的基本单位。跟元素是一对多的关系。即一个元素可能产生多个盒。比如一个属性是inline的元素在分行的时候可能产生多个盒。

### 盒的结构

盒的结构就是个由盒子似的几个长方形嵌套而成。最里面的长方形是content（内容），可以通过content-box属性设置。外面接着一圈padding（内边距），然后再接着一圈border（边框），border本身是可以有厚度的，由border框住的长方形可以由border-box属性来设置。border外面还圈了个margin（外边距）。由此组成完整的box（盒）

从内到位

content -> padding -> border -> margin

内容 -》 内边框 -》边框 -》 外边框

## 正常流（normal flow）

### 介绍

是第一代排版技术，之后的有flex，grid等排版技术。其中flex当主要学习。

正常流来源于一般的文字排版

正常流排版的主要步骤是

- 收集盒和文字进行

- 计算盒在行中的排布（行内）

- 计算行的排布（行间）

其中有两个概念，一个是line level box，这个是跟文字混排在一行。一个是block level box，单独占一行。line level box从左到右排。block level box从上到下排。

所以正常流就可以细分为下面两类

IFC(Line level formatting context)

BFC(Block level formatting context)

### 行内排布

行内的话主要是由五条线构成，从上到下分别为

- line top

- text top

- base line

- text bottom

- line bottom

其中文字的排布主要看base line和text top，text bottom。而inline box的尺寸会影响line top和line bottom的位置。

vertical-align这个属性可以用来对齐其中的某条线。align这个词就是对齐的意思。

### 块级排布（也可理解为行间排布）

这里举了两个实例来演示块级排布

#### float与clear

float：它实依附于正常流的排布方式，先把有float属性的元素当作正常流的元素排列到页面的某个位置，然后根据float的值往某个方向去济。最后调整行盒的宽度。

clear：找一个干净的空间去执行float。是配合float一起使用的一个属性。

#### margin折叠（边距折叠）

这个现象只发生在正常流的bfc中，意思是两个块的上下边距不会等于他俩的和，而是等于他俩的最大值。

### BFC合并

略

## Flex

flex排版的规则

- 收集盒进行

- 计算盒在主轴方向的排布

- 计算盒在交叉轴方向的排布

分行

- 根据主轴尺寸，把元素分进行

- 若设置了no-wrap，则强行分配进第一行

计算主轴方向

- 找出所有flex元素

- 把主轴方向的剩余尺寸按比例分配给这些元素

- 若剩余元素空间为负数，所有flex元素为0，等比压缩剩余元素

计算交叉轴方向

- 根据每一行中最大元素尺寸计算行高

- 根据行高flex-align和item-align，确定元素具体位置

## 动画（animation）

介绍了用@keyframes和animation制作动画，同时介绍了cubic-bezier曲线，它是来控制timing function的

## 颜色

介绍了几个颜色模型，包括rgb，cmyk，hsl与hsv

## 绘制

主要讲了三类的绘制

- 几何图形

  - border

  - box-shadow

  - border-radius

- 文字

  - font

  - text-decoration

位图

  - background-image




