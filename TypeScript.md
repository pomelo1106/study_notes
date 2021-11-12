# 1、引言

### 1-1、==全局安装typescript==

-`npm i -g typescript`

-`tsc` （查看是否安装成功）

### 1-2、编译成ts文件

定位到ts的文件目录下，终端执行 `tsc 文件名.ts`

就可以将ts文件转化成js文件了；

### 1-3、自动更新生成js文件

在文件目录下执行`tsc --init`,生成tsconfig.json文件![image-20210918110335895](C:\Users\cn\AppData\Roaming\Typora\typora-user-images\image-20210918110335895.png)

指定ts文件转化成js文件的目录；

点击vscode 终端 -> 运行任务 -> typescript -> 监视TypeScript/stuCode/tsconfig.json

![image-20210918110752223](C:\Users\cn\AppData\Roaming\Typora\typora-user-images\image-20210918110752223.png)

# 2、基础数据类型

## 2-1、null和undefined 

```tsx
let u: undefined = undefined;	//undefined
let n: null = null;				//null
```

## 2-2、Boolean 类型

```tsx
let isDone: boolean = false;
let isDone1 : Boolean = new Boolean(1);//定义了一个boolean类型的变量，值为true
let isDone2 : Boolean = new Boolean(0);//定义了一个boolean类型的变量，值为false
```

## 2-3、Number 类型

```tsx
let count: number = 10;
let binaryLiteral: number = 0b1010; // 二进制
let octalLiteral: number = 0o744;    // 八进制
let decLiteral: number = 6;    // 十进制
let hexLiteral: number = 0xf00d;    // 十六进制
```

## 2-4、String 类型

```tsx
let name: string = "semliker";
//使用模板字符串
let words: string = `您好，我是 ${ name } `;
console.log(words);	// 您好，我是semliker
```

## 2-5、Symbol 类型

```tsx
const sym = Symbol();
let obj = {
  [sym]: "semlinker",
};
console.log(obj[sym]); // semlinker 
let sym: symbol = Symbol("me"); //Symbol
```

## 2-6、ARRAY数组

```js
//1、创建string类型的数组
let arr:string[] = ["1","2"];		//元素必须是字符串
let arr2:Array<string> = ["1","2"]；//泛型的写法

//2、联合类型数组
 - 表示定义了一个名称叫做arr的数组, 
 - 这个数组中将来既可以存储数值类型的数据, 也可以存储字符串类型的数据
let arr3:(number | string)[];
arr3 = [1, 'b', 2, 'c'];
```

## 2-7、枚举 - Enum 

### 2-7-1、枚举用来干嘛

枚举（Enum）类型用于取值被==限定==在一定范围内的场景，比如一周只能有七天，颜色限定为红绿蓝等；

### 2-7-2、数字枚举

```tsx
enum Days {Sun, Mon, Tue, Wed, Thu, Fri, Sat};

console.log(Days["Sun"] === 0); // true
console.log(Days[0] === "Sun"); // true

//    Days[Days["Sun"] = 0] = "Sun";
//    Days[Days["Mon"] = 1] = "Mon";
//    Days[Days["Tue"] = 2] = "Tue";
//    Days[Days["Wed"] = 3] = "Wed";
//    Days[Days["Thu"] = 4] = "Thu";
//    Days[Days["Fri"] = 5] = "Fri";
//    Days[Days["Sat"] = 6] = "Sat";
```

### 2-7-3、手动赋值

==注意：==未手动赋值的枚举项会接着上一个枚举项递增。

==注意：==有可能递增的过程中，出现系数覆盖，比如下面的Days[7] === "Wed"

```tsx
enum Days {Sun = 7, Mon = 1, Tue=6, Wed, Thu, Fri, Sat};
//  Days[Days["Sun"] = 7] = "Sun";
//  Days[Days["Mon"] = 1] = "Mon";
//  Days[Days["Tue"] = 6] = "Tue";
//  Days[Days["Wed"] = 7] = "Wed";
//  Days[Days["Thu"] = 8] = "Thu";
//  Days[Days["Fri"] = 9] = "Fri";
//  Days[Days["Sat"] = 10] = "Sat";
console.log(Days[7]);	//Wed
```

