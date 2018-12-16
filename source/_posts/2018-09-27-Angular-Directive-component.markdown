---
layout:     post
title:      "Angular有了指令为什么还要组件"
subtitle:   "Component & Directive"
date:       2018-09-28 23:10:00
author:     "dali"
header-img: "img/post-bg-nextgen-web-pwa.jpg"
header-mask: 0.3
catalog:    true
categories: ['es6'] 
tags:
    - 前端开发
    - Angular
---
### Angular有了指令为什么还要组件


- 指令和组件之间的关系
- 有了指令为什么还要组件
- 
![image](/img/com-dir.png)


再看一下核心源代码里面的内容  
![directive](/img/directives.png)

#### 很明显，Component是Directive的子接口。

> 根据Angular官方文档的描述，Angular里面有3种类型的指令：

- Component是Directive的子接口，是一种特殊的指令，Component可以带有HTML模板，Directive不能有模板
- 属性型指令：用来修改DOM元素的外观和行为，但是不会改变DOM结构，Angular内置指令里面典型的属性型指令有ngClass、ngStyle。如果你打算封装自己的组件库，属性型指令是必备的内容。
- 结构型指令：可以修改DOM结构，内置的常用结构型指令有*ngFor、*ngIf和NgSwitch。由于结构型指令会修改DOM结构，所以同一个HTML标签上面不能同时使用多个结构型指令，否则大家都来改DOM结构，到底听谁的呢？如果要在同一个HTML元素上面使用多个结构性指令，可以考虑加一层空的元素来嵌套，比如在外面套一层空的<ng-container></ng-container>，或者套一层空的<div>
#### 有了组件为什么还要指令？


- 根本原因是：我们需要用指令来增强标签的功能，包括HTML原生标签和你自己自定义的标签。

举例来说：<div>是一个常用的原生HTML标签，但是请不要小看它，它上面实际上有非常多的属性，这些属性都是W3C规范规定好的：
[w3c div 32个属性列表](https://www.w3schools.com/tags/ref_standardattributes.asp/)


- 但是，这些内置属性还不够用，你想给原生的HTML标签再扩展一些属性。比方说：你想给```<div>```标签增加一个自定义的属性叫做```my-high-light```，当鼠标进入```div```内部时，```div```的背景就会高亮显示，可以这样使用```<div my-high-light>``` 

- 这时候，没有指令机制就无法实现了。

#### 总结
- 总结：“指令”是一个非常精妙的设计，利用它可以无入侵地扩展原生HTML的Attribute(属性)。
---
- 以我自己的观点来看，“指令”在Angular里面的重要性不亚于你们当年热捧的“双向数据绑定”。

