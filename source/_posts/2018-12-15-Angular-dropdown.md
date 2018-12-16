---
title: 2018-12-15-Angular-dropdown
date: 2018-12-15 17:06:49
categories: ['angular'] 
tags:
    - dropdown
    - Angular
---

### angualr 项目中 下拉菜单

来，跟我来，80行TS代码就可以搞定。

#### 第一步 分析标签结构
```ts
<ul class="nav navbar-nav navbar-right">
        <li class="dropdown" dropdown>
            <a dropdown-trigger><li class="fa fa-user-circle fa-2"></li> Admin</a>  
                <ul class="dropdown-menu  dropdown-menu-right">  
                    <li>
                        <a routerLink="sys/sysmonitor"><li class="fa fa-user-o fa-2"></li> Profile</a>
                    </li>
                    <li>
                        <a routerLink="sys/sysmonitor"><li class="fa fa-gear fa-2"></li> Settings</a>
                    </li>
                    <li>
                        <a routerLink="/login"><li class="fa fa-sign-out fa-2"></li> Logout</a>
                    </li>
                </ul>
        </li>
</ul>
```
- 文件中引用了Bootstrap定义的一些CSS样式。


- 很明显，下拉菜单是这样构成的：

![admin](/img/admin.png)

用来给鼠标点击的区域，这块区域一开始是可见的。
点击之后才会显示出来的部分，这块区域默认不可见，鼠标点了之后才显示。
#### 第二步 编写指令
根据上面的分析，我们分别写两个指令来封装对应的逻辑：

DropdownDirective，这个指令代表整个下拉菜单，很明显它一定会包含两个方法open()和close()
DropdownTriggerDirective，这个指令代表给鼠标点的那个按钮或者链接，鼠标点了之后，就把一开始隐藏的菜单显示出来。  
- 来看DropdownDirective的代码：
```ts
import { Directive, ElementRef, ContentChild, Output, EventEmitter, Input } from "@angular/core";

@Directive({
  selector: '[dropdown]',
  exportAs: 'dropdown'
})

export class DropdownDirective {
  @Input("dropdownToggle")
  public toggleClick: boolean = true;

  @Output()
  public onOpen = new EventEmitter<string>();

  @Output()
  public onClose = new EventEmitter<string>();

  constructor(private elementRef: ElementRef) { }

  open() {
    //这种操作HTML元素的方式还是很丑陋的，对吧？
    const element: HTMLElement = this.elementRef.nativeElement;
    element.classList.add("open");
    this.onOpen.emit("open");
  }

  close() {
    const element: HTMLElement = this.elementRef.nativeElement;
    element.classList.remove("open");
    this.onClose.emit("close");
  }

  isOpened(): boolean {
    const element: HTMLElement = this.elementRef.nativeElement;
    return element.classList.contains("open");
  }
}
```
- 再看DropdownTriggerDirective的代码：
```ts
import { Directive, ElementRef, OnDestroy, Host, HostListener } from "@angular/core";
import { DropdownDirective } from "./dropdown.directive";

@Directive({
    selector: '[dropdown-trigger]',
    exportAs: "dropdown-trigger"
})

export class DropdownTriggerDirective {

    private closeDropdownOnOutsideClick= (event: MouseEvent) => {this.closeIfInClosableZone(event)};

    constructor( @Host() public dropdown: DropdownDirective,
        private elementRef: ElementRef) {

    }

    open() {
        if (this.dropdown.isOpened())
            return;

        this.dropdown.open();
        document.addEventListener("click", this.closeDropdownOnOutsideClick, true);
    }

    close() {
        if (!this.dropdown.isOpened())
            return;

        this.dropdown.close();
        document.removeEventListener("click", this.closeDropdownOnOutsideClick, true);
    }

    toggle() {
        if (this.dropdown.isOpened()) {
            this.close();
        } else {
            this.open();
        }
    }

    @HostListener("click")
    openDropdown() {
        if (this.dropdown.isOpened() && this.dropdown.toggleClick) {
            this.close();
        } else {
            this.open();
        }
    }
```