### 2-7-4、常量枚举

常数枚举是使用==const enum== 定义的枚举类型：

```tsx
const enum Directions { Up,  Down,  Left,  Right }
let directions = [Directions.Up, Directions.Down, Directions.Left, Directions.Right];
console.log(directions);//[0,1,2,3]
```

### 2-7-5、外部枚举

外部枚举是使用 ==declare==关键字定义的枚举类型

```tsx
declare enum Directions { Up,  Down,  Left,  Right }
let directions = [Directions.Up, Directions.Down, Directions.Left, Directions.Right];
console.log(directions);//[0,1,2,3]
```

### 2-7-6、异构枚举

```tsx
enum Enum {
  A,
  B,
  C = "C",
  D = "D",
  E = 8,
  F,
}
//------
"use strict";
var Enum;
(function (Enum) {
    Enum[Enum["A"] = 0] = "A";
    Enum[Enum["B"] = 1] = "B";
    Enum["C"] = "C";
    Enum["D"] = "D";
    Enum[Enum["E"] = 8] = "E";
    Enum[Enum["F"] = 9] = "F";
})(Enum || (Enum = {}));

```

## 2-8、任意值 - any 

请记住，==any 是魔鬼！尽量不要用any==，因为：无法使用 TypeScript 提供的大量的保护机制

```tsx
var myFavoriteNumber:string = 'hello';
myFavoriteNumber = 7;//报错  7  是number类型，不能进行修改成string类型的数据

//如果是 `any` 类型，则允许被赋值为任意类型
let a: any = 666;
a = "Semlinker";
a = false;
a = 66
a = undefined
a = null
a = []
a = {}
```

## 2-9、Unknown 类型

所有类型都可以赋值给 `any`，所有类型也都可以赋值给 `unknown`。这使得 `unknown` 成为 TypeScript 类型系统的另一种顶级类型（另一种是 `any`）。

`unknown` 类型只能被赋值给 `any` 类型和 `unknown` 类型本身

```tsx
let value: unknown;

value = true; // OK
value = 42; // OK
value = "Hello World"; // OK
value = []; // OK
value = {}; // OK
value = Math.random; // OK
value = null; // OK
value = undefined; // OK
value = new TypeError(); // OK
value = Symbol("type"); // OK
```



## 2-10、元祖Tuple

### 2-10-1、用来干嘛的？

​	    众所周知，数组一般由同种类型的值组成，但有时我们需要在单个变量中存储不同类型的值，这时候我们就可以使用元组。

​		单个变量中存储不同类型的值，单个变量中存储不同类型的值，可以限制`数组元素的个数和类型`，它特别适合用来实现多值返回。

### 2-10-2、限制长度

```tsx
let x: [string, number]; 
// 类型必须匹配且个数必须为2

x = ['hello', 10]; // OK 
x = ['hello', 10,10]; // Error 报错
```

### 2-10-3、元祖类型的解构赋值

```tsx
let employee: [number, string] = [1, "Semlinker"];
let [id, username] = employee;
console.log(`id: ${id}`);//1
console.log(`username: ${username}`);//Semlinker 
```

### 2-10-4、可选元素

```tsx
let optionalTuple: [string, boolean?];
optionalTuple = ["Semlinker", true];
console.log(`optionalTuple : ${optionalTuple}`);// Semlinker,true
optionalTuple = ["Kakuqo"];
console.log(`optionalTuple : ${optionalTuple}`);// Kakuqo
```

### 2-10-5、剩余元素

```tsx
type RestTupleType = [number, ...string[]];
let restTuple: RestTupleType = [666, "Semlinker", "Kakuqo", "Lolo"];
console.log(restTuple[0]);//666
console.log(restTuple[1],restTuple[2],restTuple[3]);// "Semlinker", "Kakuqo", "Lolo"
```

### 2-10-6、只读元祖

关键字： ==readonly==

```tsx
let point: readonly [number, number] = [10, 20];
point[0] = 12;//报错 ，只读属性
```

## 2-11、Void类型

