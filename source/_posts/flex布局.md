---
layout: pages
title: flex布局
date: 2020-02-20 22:30:34
categories: "css"
tags: ["css","flex"]
---

# Flex布局是什么
Flex 是 Flexible Box 的缩写，意为弹性盒子；

为容器指定为一个Flex布局:
```css
.box{
    display:flex
}
```
行内元素指定为Flex布局
```css
.box{
  display: inline-flex;
}
```

# 举一个简单例子
![Image text](/images/flex.jpg)



HTMLM
```html
<div class="body-flex">
    <div class="header">header</div>
    <div class="con">
        <div class="left">left</div>
        <div class="center">center</div>
        <div class="right">right</div>
    </div>
    <div class="footer">footer</div>
</div>
```
CSS
```css
.body-flex{
    display: flex;
    height:100vh;
    flex-direction: column;
    text-align: center;  
}
.body-flex .header{
    line-height: 60px;
    height:60px;
    background: #eee;
}
.body-flex .con{
    flex:1;
    display: flex;
    line-height: 60px;    
}
.body-flex .con .left{
    width:150px;
    background: #e2dada;
}
.body-flex .con .center{
    flex:1;
    background:rgb(207, 188, 188);
}
.body-flex .con .right{
    width:150px;
    background: #e2dada;
}
.body-flex .footer{
    line-height: 60px;
    height:60px;
    background: #eee;
}
```

# 外容器Flex属性
```css
    flex-direction
    flex-wrap
    flex-flow
    justify-content
    align-items
    align-content
```

## flex-direction
`flex-direction`属性决定主轴的方向（即项目的排列方向）
```css
.box {
  flex-direction: row | row-reverse | column | column-reverse; /* 默认为row */
}
```
## flex-wrap
`flex-wrap`属性决定在一条轴上排列不下时，如何换行
```css
.box {
  flex-wrap: nowrap | wrap | wrap-reverse; /* 默认为nowrap */
}
```
## flex-flow
`flex-flow`属性是`flex-direction`属性和`flex-wrap`属性的简写形式，默认值为`row nowrap`
```css
.box {
  flex-flow: <flex-direction>  <flex-wrap>;
}
```
## justify-content
`justify-content`属性定义了盒子在主轴上的对齐方式;(内盒子宽度不够外盒子宽度时)
```css
.box {
  justify-content: flex-start | flex-end | center | space-between | space-around | space-evenly;
}
```
```css
justify-content:flex-start; /* （默认值）：内盒子相对外盒子左对齐； */
justify-content:flex-end; /* 内盒子相对外盒子右对齐； */
justify-content:center ; /* 内盒子相对外盒子居中，相当于margin: 0 auto; */
justify-content:space-between; /* 内盒子两端对齐，内盒子之间的间隔都相等； */
justify-content:space-around; /* 内盒子两侧的间隔相等，于是内盒子之间的间隔比最边的盒子间隔大一倍。 */
justify-content:space-evenly；/* 每个盒子的间隔均匀分布 */
```

## align-items
`align-items`属性定义项目在交叉轴上如何对齐。
```css
.box {
  align-items: flex-start | flex-end | center | baseline | stretch;
}
```
```css
align-items:stretch（默认值）;  /* 如果项目未设置高度或设为auto，将占满整个容器的高度。 */
align-items:flex-start; /* 如果内盒子设置高度，设置此属性则交叉轴的起点对齐。 */
align-items:flex-end;   /* 如果内盒子设置高度，设置此属性则交叉轴的终点对齐。 */
align-items:center; /* 如果内盒子设置高度，设置此属性则交叉轴的中点对齐。 */
align-items:baseline;   /* 如果内盒子设置高度，设置此属性则项目的第一行文字的基线对齐。 */
```
## align-content
`align-content`属性定义了多根轴线的对齐方式。如果项目只有一根轴线，该属性不起作用。
```css
.box {
  align-content: flex-start | flex-end | center | space-between | space-around | stretch;
}
```
```css
align-content:stretch（默认值）; /* 轴线占满整个交叉轴。 */
align-content:flex-start; /* 内盒子与交叉轴的起点对齐。 */
align-content:flex-end; /* 内盒子与交叉轴的终点对齐。 */
align-content:center; /* 内盒子与交叉轴的中点对齐。 */
align-content:space-between; /* 内盒子与交叉轴两端对齐，轴线之间的间隔平均分布。 */
align-content:space-around; /* 每根轴线两侧的间隔都相等。所以，轴线之间的间隔比轴线与边框的间隔大一倍。 */
```
# 内盒子属性
```css
    order
    flex-grow
    flex-shrink
    flex-basis
    flex
    align-self
```
## order
`order`属性定义内盒子的排列顺序，数值越小，排列越向前，默认为0，为数值；
```css
.item{
    order: <number>;/* default 0 */
}
```
## flex-grow
`flex-grow`属性定义内盒子的放大比例，即存在剩余空间则自动平分，默认为0，即不扩充盒子大小;
```css
.item {
  flex-grow: <number>; /* default 0 */
}
```
## flex-shrink
`flex-shrink`属性定义盒子的缩小比例，即空间不足时自动缩小当前盒子大小，默认为1，即如果空间不足，该项目将缩小。
```css
.item {
  flex-shrink: <number>; /* default 1 */
}
```
## flex-basis
`flex-basis`属性定义了在分配多余空间之前，项目占据的主轴空间（main size）。浏览器根据这个属性，计算主轴是否有多余空间。它的默认值为auto，即项目的本来大小,可跟设置宽度高度一样设置；
```css
.item {
  flex-basis: <length> | auto; /* default auto */
}
```

## flex
`flex`属性是flex-grow, flex-shrink 和 flex-basis的简写，默认值为0 1 auto。后两个属性可选。
```css
.item {
  flex: none | [ <'flex-grow'> <'flex-shrink'>? || <'flex-basis'> ]
}
```
## align-self
`align-self`属性允许单个项目有与其他项目不一样的对齐方式，可覆盖`align-items`属性。默认值为auto，表示继承父元素的`align-items`属性，如果没有父元素，则等同于`stretch`。
```css
.item {
  align-self: auto | flex-start | flex-end | center | baseline | stretch;
}
```

