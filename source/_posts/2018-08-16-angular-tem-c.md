---
title:      "Angular-模版介绍及应用"
date:       2018-09-18 12:00:00
author:     "dali"
catalog:    true
categories: ['angular'] 
tags:
    - Angular
    - 前端
    
---



## 组件：模板


> 模板是编写 Angular 组件最重要的一环，你至少需要深入理解以下知识点才能玩转 Angular 模板：  
> 对比各种 JS 模板引擎的设计思路  
> Mustache（八字胡）语法  
> 模板内的局部变量  
> 属性绑定、事件绑定、双向绑定  
> 在模板里面使用结构型指令 *ngIf、*ngFor、ngSwitch  
> 在模板里面使用属性型指令 NgClass、NgStyle、NgModel  
> 在模板里面使用管道格式化数据  
- [ ] mustache 
- [ ] 模版内局部变量 
- [ ] 属性绑定 事件绑定  双向绑定
- [ ] 在模版里使用属性指令
- [ ] NgClass,NgStyle,NgModel
-  [] 结构型指令  
Ngif,NgFor NgSwitch ,
在模版里 使用管道化格式数据

- mustache 语法  
他可以获取到组件里定义的属性值  
可以自动获得 简单表达式的计算值  
可以获取方法的返回值

- 举个例子 
- 插值语法关键代码实例：


```
<h3>
    欢迎来到{{title}}！
</h3>
```
public title = '假的星际争霸2'; 
简单的数学表达式求值：
```
<h3>1+1={{1+1}}</h3>
```
调用组件里面定义的方法：

```<h3>可以调用方法{{getVal()}}</h3>```  
public getVal():any{  
    return 65535;  
}  
模板内的局部变量
```
<input #heroInput>
<p>{{heroInput.value}}</p>
``` 
有一些朋友会追问，如果我在模板里面定义的局部变量和组件内部的属性重名会怎么样呢？

如果真的出现了重名，Angular 会按照以下优先级来进行处理：

模板局部变量 > 指令中的同名变量 > 组件中的同名属性

- 属性绑定是用方括号来做的，写法：

<img [src]="imgSrc"/>  
public imgsrc:string="../../../.jpg";

 - 事件绑定

<button  class="btn btn-success" (click)="btnClick($event)">测试事件</button>

public btnClick(event):void{
    alter("测试事件绑定！");
}

- 双向数据绑定

双向绑定


<font-resizer [(size)]="fontsizePx" ></font-resizer>

对应组件内部的定义

public fontsizePx:number=14;  

AngularJS 是第一个把“双向数据绑定”这个特性带到前端来的框架，这也是 AngularJS 当年最受开发者追捧的特性，之一。  

根据 AngularJS 团队当年讲的故事，“双向数据绑定”这个特性可以大幅度压缩前端代码的规模，一个绑定表达式就搞定。目前，主流的几款前端框架都已经接受了“双向数据绑定”这个特性


- 在模版里使用结构型指令

angualr 内置三个结构性指令 1.NgIf 2.NgFor 3.NgSwitch  


```ts
<p *ngIf="isshow"  style="background-color:#e3f2f0">ngif 测试是否显示</p>



<btton btn btn-success (Click)="toggleShow()">控制显示还是隐藏</button>

```
```ts
public isShow:boolean='true';
 
public toggleShow():void{
    this.isShow=!this.isShow;
}  
```

- Ngfor 实例
 ```ts
  <li *ngFor="let reace of reaces,let i=index;">
{{i+1}}-{{reace.name}}
</li>



public reaces:Arreay<any>=[
   {name:"人族"},
   {name:"虫族"},
   {name:"兽族"},
   {name:"神族"},
]，
```

```ts
- ngswitch
 <div [ngSwitch]="mapStatus">
<p ngSwitchcase="0"> 开始下载。。。</p>
<p ngSwitchcase="1"> 下载中。。。</p>
<p ngSwitchcase="2">下载完毕。。。 </p>
</div>


public mapStatus:number="1";
```
特别注意：一个 HTML 标签上只能同时使用一个结构型的指令。

因为“结构型”指令会修改 DOM 结构，如果在一个标签上使用多个结构型指令，大家都一起去修改 DOM 结构，到时候到底谁说了算？

那么需要在同一个 HTML 上使用多个结构型指令应该怎么办呢？有两个办法：

加一层空的 div 标签
加一层<ng-container>

- ### 在模版里使用 属性型指令
 使用频率较高的3个内置指令是：NgClass,NgStyle,NgModel.
 
 1.NgClass案例使用代码：
  ```ts
<div [ngClass]="currentClass"> 同时设置多个样式</div>
<button (click)="setCurrentsClass">设置</button>


public currentClass:{}
// 属性是否显示
public canSave: boolean = true;
public isUnchanged: boolean = true;
public isSpecial: boolean = true;

setCurrentsClass(){
   this.currentClass{
        'saveable': this.canSave,
        'modified': this.isUnchanged,
        'special': this.isSpecial
   }
}


.saveable{
    font-size: 18px;
} 
.modified {
    font-weight: bold;
}
.special{
    background-color: #ff3300;
}
 ```
 
 ```ts
 
 NgStyle 使用案例代码：

<div [ngStyle]="currentStyles">
    用NgStyle批量修改内联样式！
</div>
<button class="btn btn-success" (click)="setCurrentStyles()">设置</button>
public currentStyles: {}
public canSave:boolean=false;
public isUnchanged:boolean=false;
public isSpecial:boolean=false;

setCurrentStyles() {
    this.currentStyles = {
        'font-style':  this.canSave      ? 'italic' : 'normal',
        'font-weight': !this.isUnchanged ? 'bold'   : 'normal',
        'font-size':   this.isSpecial    ? '36px'   : '12px'
    };
}

```
ngStyle 这种方式相当于在代码里面写 CSS 样式，比较丑陋，违反了注意点分离的原则，而且将来不太好修改，非常不建议这样写。

```ts

<p class="text-danger">ngModel只能用在表单类的元素上面</p>
    <input [(ngModel)]="currentRace.name">
<p>{{currentRace.name}}</p>

public currentRace:any{
    name:"悟空"
}

```

请注意，如果你需要使用 NgModel 来进行双向数据绑定，必须要在对应的模块里面 import FormsModule
- 管道

管道的一个典型作用是用来格式化数据，来一个最简单的例子：
```ts
{{currentTime | date:'yyyy-MM-dd HH:mm:ss'}}
public currentTime: Date = new Date();
```
Angular里面一共内置了12个管道：