void 类型像是与 any 类型相反，它表示没有任何类型。当一个函数没有返回值时，你通常会见到其返回值类型是 void

```tsx
function warnUser(): void {
  console.log("This is my warning message");
}
```

声明一个 void 类型的变量没有什么作用:

```tsx
let unusable: void = undefined;
```

## 2-12、Never 类型

类型表示的是那些永不存在的值的类型，会抛出异常或根本就不会有返回值的函数表达式或箭头函数表达式的返回值类型。

```tsx
// 返回never的函数必须存在无法达到的终点
function error(message: string): never {
  throw new Error(message);
}

function infiniteLoop(): never {
  while (true) {}
}
```

在 TypeScript 中，可以利用 never 类型的特性来实现全面性检查，具体示例如下：

```typescript
type Foo = string | number;

function controlFlowAnalysisWithNever(foo: Foo) {
  if (typeof foo === "string") {
    // 这里 foo 被收窄为 string 类型
  } else if (typeof foo === "number") {
    // 这里 foo 被收窄为 number 类型
  } else {
    // foo 在这里是 never
    const check: never = foo;
  }
}
```

# 3、数组类型

## 3-1、类型 + 方括号表示法

定义了一个Number类型的数组，数组中==不允许==出现Number类型以外的元素，比如String、undefined...

```tsx
let fibonacci: number[] = [1, 1, 2, 3, 5];
fibonacci.push(6)
console.log(fibonacci); //[ 1, 1, 2, 3, 5, 6 ]
```

## 3-2、数组泛型

```tsx
let fibonacci: Array<number> = [1, 1, 2, 3, 5];
console.log(fibonacci);//[ 1, 1, 2, 3, 5 ]
```

## 3-3、使用any定义数组

什么类型都可以放

```tsx
let list: any[] = ["12",21,"cn",{name:"cnn",age:12}];
console.log(list)   //[ '12', 21, 'cn', { name: 'cnn', age: 12 } ]
```

# 4、函数类型

### 4-1、函数声明

- 定义了一个函数，参数是x，y,都是Number类型；
- 返回的结果也是Number类型；
- 一旦执行函数时，参数是字符串就会报错；
- 而且参数的个数必须和函数定义时的参数个数一致

```tsx
function sum(x: number, y: number): number {
    return x + y;
}
console.log(sum(1,2));//3
```

### 4-2、函数表达式

 TypeScript 的类型定义中，`=>` 用来表示函数的定义，左边是输入类型，需要用括号括起来，右边是输出类型。

```tsx
let mySum: (x: number, y: number) => number = function (x: number, y: number): number {
    return x + y;
};
console.log(mySum(1,2));//3
```

### 4-3、可选参数

- firstName：必选参数
- lastName：可选参数
- ==可选参数必须跟在必选参数后面，也就是说，可选参数后面不能有必选参数==

```tsx
function buildName(firstName: string, lastName?: string) {
    if (lastName) {
        return firstName + ' ' + lastName;
    } else {
        return firstName;
    }
}
console.log(buildName('Tom', 'Cat'))//Tom Cat
console.log(buildName('Tom'));//Tom
```

### 4-4、参数默认值

```tsx
//1-
function buildName(firstName: string, lastName: string = 'Cat') {
    return firstName + ' ' + lastName;
}
console.log(buildName('Tom', 'Cat'))//Tom Cat
console.log(buildName('Tom'))//Tom Cat

//2-
function buildName(firstName: string = 'Tom', lastName: string) {
    return firstName + ' ' + lastName;
}
console.log(buildName('Tom', 'Cat'))//Tom Cat
console.log(buildName(undefined, 'Cat'))//Tom Cat
```

### 4-5、剩余参数

```tsx
function push(array:any, ...items:any[]) {
    items.forEach(function(item) {
        array.push(item);
    });
}

var a = [];
push(a, 1, 2, 3);
console.log(a);	//[1,2,3]
```

### 4-6、重载

实现一个将参数反转的函数

```tsx
function reverse(x: number): number;
function reverse(x: string): string;
function reverse(x: number | string): number | string | void {
    if (typeof x === 'number') {
        return Number(x.toString().split('').reverse().join(''));
    } else if (typeof x === 'string') {
        return x.split('').reverse().join('');
    }
}
console.log(reverse(123123));//321321
console.log(reverse("chengneng"));//gnengnehc
```





