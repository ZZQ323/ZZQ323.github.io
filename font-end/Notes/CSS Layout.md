# 【Notes】LayOut All in One

[**flex 布局的基本概念：MDN**](https://developer.mozilla.org/zh-CN/docs/Web/CSS/CSS_flexible_box_layout/Basic_concepts_of_flexbox)

# abstract

- 为什么说FlexBox是一维的呢？

# Flex Box

## Model Summary

Flex模型主要有两根轴线可以选：`row` 和 `column`；写上是什么哪个就是主轴。

`flex-direction` 定义主轴，`reverse` 则会导致反向排布，你同时还可以使用`order`进行排序。

`flex-basis` 的设置会优先于 `width` 以及 `height` 的设置；

起始线和终止线条：现代的布局方式涵盖了书写模式 `writing-mode` ，所以我们不再假设一行文字是从文档的左上角开始向右书写（样例：英文与阿拉伯文）。

<img title="" src="https://developer.mozilla.org/zh-CN/docs/Web/CSS/CSS_flexible_box_layout/Basic_concepts_of_flexbox/basics5.svg" alt="书写英文时，主轴的起始线是左边" width="398" data-align="center">

<img title="" src="https://developer.mozilla.org/zh-CN/docs/Web/CSS/CSS_flexible_box_layout/Basic_concepts_of_flexbox/basics6.svg" alt="书写阿拉伯文时，主轴的起始线是右边" width="397" data-align="center">



`flex` 属性分别是：`flex-grow`、`flex-shrink`、`flex-basis`

    特殊的写法有：`flex:auto`、`flex:2`

    理解：`flex` 设置的属性就是说明每个盒子的“弹性”

`flex-flow` 属性分别是：`flex-direction`、`flex-wrap`

    理解：`flex-flow`属性就是为了说明，整个flex盒子里面的元素是怎么流动的（flow）。

布局肯定会涉及到对齐，其中的内容就有：

- [ ] `align-item`、`align-self`：交叉轴对齐

- [ ] `align-content`：多条主轴的，交叉轴对齐

- [ ] `justify-content`、`justify-self`：主轴项目对齐

- [ ] `margin:auto`：



以及参数：

（`flex-`）`start`、（`flex-`）`end`、`stretch`、`center`、`baseline`、`fist baseline` 、`last baseline`



因为盒子只有一个维度，如果盒子过宽，或者我们想要一个多列的布局（使得整体上更加紧凑），那么我们就需要 wrap 来创建新行。



## 【问题】对齐效果理解

vscode



## 【问题】文本方向

[direction - CSS：层叠样式表 | MDN](https://developer.mozilla.org/zh-CN/docs/Web/CSS/direction)

[unicode-bidi - CSS：层叠样式表 | MDN](https://developer.mozilla.org/zh-CN/docs/Web/CSS/unicode-bidi)

[writing-mode - CSS：层叠样式表 | MDN](https://developer.mozilla.org/zh-CN/docs/Web/CSS/writing-mode)

以及 inline 元素的断行问题





# Grid Layout