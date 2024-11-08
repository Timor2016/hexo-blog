---
tags:
  - harmony
  - study
title: 鸿蒙page页UI描述
categories: harmony
date: '2024-11-06 22:22'
abbrlink: 43b8754a
---
>说明：摘抄自[创建自定义组件](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides-V5/arkts-create-custom-components-V5),仅作快速了解。就是一些规则，需要了解。
## ArkTS的基本组成
![image.png](https://gitee.com/wc2017/blog-img/raw/master/20241106/171244861-20241106171240-52a92.png)
- 装饰器： 用于装饰类、结构、方法以及变量，并赋予其特殊的含义。如上述示例中@Entry、@Component和@State都是装饰器，@Component表示自定义组件，@Entry表示该自定义组件为入口组件，@State表示组件中的状态变量，状态变量变化会触发UI刷新。
其他的瞄一眼就知道啥意思了
## 创建组件
根据组件构造方法的不同，创建组件包含有参数和无参数两种方式。
### 无参数
如果组件的接口定义没有包含必选构造参数，则组件后面的“()”不需要配置任何内容。
```
Column() {
  Text('item 1')
  Divider()
  Text('item 2')
}
```
### 有参数
如果组件的接口定义包含构造参数，则在组件后面的“()”需要配置相应参数。
```
Image('https://xyz/test.jpg')
```
## 配置属性
属性方法以“.”链式调用的方式配置系统组件的样式和其他属性，建议每个属性方法单独写一行。
```
Text('hello')
  .fontSize(this.size)
Image('test.jpg')
  .width(this.count % 2 === 0 ? 100 : 200)    
  .height(this.offset + 100)
```
## 配置事件
事件方法以“.”链式调用的方式配置系统组件支持的事件，建议每个事件方法单独写一行。
- 使用箭头函数表达式配置组件的事件方法，要求使用“() => {...}”，以确保函数与组件绑定，同时符合ArkTS语法规范

	```
		Button('add counter').onClick(() => {
		    this.counter += 2;})
	```
- 使用组件的成员函数配置组件的事件方法，需要bind this。ArkTS语法不推荐使用成员函数配合bind this去配置组件的事件方法。

	```
		myClickHandler(): void {
		  this.counter += 2;}
			...
		Button('add counter')
		  .onClick(this.myClickHandler.bind(this))
	```
- 使用声明的箭头函数，可以直接调用，不需要bind this。

	```
		fn = () => {
		  console.info(`counter: ${this.counter}`)
		  this.counter++
		  }
		...
		Button('add counter')
		  .onClick(this.fn)
	```

## 配置子组件
如果组件支持子组件配置，则需在尾随闭包"{...}"中为组件添加子组件的UI描述。Column、Row、Stack、Grid、List等组件都是容器组件。
以下是简单的Column组件配置子组件的示例。
```
Column() {
  Text('Hello')
    .fontSize(100)
  Divider()
  Text(this.myText)
    .fontSize(100)
    .fontColor(Color.Red)
}
```
容器组件均支持子组件配置，可以实现相对复杂的多级嵌套。
```
Column() {
  Row() {
    Image('test1.jpg')
      .width(100)
      .height(100)
    Button('click +1')
      .onClick(() => {
        console.info('+1 clicked!');
      })
  }
}
```
## 自定义组件
```
@Component
struct HelloComponent {
  @State message: string = 'Hello, World!';

  build() {
    // HelloComponent自定义组件组合系统组件Row和Text
    Row() {
      Text(this.message)
        .onClick(() => {
          // 状态变量message的改变驱动UI刷新，UI从'Hello, World!'刷新为'Hello, ArkUI!'
          this.message = 'Hello, ArkUI!';
        })
    }
  }
}
```
简单的自定义其实就是各个组件的组合。瞄一眼就知道怎么回事了
### 自定义组件的基本结构
- struct：自定义组件基于struct实现，struct + 自定义组件名 + {...}的组合构成自定义组件，不能有继承关系。对于struct的实例化，可以省略new。
>[!tip]  说明
>自定义组件名、类名、函数名不能和系统组件名相
- @Component：@Component装饰器仅能装饰struct关键字声明的数据结构。struct被@Component装饰后具备组件化的能力，需要实现build方法描述UI，一个struct只能被一个@Component装饰。@Component可以接受一个可选的bool类型参数。
	**freezeWhenInactive** 组件冻结选项，未UI性能设计的，有些情况下，状态变量绑定了多个UI组件，其变化可能触发大量UI组件的刷新，进而导致界面卡顿和响应延迟。
	启用后，系统将仅对处于激活状态的自定义组件进行更新，这使得UI框架可以尽量缩小更新范围，仅限于用户可见范围内（激活状态）的自定义组件，从而提高复杂UI场景下的刷新效率。
	当之前处于inactive状态的自定义组件重新变为active状态时，状态管理框架会对其执行必要的刷新操作，确保UI的正确展示。
	组件active/inactive并不等同于其可见性。组件冻结目前仅适用于以下场景：
	1. 页面路由：当前栈顶页面为active，非栈顶不可见页面为inactive。
	2. TabContent：只有当前显示的TabContent中的自定义组件处于active状态，其余则为inactive。
	3. LazyForEach：仅当前显示的LazyForEach中的自定义组件为active，而缓存节点的组件则为inactive。
	4. Navigation：当前显示的NavDestination中的自定义组件为active，而其他未显示的NavDestination组件则为inactive。
	5. 其他场景，如堆叠布局（Stack）下的被遮罩的组件，这些组件尽管不可见，但并不被视为inactive状态，因此不在组件冻结的适用范围内。
- build()函数：build()函数用于定义自定义组件的声明式UI描述，自定义组件必须定义build()函数。
- @Entry：@Entry装饰的自定义组件将作为UI页面的入口。在单个UI页面中，最多可以使用@Entry装饰一个自定义组件。@Entry可以接受一个可选的LocalStorage的参数。
	![img_v3_02gc_5f46abdb-2b70-41c7-bf40-6d41bc3e59hu.jpg](https://gitee.com/wc2017/blog-img/raw/master/20241106/174918885-20241106174912-3bedb.png)
	```
		@Entry({ routeName : 'myPage' })
		@Component
		struct MyComponent {
		}
	```
- @Reusable：@Reusable装饰的自定义组件具备可复用能力
### 成员函数/变量
自定义组件除了必须要实现build()函数外，还可以实现其他成员函数，成员函数具有以下约束：
- 自定义组件的成员函数为私有的，且不建议声明成静态函数。
自定义组件可以包含成员变量，成员变量具有以下约束：
- 自定义组件的成员变量为私有的，且不建议声明成静态变量。
- 自定义组件的成员变量本地初始化有些是可选的，有些是必选的。
### 自定义组件的参数规定
在创建自定义组件的过程中，根据装饰器的规则来初始化自定义组件的参数。
```
@Entry
@Component
struct Parent {
  @State cnt: number = 0
  submit: () => void = () => {
    this.cnt++;
  }

  build() {
    Column() {
      Text(`${this.cnt}`)
      Son({ submitArrow: this.submit })
    }
  }
}

@Component
struct Son {
  submitArrow?: () => void

  build() {
    Row() {
      Button('add')
        .width(80)
        .onClick(() => {
          if (this.submitArrow) {
            this.submitArrow()
          }
        })
    }
    .justifyContent(FlexAlign.SpaceBetween)
    .height(56)
  }
}
```
可以瞄一眼
###  build()函数
所有声明在build()函数的语句，我们统称为UI描述，UI描述需要遵循以下规则：
- @Entry装饰的自定义组件，其build()函数下的根节点唯一且必要，且必须为容器组件，其中ForEach禁止作为根节点。
- @Component装饰的自定义组件，其build()函数下的根节点唯一且必要，可以为非容器组件，其中ForEach禁止作为根节点。
- 不允许声明本地变量，反例如下。
	```
		build() {
		  // 反例：不允许声明本地变量
		  let a: number = 1;
		}
	```
- 不允许在UI描述里直接使用console.info，但允许在方法或者函数里使用，反例如下。
	```
		build() {
		  // 反例：不允许console.info
		  console.info('print debug log');
		}
	```
- 不允许创建本地的作用域，反例如下。
	```
		build() {
		  // 反例：不允许本地作用域
		  {
			...
		  }
		}
	```
- 不允许调用没有用@Builder装饰的方法，允许系统组件的参数是TS方法的返回值。
	```
		@Component
		struct ParentComponent {
		  doSomeCalculations() {
		  }

		  calcTextValue(): string {
		    return 'Hello World';
		  }

		  @Builder doSomeRender() {
		    Text(`Hello World`)
		  }

		  build() {
		    Column() {
		      // 反例：不能调用没有用@Builder装饰的方法
		      this.doSomeCalculations();
		      // 正例：可以调用
		      this.doSomeRender();
		      // 正例：参数可以为调用TS方法的返回值
		      Text(this.calcTextValue())
		    }
		  }
		}
	```
- 不允许使用switch语法，如果需要使用条件判断，请使用if。示例如下：
	```
		build() {
		  Column() {
		    // 反例：不允许使用switch语法
		    switch (expression) {
		      case 1:
		        Text('...')
		        break;
		      case 2:
		        Image('...')
		        break;
		      default:
		        Text('...')
		        break;
		    }
		    // 正例：使用if
		    if(expression == 1) {
		      Text('...')
		    } else if(expression == 2) {
		      Image('...')
		    } else {
		      Text('...')
		    }
		  }
		}
	```
- 不允许使用表达式，反例如下。
	```
		build() {
		  Column() {
		    // 反例：不允许使用表达式
		    (this.aVar > 10) ? Text('...') : Image('...')
		  }
		}
	```
- 不允许直接改变状态变量，反例如下:
	```
		@Component
		struct CompA {
		  @State col1: Color = Color.Yellow;
		  @State col2: Color = Color.Green;
		  @State count: number = 1;
		  build() {
		    Column() {
		      // 应避免直接在Text组件内改变count的值
		      Text(`${this.count++}`)
		        .width(50)
		        .height(50)
		        .fontColor(this.col1)
		        .onClick(() => {
		          this.col2 = Color.Red;
		        })
		      Button("change col1").onClick(() =>{
		        this.col1 = Color.Pink;
		      })
		    }
		    .backgroundColor(this.col2)
		  }
		}
	```
	