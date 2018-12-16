---
title: Angular-Pipe 管道的介绍及应用
date: 2018-12-01 16:05:45
categories: ['angular'] 
catalog: true
tags:
    - Angular
    - Pipe
---


### Angular 中 Pipe
> Angular 中 Pipe（管道） 与 Angular 1.x 中的 filter（过滤器）的作用的是一样的。它们都是用来对输  入的数据进行处理，如大小写转换、数值和日期格式  化等。

``` html
<div>
   <p ngNonBindable>{{ lo | repeat:3 }}</p>
   <p>{{ lo | repeat:3 }}</p> <!-- Output: lololo -->
</div>
```


- 大写转换

``` html
<div>
  <p ngNonBindable>{{ Angular | uppercase }}</p>
  <p>{{ Angular | uppercase }}</p> <!-- Output: ANGULAR -->
</div>
```

``` html
<div>
  <p ngNonBindable>{{ Angular | lowercase }}</p>
  <p>{{ Angular | lowercase }}</p> <!-- Output: angular -->
</div>
```
- 数值格式化  
``` 
<div>
  <p ngNonBindable>{{ 3.14159265 | number: 1.4-4 }}</p>
  <p>{{ 3.14159265 | number: 1.4-4}}</p> <!-- Output: 3.1416 -->
</div>
```

- 日期格式化  
``` html
<div>
  <p ngNonBindable>{{ today | date:shortTime }}</p>
  <p>{{ today | date: 'shortTime' }}</p> <!-- Output: 以当前时间为准，输出格式：10:40 AM -->
</div>  
```

- JavaScript 对象序列化  



- 对象转换  

``` 
 <!-- object: {[key: number]: string} = {2: 'foo', 1: 'bar'}; -->
<div *ngFor="let item of object | keyvalue">
   {{item.key}}: {{item.value}} 
</div>  
```

- 管道参数  
管道可以接收任意数量的参数，使用方式是在管道名称后面添加 : 和参数值。如 number: '1.4-4' ，  
若需要传递多个参数则参数之间用冒号隔开，具体示例如下：  

```   
<div>
   <p ngNonBindable>{{ lo | repeat:3 }}</p>
   <p>{{ 'lo' | repeat:3 }}</p> <!-- Output: lololo -->
</div>  
```

#### 内建管道及分类
String -> String  
UpperCasePipe  
LowerCasePipe  
TitleCasePipe  
Number -> String  
DecimalPipe  
PercentPipe  
CurrencyPipe  
Object -> String  
JsonPipe  
DatePipe  
Tools  
KeyValuePipe（v6.1.0）  
SlicePipe  
AsyncPipe  
I18nPluralPipe  
I18nSelectPipe 

#### 内建管道使用示例 

#### 自定义管道
- 自定义管道的步骤：

> 使用 @Pipe 装饰器定义 Pipe 的 metadata 信息，如 Pipe 的名称 - 即 name 属性
实现 PipeTransform 接口中定义的 transform 方法
- WelcomePipe 定义  

- WelcomePipe 使用

- 当 WelcomePipe 的输入参数，即 value 值为非字符串时，如使用 123，则控制台将会抛出以下异常：


> EXCEPTION: Error in ./AppComponent class AppComponent caused by: Invalid pipe argument for WelcomePipe

- RepeatPipe 定义

- RepeatPipe 使用

#### 管道分类
-  pure 管道：仅当管道输入值变化的时候，才执行转换操作，默认的类型是 pure 类型。（备注：输入值变化是指原始数据类型如：string、number、boolean 等的数值或对象的引用值发生变化）。  
- impure 管道：在每次变化检测期间都会执行，如鼠标点击或移动都会执行 impure 管道。  
### 总结
> 本文介绍了 Angular 中的常用内建管道的用法和管道的分类，同时也介绍了 pure 和 impure 管道的区别。 此外我们通过两个示例展示了如何自定义管道，最后详细分析了 RepeatPipe 管道的工作原理。
