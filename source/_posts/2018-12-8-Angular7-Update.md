---
layout:     post
title:      "Angular发布了最新版本Angular 7.0"
subtitle:   "Angular 7.0新功能"
date:       2018-12-8 23:10:00
author:     "dali"
header-img: "img/post-bg-nextgen-web-pwa.jpg"
header-mask: 0.3
catalog:    true
categories: ['angular'] 
tags:
    - 前端开发
    - Angular
---


## Angular发布了最新版本Angular 7.0
那么主要更新了哪些内容呢？我们一起来了解一下

### Angular 7.0中有什么新功能?



> 在创建新的Angular应用程序时，Angular CLI将提示用> 户选择是否要添加Angular路由等功能或者要在其应用程> 序中使用的样式表格式。
> 如果应用程序包大小超过预定义的限制，Angular 7.0应> 用程序将使用Angular CLI的Bundle Budget功能来警告> 开发人员。警告的默认值设置为2MB，错误的默认值为> > 5MB。此值是可配置的，可以从angular.json文件更改。> 此功能大大增强了应用程序性能。  

**Angular Material的 Component Dev Kit（CDK）更新了一些新功能。  
CDK的两个新增功能如下：**

#### 1.虚拟滚动

如果您尝试加载大量元素，则会影响应用程序性能。可用于仅加载屏幕上列表的可见部分。它只会渲染适合屏幕的项目。当用户滚动列表时，DOM将根据显示大小动态加载和卸载元素。不要将此功能与无限滚动相混淆，无限滚动完全是加载元素的不同策略。

- 虚拟滚动基于列表的可见部分从DOM中加载和卸载元素，使得有可能为拥有非常大的可滚动列表的用户构建非常快速的体验。  
![guidogn](/img/guidong.gif)
```ts

<cdk-virtual-scroll-viewport itemSize="50" class="example-viewport">
  <div *cdkVirtualFor="let item of items" class="example-item">{{item}}</div>
</cdk-virtual-scroll-viewport>
```
#### 2.拖放

我们可以轻松地为项目添加拖放功能。它支持诸如自由拖动元素，重新排序列表项，在列表之间移动项目，动画，添加自定义拖动手柄以及沿X或Y轴限制拖动等功能。 

![tuofang](/img/tuofang.gif)

- CDK现在支持拖放功能，并且包括当用户移动元素时的自动渲染、用于列表重新排序( moveItemInArray )和在列表之间移动元素( transferrarrayitem)的辅助方法。

```ts
<div cdkDropList class="list" (cdkDropListDropped)="drop($event)">
  <div class="box" *ngFor="let movie of movies" cdkDrag>{{movie}}</div>
</div>
```
```ts
drop(event: CdkDragDrop<string[]>) {
    moveItemInArray(this.movies, event.previousIndex, event.currentIndex);
}
```
- mat-form-field现在将支持使用本机select元素。这将为应用程序提供增强的性能和可用性。

- Angular 7.0已更新其依赖项以支持TypeScript 3.1，RxJS 6.3和Node 10。

#### Angular Elements
> Angular Elements现在支持对自定义元素使用web标准进行内容投影。

```ts 
<my-custom-element>This content can be projected!</my-custom-element>
```
### 如何更新到v7
> -访问update.angular.io以获取有关更新应用程序的详细信息和指导，更新到v7只需要一个命令：
```
>> ng update @angular/cli @angular/core  
```
v7版本早期使用者报告说，升级速度比以往任何时候都快，许多应用程序的升级时间不到10分钟。

> CLI提示
现在，CLI将在运行诸如ng new或ng add @angular/material之类的常用命令时提示用户，以帮助你发现CLI内置的路由或支持SCSS等功能。

### 依赖更新
更新了对主要第三方项目的依赖。
```
TypeScript 3.1  
RxJS 6.3  
Node 10 — 增加了对Node 10的支持，
并且仍然支持  Node 8  
```