# 5、对象类型

### 5-1、什么是接口

在TypeScript中，接口Interfaces除了可用于对类的一部分行为进行抽象以外，也常用于对「对象的形状（Shape）」进行描述

### 5-2、接口定义对象

```tsx
interface Person {
    name: string;
    age: number;
}
let tom: Person = {
    name: 'Tom',
    age: 25
};

//-----报错-----赋值的时候，变量的形状必须和接口的形状保持一致
let tom1: Person = {
    name: 'Tom'
};
let tom2: Person = {
    name: 'Tom',
    age: 25,
    gender: 'male'
};
```

### 5-3、可选属性

```tsx
interface Person {
    name: string;
    age?: number;	//设置为可选
}
let tom1: Person = {
    name: 'Tom'
};
let tom2: Person = {
    name: 'Tom',
    age: 25
};
```

### 5-4、任意属性

```tsx
interface Person {
    name: string;
    age?: number;
    [propName: string]: any;
}
let tom: Person = {
    name: 'Tom',
    gender: 'male',
    hobby:'pin'
};
```

### 5-5、只读属性

```tsx
interface Person {
    readonly id: number;//使用readonly关键字，将id设置成number类型的只读不可更改的变量
    name: string;
    age?: number;
    [propName: string]: any;
}

let tom: Person = {
    id: 89757,		//设定初始值
    name: 'Tom',
    gender: 'male'
};
```



# 6、联合类型 ==|==

### 6-1、初始

这里 `name` 的类型是 `string | undefined` 意味着可以将 `string` 或 `undefined` 的值传递给`sayHello` 函数

```tsx
const sayHello = (name: string | number) => {
  console.log(name)
}
sayHello("cn");//cn
sayHello(12);//12

sayHello(true);//报错，Boolean值，为定义
```









# 6、TS中class类

### 6-1、访问修饰符

- `public` 修饰的属性或方法是公有的，可以在任何地方被访问到，默认所有的属性和方法都是 `public` 的
- `private` 修饰的属性或方法是私有的，不能在声明它的类的外部访问，该类不允许被继承或者实例化：
- `protected` 修饰的属性或方法是受保护的，该类只允许被继承：

```tsx
class Animal {
   public name;		//name属性设置成public公有属性，在实例出可以别访问
   public constructor(name:any) {
      this.name = name;
   }
}
  
let cat = new Animal('Jack');
console.log(cat.name); // Jack
cat.name = 'Tom';
console.log(cat.name); // Tom
```

<img src="C:\Users\cn\AppData\Roaming\Typora\typora-user-images\image-20210919151816705.png" alt="image-20210919151816705" style="zoom:67%;" />

<img src="C:\Users\cn\AppData\Roaming\Typora\typora-user-images\image-20210919152340824.png" alt="image-20210919152340824" style="zoom:67%;" />

### 6-2、参数属性

是的代码表达更加简洁，

```tsx
//1、public
class Animal {
  // public name: string;
  public constructor(public name) {
    // this.name = name;
  }
}
//2、private
class Animal {
  // private name: string;
  public constructor(private name) {
    // this.name = name;
  }
}
//3、protected
class Animal {
  // protected name: string;
  public constructor(protected name) {
    // this.name = name;
  }
}
```

### 6-3、只读属性readonly

<img src="C:\Users\cn\AppData\Roaming\Typora\typora-user-images\image-20210919153023967.png" alt="image-20210919153023967" style="zoom:67%;" />

### 6-4、抽象类

使用关键字 ==abstract==定义一个抽象类；

- 抽象类不允许被实例化；
- 只能通过继承的方式；

```tsx
abstract class Animal {
    public name;
    public constructor(name :any) {
      this.name = name;
    }
    public abstract sayHi(): any;
}
  
class Cat extends Animal {
    public sayHi() {
      console.log(`Meow, My name is ${this.name}`);
    }
}
  
let cat = new Cat('Tom');
cat.sayHi();//Meow, My name is Tom
```