> 如果点击的位置不在下拉菜单内部，则关闭下拉


```ts
    private closeIfInClosableZone(event: Event) {
        if (event.target !== this.elementRef.nativeElement
            && !this.elementRef.nativeElement.contains(event.target)) {
            this.dropdown.close();
            document.removeEventListener("click", this.closeDropdownOnOutsideClick, true);
        }
     }

     ngOnDestroy() {
        document.removeEventListener("click", this.closeDropdownOnOutsideClick, true);
     }
}

```


>去掉空行和注释，80行不到，耐心阅读一下，一点儿都不复杂，对吧？  


#### 第三步：使用指令
别忘记在你的模块定义里面导入你自己编写的指令，就像这样：

 ![directive](/img/dorpdown.png)

然后就可以在HTML标签里面使用这两个指令啦，来个复杂的，题图里面的菜单完整标签结构如下：



```ts
<ul class="nav navbar-nav navbar-right">
    <li class="dropdown" dropdown>
        <a dropdown-trigger><li class="fa fa-bars fa-2"></li> 库存管理</a>
        <ul class="dropdown-menu dropdown-menu-left">
            <li>
                <a routerLink="inventory/inventory-table/page/1">库存</a>
            </li>
            <li>
                <a routerLink="inventory/inbound-table/page/1">入库</a>
            </li>
            <li>
                <a routerLink="inventory/outbound-table/page/1">出库</a>
            </li>
            <li>
                <a routerLink="inventory/shift-table/page/1">移库</a>
            </li>
            <li>
                <a routerLink="inventory/loss-table/page/1">库损</a>
            </li>
        </ul>
    </li>
    <li class="dropdown" dropdown>
        <a dropdown-trigger><li class="fa fa-cogs fa-2"></li> 基础资料</a>
        <ul class="dropdown-menu  dropdown-menu-left">
            <li>
                <a routerLink="basic-data/warehouse-map">仓库地图</a>
            </li>
            <li>
                <a routerLink="basic-data/warehouse-table/page/1">仓库资料</a>
            </li>
            <li>
                <a routerLink="basic-data/category-table/page/1">类别资料</a>
            </li>
            <li>
                <a routerLink="basic-data/vendor-table/page/1">供应商资料</a>
            </li>
            <li>
                <a routerLink="basic-data/customer-table/page/1">客户资料</a>
            </li>
            <li>
                <a routerLink="basic-data/staff-table/page/1">员工资料</a>
            </li>
        </ul>
    </li>
    <li class="dropdown" dropdown>
        <a dropdown-trigger><li class="fa fa-area-chart fa-2"></li> 系统监控</a>
        <ul class="dropdown-menu  dropdown-menu-left">
            <li>
                <a routerLink="sys/sysmonitor">Echarts</a>
            </li>
            <li>
                <a routerLink="sys/sysmonitor">百度地图</a>
            </li>
        </ul>
    </li>
    <li class="dropdown" dropdown>
        <a dropdown-trigger><li class="fa fa-user-circle fa-2"></li> Admin</a>
        <ul class="dropdown-menu  dropdown-menu-right">
            <li>
                <a routerLink="sys/sysmonitor"><li class="fa fa-user-o fa-2"></li> Profile</a>
            </li>
            <li>
                <a routerLink="sys/sysmonitor"><li class="fa fa-gear fa-2"></li> Settings</a>
            </li>
            <li>
                <a routerLink="/login"><li class="fa fa-sign-out fa-2"></li> Logout</a>
            </li>
        </ul>
    </li>
</ul>
```

#### 小结
本篇以下拉菜单为例子，讲解了通过指令来写下拉菜单功能，学会Angular指令的玩法，注意掌握指令的基本用法。

