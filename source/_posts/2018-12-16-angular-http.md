---
layout: angular-http
title: Angular前后台数据交互
date: 2018-12-15 22:56:05
categories: ['angular'] 
tags:
     - dropdown
     - Angular
---

### 本文介绍angular http 数据交互的方式
1. Angular get 请求数据
2. Angular post 提交数据
3. Angular Jsonp 请求数据
4. Angular 中使用第三方模块axios请求数据
#### 一、Angular get 请求数据
Angualr5.x以后get、post和服务器交互使用的是HttpClientModule模块
##### 1、在app.module.ts中引入HttpClientModule 并注入
```
import {HttpClientModule} from '@angular/common/http';

imports:[
    BrowserModule,
    HttpClientModule
]
```
##### 2.在用到的地方引入HttpClient并在构造函数声明
 ```
import {HttpClient}from "@angular/common/http";

constructor(public http:httpClient){

}
```

##### 3、get 请求数据
```
   let api="https://api.ngclub.cn/api/booklists";
   this.http.get(api).subscribe(response)=>{
       
   }
   ```