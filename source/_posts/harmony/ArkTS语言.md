---
tags:
  - harmony
  - study
title: ArkTS语言
categories: harmony
date: '2024-11-06 22:11'
abbrlink: 86c57a0
---
>说明：摘抄自[华为的ArkTS语言介绍](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides-V5/introduction-to-arkts-V5),仅作快。如果有Java、kotlin、js语言基础的话，很容易上手
# 声明
**变量**
以关键字let开头的声明引入变量，该变量在程序执行期间可以具有不同的值。
```
let hi: string = 'hello';
hi = 'hello, world';
```
**常量**
以关键字const开头的声明引入只读常量，该常量只能被赋值一次。
```
const hello: string = 'hello';
```
**自动类型推断**
由于ArkTS是一种静态类型语言，所有数据的类型都必须在编译时确定。但是，如果一个变量或常量的声明包含了初始值，那么开发者就不需要显式指定其类型。
```
let hi1: string = 'hello';
let hi2 = 'hello, world';
```
# 数据类型
**Number类型**
ArkTS提供number和Number类型，任何整数和浮点数都可以被赋给此类型的变量。
数字字面量包括整数字面量和十进制浮点数字面量。
整数字面量包括以下类别：
- 由数字序列组成的十进制整数
- 以0x（或0X）开头的十六进制整数
- 以0o（或0O）开头的八进制整数
- 以0b（或0B）开头的二进制整数
浮点字面量包括以下：
- 十进制整数，可为有符号数（即，前缀为“+”或“-”）
-  小数点（“.”）
- 小数部分
- 以“e”或“E”开头的指数部分
**Boolean类型**
**String类型**
字符串字面量由单引号（'）或双引号（"）之间括起来的零个或多个字符组成。字符串字面量还有一特殊形式，是用反向单引号（\`）括起来的模板字面量。
**Void类型**
void类型用于指定函数没有返回值。
此类型只有一个值，同样是void。由于void是引用类型，因此它可以用于泛型类型参数。
```
class Class<T> {
	//...
}
let instance: Class <void>
```
**Object类型**
Object类型是所有引用类型的基类型。任何值，包括基本类型的值（它们会被自动装箱），都可以直接被赋给Object类型的变量。
**Array类型**
**Enum类型**
**Union类型**
union类型，即联合类型，是由多个类型组合成的引用类型。联合类型包含了变量可能的所有类型。
```
class Cat {
	name: string = 'cat';
	// ...
}
class Dog {
	name: string = 'dog';
	// ...
}
class Frog {
	name: string = 'frog';
// ...
}
type Animal = Cat | Dog | Frog | number;
// Cat、Dog、Frog是一些类型（类或接口）

let animal: Animal = new Cat();
animal = new Frog();
animal = 42;
// 可以将类型为联合类型的变量赋值为任何组成类型的有效值
```
可以用不同的机制获取联合类型中特定类型的值。
```
class Cat { sleep () {}; meow () {} }
class Dog { sleep () {}; bark () {} }
class Frog { sleep () {}; leap () {} }

type Animal = Cat | Dog | Frog;

function foo(animal: Animal) {
	if (animal instanceof Frog) {
		animal.leap(); // animal在这里是Frog类型
	}
	animal.sleep(); // Animal具有sleep方法
}
```
**Aliases类型**
Aliases类型为匿名类型（数组、函数、对象字面量或联合类型）提供名称，或为已有类型提供替代名称。
```
type Matrix = number[][];
type Handler = (s: string, no: number) => string;
type Predicate <T> = (x: T) => boolean;
type NullableObject = Object | null;
```
# 运算符
1. **比较运算符**
		![image.png](https://gitee.com/wc2017/blog-img/raw/master/20241105/174347808-20241105174340-9b22c.png)
2. **算术运算符**
	![image.png](https://gitee.com/wc2017/blog-img/raw/master/20241105/174624379-20241105174619-ad14b.png)
3. **位运算符**
	![image.png](https://gitee.com/wc2017/blog-img/raw/master/20241105/174800399-20241105174753-6f93a.png)
4. **逻辑运算符**
	![image.png](https://gitee.com/wc2017/blog-img/raw/master/20241105/174836761-20241105174832-0c840.png)
# 语句
**If语句**
**Switch语句**
**条件表达式**
条件表达式由第一个表达式的布尔值来决定返回其它两个表达式中的哪一个。
```
condition ? expression1 : expression2
```
**For语句**
**For-of语句**
使用for-of语句可遍历数组或字符串。示例如下：
```
for (forVar of expression) {
	statements
}
```
**While语句**
**Do-while语句**
**Break语句**
使用break语句可以终止循环语句或switch。
如果break语句后带有标识符，则将控制流转移到该标识符所包含的语句块之外。
```
let x = 1;
label: while (true) {
	switch (x) {
	case 1:
		// statements
		break label; // 中断while语句
	}
}
```
**Continue语句**
continue语句会停止当前循环迭代的执行，并将控制传递给下一个迭代。
**Throw和Try语句**
throw语句用于抛出异常或错误：
```
throw new Error('this error')
```
try语句用于捕获和处理异常或错误：
```
try {
/	/ 可能发生异常的语句块
} catch (e) {
	// 异常处理
}
```
# 函数
## 函数声明
函数声明引入一个函数，包含其名称、参数列表、返回类型和函数体。
```
function add(x: string, y: string): string {
	let z: string = `${x} ${y}`;
	return z;
}
```
在函数声明中，必须为每个参数标记类型。如果参数为可选参数，那么允许在调用函数时省略该参数。函数的最后一个参数可以是rest参数。
### 可选参数
可选参数的格式可为name?: Type。
```
function hello(name?: string) {
	if (name == undefined) {
		console.log('Hello!');
	} else {
		console.log(`Hello, ${name}!`);
	}
}
```
可选参数的另一种形式为设置的参数默认值。如果在函数调用中这个参数被省略了，则会使用此参数的默认值作为实参。
```
function multiply(n: number, coeff: number = 2): number {
	return n * coeff;
}
multiply(2); // 返回2*2
multiply(2, 3); // 返回2*3
```
### Rest参数
函数的最后一个参数可以是rest参数。使用rest参数时，允许函数或方法接受任意数量的实参。
```
function sum(...numbers: number[]): number {
	let res = 0;
	for (let n of numbers)
	res += n;
	return res;
}

sum(); // 返回0
sum(1, 2, 3); // 返回6
```
### 返回类型
如果可以从函数体内推断出函数返回类型，则可在函数声明中省略标注返回类型。
```
// 显式指定返回类型
function foo(): string { return 'foo'; }

// 推断返回类型为string
function goo() { return 'goo'; }
```
不需要返回值的函数的返回类型可以显式指定为void或省略标注。这类函数不需要返回语句
```
function hi1() { console.log('hi'); }
function hi2(): void { console.log('hi'); }
```
## 函数的作用域
函数中定义的变量和其他实例仅可以在函数内部访问，不能从外部访问。
如果函数中定义的变量与外部作用域中已有实例同名，则函数内的局部变量定义将覆盖外部定义。
## 函数调用
调用函数以执行其函数体，实参值会赋值给函数的形参。
```
function join(x: string, y: string): string {
	let z: string = `${x} ${y}`;
	return z;
}

let x = join('hello', 'world');
console.log(x);
```
## 函数类型
函数类型通常用于定义回调：
```
type trigFunc = (x: number) => number // 这是一个函数类型

function do_action(f: trigFunc) {
f(3.141592653589); // 调用函数
}

do_action(Math.sin); // 将函数作为参数传入
```
## 箭头函数（又名Lambda函数）
函数可以定义为箭头函数，例如：
```
let sum = (x: number, y: number): number => {
  return x + y;
}
```
箭头函数的返回类型可以省略；省略时，返回类型通过函数体推断。

## 闭包
闭包是由函数及声明该函数的环境组合而成的。该环境包含了这个闭包创建时作用域内的任何局部变量。
在下例中，f函数返回了一个闭包，它捕获了count变量，每次调用z，count的值会被保留并递增。
```
function f(): () => number {
  let count = 0;
  let g = (): number => { count++; return count; };
  return g;
}

let z = f();
z(); // 返回：1
z(); // 返回：2
```
## 函数重载
我们可以通过编写重载，指定函数的不同调用方式。具体方法为，为同一个函数写入多个同名但签名不同的函数头，函数实现紧随其后。
```
function foo(x: number): void;            /* 第一个函数定义 */
function foo(x: string): void;            /* 第二个函数定义 */
function foo(x: number | string): void {  /* 函数实现 */
}

foo(123);     //  OK，使用第一个定义
foo('aa'); // OK，使用第二个定义
```
# 类
类声明引入一个新类型，并定义其字段、方法和构造函数。
```
class Person {
  name: string = '';
  surname: string = '';
  constructor (n: string, sn: string) {
    this.name = n;
    this.surname = sn;
  }
  fullName(): string {
    return this.name + ' ' + this.surname;
  }
}
```
定义类后，可以使用关键字new创建实例：
```
let p = new Person('John', 'Smith');
console.log(p.fullName());
```
或者，可以使用对象字面量创建实例：
```
class Point {
  x: number = 0;
  y: number = 0;
}
let p: Point = {x: 42, y: 42};
```
## 字段
**实例字段**
实例字段存在于类的每个实例上。每个实例都有自己的实例字段集合。
**静态字段**
使用关键字static将字段声明为静态。静态字段属于类本身，类的所有实例共享一个静态字段
**字段初始化**
ArkTS要求所有字段在声明时或者构造函数中显式初始化
**getter和setter**
setter和getter可用于提供对对象属性的受控访问。
```
class Person {
  name: string = '';
  private _age: number = 0;
  get age(): number { return this._age; }
  set age(x: number) {
    if (x < 0) {
      throw Error('Invalid age argument');
    }
    this._age = x;
  }
}

let p = new Person();
p.age; // 输出0
p.age = -42; // 设置无效age值会抛出错误
```
## 方法
方法属于类。类可以定义实例方法或者静态方法。静态方法属于类本身，只能访问静态字段。而实例方法既可以访问静态字段，也可以访问实例字段，包括类的私有字段。
**实例方法**
```
class RectangleSize {
  private height: number = 0;
  private width: number = 0;
  constructor(height: number, width: number) {
    this.height = height;
    this.width = width;
  }
  calculateArea(): number {
    return this.height * this.width;
  }
}
```
**静态方法**
```
class Cl {
  static staticMethod(): string {
    return 'this is a static method.';
  }
}
console.log(Cl.staticMethod());
```
## 继承
一个类可以继承另一个类（称为基类），并使用以下语法实现多个接口：
```
class [extends BaseClassName] [implements listOfInterfaces] {
  // ...
}
```
继承类继承基类的字段和方法，但不继承构造函数。继承类可以新增定义字段和方法，也可以覆盖其基类定义的方法。

基类也称为“父类”或“超类”。继承类也称为“派生类”或“子类”。
**父类访问**
关键字super可用于访问父类的实例字段、实例方法和构造函数。在实现子类功能时，可以通过该关键字从父类中获取所需接口
**方法重写**
子类可以重写其父类中定义的方法的实现。重写的方法必须具有与原始方法相同的参数类型和相同或派生的返回类型。
**方法重载签名**
通过重载签名，指定方法的不同调用。具体方法为，为同一个方法写入多个同名但签名不同的方法头，方法实现紧随其后。
```
class C {
  foo(x: number): void;            /* 第一个签名 */
  foo(x: string): void;            /* 第二个签名 */
  foo(x: number | string): void {  /* 实现签名 */
  }
}
let c = new C();
c.foo(123);     // OK，使用第一个签名
c.foo('aa'); // OK，使用第二个签名
```
## 构造函数
类声明可以包含用于初始化对象状态的构造函数。
```
constructor ([parameters]) {
  // ...
}
```
如果未定义构造函数，则会自动创建具有空参数列表的默认构造函数，
**派生类的构造函数**
构造函数函数体的第一条语句可以使用关键字super来显式调用直接父类的构造函数。
```
class RectangleSize {
  constructor(width: number, height: number) {
    // ...
  }
}
class Square extends RectangleSize {
  constructor(side: number) {
    super(side, side);
  }
}
```
**构造函数重载签名**
## 可见性修饰符
可见性修饰符包括：private、protected和public
## 对象字面量
对象字面量是一个表达式，可用于创建类实例并提供一些初始值。它在某些情况下更方便，可以用来代替new表达式。
```
class C {
  n: number = 0;
  s: string = '';
}

let c: C = {n: 42, s: 'foo'};
```
ArkTS是静态类型语言，如上述示例所示，对象字面量只能在可以推导出该字面量类型的上下文中使用。其他正确的例子：
```
class C {
  n: number = 0;
  s: string = '';
}

function foo(c: C) {}

let c: C

c = {n: 42, s: 'foo'};  // 使用变量的类型
foo({n: 42, s: 'foo'}); // 使用参数的类型

function bar(): C {
  return {n: 42, s: 'foo'}; // 使用返回类型
}
```
也可以在数组元素类型或类字段类型中使用
```
class C {
  n: number = 0;
  s: string = '';
}
let cc: C[] = [{n: 1, s: 'a'}, {n: 2, s: 'b'}];
```
**Record类型的对象字面量**
泛型Record<K, V>用于将类型（键类型）的属性映射到另一个类型（值类型）。常用对象字面量来初始化该类型的值：
```
let map: Record<string, number> = {
  'John': 25,
  'Mary': 21,
}

map['John']; // 25


interface PersonInfo {
  age: number;
  salary: number;
}
let map: Record<string, PersonInfo> = {
  'John': { age: 25, salary: 10},
  'Mary': { age: 21, salary: 20}
}

```
# 接口
任何一个类的实例只要实现了特定接口，就可以通过该接口实现多态。
```
// 接口：
interface AreaSize {
  calculateAreaSize(): number; // 方法的声明
  someMethod(): void;     // 方法的声明
}

// 实现：
class RectangleSize implements AreaSize {
  private width: number = 0;
  private height: number = 0;
  someMethod(): void {
    console.log('someMethod called');
  }
  calculateAreaSize(): number {
    this.someMethod(); // 调用另一个方法并返回结果
    return this.width * this.height;
  }
}
```
## 接口属性
接口属性可以是字段、getter、setter或getter和setter组合的形式。
属性字段只是getter/setter对的便捷写法。以下表达方式是等价的：
```
interface Style {
  color: string;
}

interface Style {
  get color(): string;
  set color(x: string);
}
```
实现接口的类也可以使用以下两种方式:
```
interface Style {
  color: string;
}

class StyledRectangle implements Style {
  color: string = '';
}


class StyledRectangle implements Style {
  private _color: string = '';
  get color(): string { return this._color; }
  set color(x: string) { this._color = x; }
}
```

## 接口继承
接口可以继承其他接口
```
interface Style {
  color: string;
}

interface ExtendedStyle extends Style {
  width: number;
}
```
# 泛型类型和函数
泛型类型和函数允许创建的代码在各种类型上运行，而不仅支持单一类型。
## 泛型类和接口
```
class CustomStack<Element> {
  public push(e: Element):void {
    // ...
  }
}
```
## 泛型约束
```
interface Hashable {
  hash(): number;
}
class MyHashMap<Key extends Hashable, Value> {
  public set(k: Key, v: Value) {
    let h = k.hash();
    // ...其他代码...
  }
}
```
## 泛型函数
```
function last<T>(x: T[]): T {
  return x[x.length - 1];
}
```
## 泛型默认值
泛型类型的类型参数可以设置默认值。这样可以不指定实际的类型实参，而只使用泛型类型名称。
```
class SomeType {}
interface Interface <T1 = SomeType> { }
class Base <T2 = SomeType> { }
class Derived1 extends Base implements Interface { }
// Derived1在语义上等价于Derived2
class Derived2 extends Base<SomeType> implements Interface<SomeType> { }

function foo<T = number>(): T {
  // ...
}
foo();
// 此函数在语义上等价于下面的调用
foo<number>();
```
# 空安全
默认情况下，ArkTS中的所有类型都是不可为空的.
可以为空值的变量定义为联合类型T | null。
```
let x: number | null = null;
x = 1;    // ok
x = null; // ok
if (x != null) { /* do something */ }
```
## 非空断言运算符
后缀运算符!可用于断言其操作数为非空.
```
class A {
  value: number = 0;
}

function foo(a: A | null) {
  a.value;   // 编译时错误：无法访问可空值的属性
  a!.value;  // 编译通过，如果运行时a的值非空，可以访问到a的属性；如果运行时a的值为空，则发生运行时异常
}
```
## 空值合并运算符
空值合并二元运算符??用于检查左侧表达式的求值是否等于null或者undefined。如果是，则表达式的结果为右侧表达式；否则，结果为左侧表达式。
换句话说，a ?? b等价于三元运算符(a != null && a != undefined) ? a : b。
## 可选链
在访问对象属性时，如果该属性是undefined或者null，可选链运算符会返回undefined。
```
class Person {
  nick: string | null = null;
  spouse?: Person

  setSpouse(spouse: Person): void {
    this.spouse = spouse;
  }

  getSpouseNick(): string | null | undefined {
    return this.spouse?.nick;
  }

  constructor(nick: string) {
    this.nick = nick;
    this.spouse = undefined;
  }
}
```
>[!tip] 说明
>getSpouseNick的返回类型必须为string | null | undefined，因为该方法可能返回null或者undefined。

可选链可以任意长，可以包含任意数量的?.运算符。

# 模块
程序可划分为多组编译单元或模块。

每个模块都有其自己的作用域，即，在模块中创建的任何声明（变量、函数、类等）在该模块之外都不可见，除非它们被显式导出。

与此相对，从另一个模块导出的变量、函数、类、接口等必须首先导入到模块中。

## 导出
可以使用关键字export导出顶层的声明。未导出的声明名称被视为私有名称，只能在声明该名称的模块中使用。
```
export class Point {
  x: number = 0;
  y: number = 0;
  constructor(x: number, y: number) {
    this.x = x;
    this.y = y;
  }
}
export let Origin = new Point(0, 0);
export function Distance(p1: Point, p2: Point): number {
  return Math.sqrt((p2.x - p1.x) * (p2.x - p1.x) + (p2.y - p1.y) * (p2.y - p1.y));
}
```
## 导入
### 静态导入
导入声明用于导入从其他模块导出的实体，并在当前模块中提供其绑定。导入声明由两部分组成：
- 导入路径，用于指定导入的模块；
- 导入绑定，用于定义导入的模块中的可用实体集和使用形式（限定或不限定使用）。
导入绑定可以有几种形式。
假设模块具有路径“./utils”和导出实体“X”和“Y”。
导入绑定* as A表示绑定名称“A”，通过A.name可访问从导入路径指定的模块导出的所有实体：
```
import * as Utils from './utils'
Utils.X // 表示来自Utils的X
Utils.Y // 表示来自Utils的Y
```
导入绑定{ ident1, ..., identN }表示将导出的实体与指定名称绑定，该名称可以用作简单名称：
```
import { X, Y } from './utils'
X // 表示来自utils的X
Y // 表示来自utils的Y
```
如果标识符列表定义了ident as alias，则实体ident将绑定在名称alias下：
```
import { X as Z, Y } from './utils'
Z // 表示来自Utils的X
Y // 表示来自Utils的Y
X // 编译时错误：'X'不可见
```
### 动态导入
应用开发的有些场景中，如果希望根据条件导入模块或者按需导入模块，可以使用动态导入代替静态导入。
import()语法通常称为动态导入dynamic import，是一种类似函数的表达式，用来动态导入模块。以这种方式调用，将返回一个promise。
```
let modulePath = prompt("Which module to load?");
import(modulePath)
.then(obj => <module object>)
.catch(err => <loading error, e.g. if no such module>)
```
如果在异步函数中，可以使用let module = await import(modulePath)。
```
// say.ts
export function hi() {
  console.log('Hello');
}
export function bye() {
  console.log('Bye');
}

async function test() {
  let ns = await import('./say');
  let hi = ns.hi;
  let bye = ns.bye;
  hi();
  bye();
}

```
### 导入HarmonyOS SDK的开放能力
HarmonyOS SDK提供的开放能力（接口）也需要在导入声明后使用。可直接导入接口模块来使用该模块内的所有接口能力，例如：
```
import UIAbility from '@ohos.app.ability.UIAbility';
```
通过导入Kit方式使用开放能力有三种方式：
**方式一：导入Kit下单个模块的接口能力。例如：**
```
import { UIAbility } from '@kit.AbilityKit';
```
**方式二：导入Kit下多个模块的接口能力。例如：**
```
import { UIAbility, Ability, Context } from '@kit.AbilityKit';
```
**方式三：导入Kit包含的所有模块的接口能力。例如：**
```
import * as module from '@kit.AbilityKit';
```
>[!tip] 说明
>方式三可能会导入过多无需使用的模块，导致编译后的HAP包太大，占用过多资源，请谨慎使用。
## 顶层语句
顶层语句是指在模块的最外层直接编写的语句，这些语句不被包裹在任何函数、类、块级作用域中。顶层语句包括变量声明、函数声明、表达式等。
# 关键字
### this
关键字this只能在类的实例方法中使用。
