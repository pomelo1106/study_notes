# 0、`JS`中的数据类型（7种）

- Undefined；
- Null；
- 布尔值（Boolean）；
- 字符串（String）；
- 数值（Number）；
- 对象（Object）；
- symbol（表示唯一值）【ximbou~】

<img src="C:\Users\cn\AppData\Roaming\Typora\typora-user-images\image-20210928111444594.png" alt="image-20210928111444594" style="zoom: 80%;" />

### 0-1、js的数据类型的转换

在 JS 中类型转换只有三种情况，分别是：

- 转换为布尔值（调用Boolean()方法）
- 转换为数字（调用Number()、parseInt()和parseFloat()方法）
- 转换为字符串（调用.toString()或者String()方法）
- ==null和underfined没有.toString方法==

### 0-2、JS中数据类型的判断

#### 0-2-1、typeof

​		typeof 对于原始类型来说，除了 null 都可以显示正确的类型。可以利用 `typeof` 来判断`number`, `string`, `object`, `boolean`, `function`, `undefined`, `symbol` 这七种类型

```js
console.log(typeof 2);               // number
console.log(typeof true);            // boolean
console.log(typeof 'str');           // string
console.log(typeof undefined);       // undefined

console.log(typeof null);            // object     null 的数据类型被 typeof 解释为 object
console.log(typeof []);              // object     []数组的数据类型在 typeof 中被解释为 object
console.log(typeof {});              // object
console.log(typeof function(){});    // function
```

#### 0-2-2、instanceof

​			instanceof可以精准判断引用数据类型（Array，Function，Object），而基本数据类型不能被instanceof精准判断。内部机制是通过__proto__（隐式原型一层一层往上找，能否找到对应构造函数的prototype）

```js
console.log(2 instanceof Number);                    // false
console.log(true instanceof Boolean);                // false 
console.log('str' instanceof String);                // false  
console.log([] instanceof Array);                    // true
console.log(function(){} instanceof Function);       // true
console.log({} instanceof Object);                   // true  
```

#### 0-2-3、constructor

```js
console.log((2).constructor === Number); // true
console.log((true).constructor === Boolean); // true
console.log(('str').constructor === String); // true
console.log(([]).constructor === Array); // true
console.log((function() {}).constructor === Function); // true
console.log(({}).constructor === Object); // true
//--------------
function Fn(){};
Fn.prototype=new Array();
var f=new Fn();
console.log(f.constructor===Fn);    // false
console.log(f.constructor===Array); // true 
```

#### 0-2-4、Object.prototype.toString.call()

```js
console.log(Object.prototype.toString.call(2)); //[object Number]
console.log(Object.prototype.toString.call(true)); //[object Boolean]
console.log(Object.prototype.toString.call('str')); //[object String]
console.log(Object.prototype.toString.call([])); //[object Array]
console.log(Object.prototype.toString.call(function () {})); //[object Function]
console.log(Object.prototype.toString.call({})); //[object Object]
console.log(Object.prototype.toString.call(undefined)); //[object Undefined]
console.log(Object.prototype.toString.call(null)); //[object Null]
```



# 1、变量定义(var\let\const)

### 1-1、概念：

- **`var`**定义的变量可被更改，如果不初始化而直接使用也不会报错
- **`let`**定义的变量和var类似，但作用域在当前声明的范围内
- **`const`**定义的变量只可初始化一次且作用域内不可被更改，使用前必须初始化

### 1-2、var:

1. 变量的声明，会在代码被执行之前被处理。
2. 用var声明的JavaScript变量，其可用范围在当前执行上下文。
3. 在函数外声明的JavaScript变量，其作用范围是**全局**。

```javascript
function nodeSimplified() {
 var a =10;
 console.log(a); // 输出 10
 if(true) {
 	var a=20;
 	console.log(a); // 输出 20
 }
 console.log(a); // 输出 20
}
nodeSimplified();
```

​		PS:	当变量a在if代码段里被更新时，它的值被全局更新了，因此在经过了if代码后，被更新的值仍然被保留着。在使用这个`var`时要非常小心，因为它有可能会覆盖一个已有的值。

### 1-3、let(建议常用):

1. `	let`语句在一个**块级范围**里声明一个**局部变量**。和var类似，我们可以在声明时初始化它的值

```javascript
function nodeSimplified() {
 let a =10;
 console.log(a); // output 10
 if(true) {
 	let a=20;
 	console.log(a); // output 20
 }
 console.log(a); // output 10
}
nodeSimplified();
```

​         2、`let`变量声明：具有局部作用域，只在它声明变量的作用域范围内进行使用，不造成变量冲突、污染;

可以很好的维护变量的作用范围。当使用内部函数时，let语句让你的代码更整洁

```javascript
function nodeSimplified() {
 let a =10;
 let a =20; // 抛出语法错误 "未捕获的异常:标识符'a'已经被声明过。"
 console.log(a); 
}
nodeSimplified();
```

### 1-4、const:

​		1、`	const`语句在一个**块级范围**里声明一个**局部变量**。和`let`类似，但是必须进行初始化；否则就会报错

```javascript
const My_value;
console.log(My_value);	// Missing initializer in const declaration(必须要赋初值)
```

​		2、当const声明的变量进行初始化赋值后，不可对该变量进行二次赋值，否则报错

```javascript
const My_value = 12;
My_value = 15;

console.log(My_value)//Assignment to constant variable（const定义了变量且存在初始值）
```







# 2、数组Array

### **2-1、创建：**

1. 使用 JavaScript 关键词 new；

   ```javascript
   var cars = new Array("Saab", "Volvo", "BMW");
   ```

2. 创建 JavaScript 数组最简单的方法；

   ```javascript
   var cars = ["Saab", "Volvo", "BMW"];
   ```

### **2-2、操作数组方法(常用)**

##### 1、unshift(前面添加)

- 在数组的首位新增一个或多数据，并且返回新数组的长度，==**会改变原来的数组**==

  ```javascript
  var arr = ["a", "b"];
  arr.unshift("12","88");
  console.log(arr);	//[ '12', '88', 'a', 'b' ]
  ```

##### 2、push(后面添加)

- 在数组的最后一位新增一个或多个数据，并且返回新数组的长度，==**会改变原来的数组**==

  ```javascript
  var arr = ["a", "b"];
  arr.push("12","88");
  console.log(arr);	//[  'a', 'b' ,'12', '88']
  ```

##### 3、shift(删除前面一位)

- 删除数组的第一位数据，并且返回新数组的长度，==**会改变原来的数组**==

  ```javascript
  var str1 = [12,2,"hello"];
  console.log(str1.shift());　　　　　　//12
  console.log(str1);　				   //[2,'hello']
  ```

##### 4、pop(删除最后一位)

- 删除数组的最后一位，并且返回删除的数据，==**会改变原来的数组**==

  ```javascript
  var str1 = [12,2,"hello"];
  console.log(str1.pop())　　// hello
  console.log(str1);　  	 //	[ 12, 2 ]
  ```

##### 5、sort(排“升”序)

- 对数组内的数据进行排序(默认为升序)，并且返回排过序的新数组，==会改变原来的数组==

- 字母排序

  ```javascript
  var str1 = ["b","c","a"];
  console.log(str1.sort()); //[ 'a', 'b', 'c' ]
  ```

- 数字排序

  ```javascript
  var str1 = [12,2,43,5,2,5];
  function fn (a,b){
      return a-b;
  }
  console.log(str1.sort(fn)); //[ 2, 2, 5, 5, 12, 43 ]
  ```

##### 6、reverse（反转）

将数组的数据进行反转，并且返回反转后的数组，==**会改变原数组**==

```javascript
var str1 = [12,2,"hello"];
console.log(str1.reverse());　　　　　　//["hello", 2, 12]
console.log(str1);　　　　　　　　　　　　//["hello", 2, 12]
```

##### 7、splice(综合)

​	方法向/从数组中添加/删除项目，然后返回被删除的项目,==**会改变原数组**==

```shell
arrayObject.splice(index,howmany,item1,.....,itemX)
---------------------------------------
index	必需。整数，规定添加/删除项目的位置，使用负数可从数组结尾处规定位置。
howmany	必需。要删除的项目数量。如果设置为 0或者1，则不会删除项目。
item1, ..., itemX	可选。向数组添加的新项目。
```

- 添加

  ```javascript
  var str1 = ["b","c","a","d","e","f"];
  str1.splice(4,0,'gggg');
  console.log(str1);	//[ "b",c","a","d","gggg","e","f"]
  ```

- 替换

  ```javascript
  var str1 = ["b","c","a","d","e","f"];
  str1.splice(4,1,'g');
  console.log(str1);	//[ 'b', 'c', 'a', 'd', 'gggg', 'f' ]
  ```

- 删除

  ```javascript
  var str1 = ["b","c","a","d","e","f"];
  str1.splice(4,2);
  console.log(str1);		//[ 'b', 'c', 'a', 'd' ]
  ```

##### 8、sort(排“降”序)

```javascript
var str1 = [12,2,43,5,2,5];
console.log(str1.sort(fn)); //[ 2, 2, 5, 5, 12, 43 ]
function fn (a,b){
    return b-a;
}
```



### **2-3、扩展方法**

##### 1、concat(合并)

合并数组，可以合并一个或多个数组，会返回合并数组之后的数据，**不会改变原来的数组**

```javascript
var str1 = [1,2,3];
var str2 = [4,5,6];
console.log(str1.concat(str2));//[ 1, 2, 3, 4, 5, 6 ]
```

##### 2、join

​	将数组转为字符串并返回转化的字符串数据，**不会改变原来的数组**

```javascript
var str1 = [12,2,"hello"];
var str2 = ["world"];
console.log(str1.join("-"));　　　　　　　　//12-2-hello
console.log(str1);　　　　　　　　　　　　　　//[12, 2, "hello"]
```

##### 3、slice(截取)

截取指定位置的数组，并且返回截取的数组，**不会改变原数组**

slice(start,end)		表示从 start  开始截取，截取end位 （不包括end位）

```javascript
var arr = ["a","b","c","d"];
console.log(arr.slice(1));//[ 'b', 'c', 'd' ]
console.log(arr.slice(1,2));//[ 'b' ]
console.log(arr.slice(1,3));	//[ 'b', 'c' ]
```

##### 4、IndexOf(迭代)

​		根据指定的数据，**从左向右**，查询在数组中出现的位置；

1. ​		如果不存在指定的数据，返回-1

2. ​		找到了指定的数据返回该数据的索引

   参数：indexOf(value, start);

   ​	value为要查询的数据；

   ​	start为可选，表示开始查询的位置，

   ​	当start为负数时，从数组的尾部向前数；

   ​	如果查询不到value的存在，则方法返回-1；

   ```javascript
   var arr = ["a","bb","c","d","bb"];
   console.log(arr.indexOf("bb"));		//1
   console.log(arr.indexOf("bb",3));	//4
   console.log(arr.indexOf("ggg"));	// -1
   ```

##### 5、reduce(逼格更高)

　			**功能：从数组的第一项开始，逐个遍历到最后，迭代数组的所有项，然后构建一个最终返回的值**；

​				reduce 为数组中的每一个元素依次执行回调函数，不包括数组中被删除或从未被赋值的元素，接受四个参数：初始值（或者上一次回调函数的返回值），当前元素值，当前索引，调用 reduce 的数组；

```shell
callback （执行数组中每个值的函数，包含四个参数）

    1、previousValue （上一次调用回调返回的值，或者是提供的初始值（initialValue））
    2、currentValue （数组中当前被处理的元素）
    3、index （当前元素在数组中的索引）
    4、array （调用 reduce 的数组）

initialValue （作为第一次调用 callback 的第一个参数。）
```

```javascript
var arr = [1, 2, 3, 4];
var sum = arr.reduce(function(prev, cur, index, arr) {
    console.log(prev, cur, index,arr);
    return prev + cur;
})
//1 2 1 [ 1, 2, 3, 4 ]
//3 3 2 [ 1, 2, 3, 4 ]
//6 4 3 [ 1, 2, 3, 4 ]
```

##### 6、reduce（求和）

```javascript
function Sum(...nums){
    return nums.reduce((preValue,currntValue) => {
        return preValue+currntValue
    })
}
console.log(sum(1,2,3));//6
```

##### 7、includes()

==作用：==用于判断arr中是否存在某一值，存在返回ture否则返回false

```js
var arr = [1, 2, 3]
arr.includes(2);     // true
arr.includes(4);     // false
[1, 2, NaN].includes(NaN); // true
```

### **2-4、遍历数组**

##### 1、for循环

```javascript
var arr = ["a","bb","c","d","bb"];
for(var i=0; i<arr.length; i++){
    console.log(arr[i])
}
//a
//bb
//c
//d
//bb
```

##### 2、`forEach`()

​		`ES5`新增的方法，用来**遍历**数组，没有返回值，

　　　 参数：forEach(callback);callback默认有三个参数，分别为

- value(遍历到的数组的数据)，
- index(对应的索引)，
- self(数组自身)

```javascript
var arr = ["a","bb","c","d","bb"];
arr.forEach(function(value, index, array){
    if(index == 0){//仅在访问第一个元素时
        console.log("arr : " + arr);
    }
    console.log(index + " : " + value);
})
//arr : a,bb,c,d,bb
//0 : a
//1 : bb
//2 : c
//3 : d
//4 : bb
```

##### 3、map()

​		同`forEach`功能；

　　map的回调函数会将执行结果返回，最后map将所有回调函数的返回值组成新数组返回。

　 	参数：map(callback);callback默认有三个参数，分别为

- value(遍历到的数组的数据)，
- index(对应的索引)，
- self(数组自身),

```javascript
var num = [1, 2, 3];
var newNum = num.map((value, index) => {
    return value + 3*index		//index:0,1,2
})
console.log(newNum);  // [ 1, 5, 9 ]
```

##### 4、filter(过滤)

​			1、同`forEach`功能；（遍历）

```javascript
var arr = [5, 6, 15, 26, 8, 99, 1]
var a = arr.filter(function(value,index,self){
    console.log(value + "--" + index + "--" + (arr === self))
})
//5--0--true
//6--1--true
//15--2--true
//26--3--true
//8--4--true
//99--5--true
//1--6--true
```

​			2、`filter`的回调函数需要返回布尔值，当为`true`时，将本次数组的数据返回给`filter`，最后filter将所有回调函数的返回值组成新数组返回（此功能可理解为“过滤”）。

　　　 参数：filter(callback);callback默认有三个参数，分别为value，index，self。

```javascript
var arr = [5, 6, 15, 26, 8, 99, 1]
var res = arr.filter(function (item) {
    return item > 10;
})
console.log('res：', res);// res：[15, 26, 99]
```

##### 5、every()

​		判断数组中每一项是否都满足条件，**只有所有项都满足条件**，才会返回true

​			当每个回调函数的返回值都为true时，every的返回值为true，只要有一个回调函数的返回值为false，every的返回值都为false

```javascript
var arr = ["Tom","abc","Jack","Lucy","Lily","May"];
var a = arr.every(function(value,index,self){
    return value.length > 3;
})
console.log(a);           //false

var b = arr.every(function(value,index,self){
    return value.length > 2;
})
console.log(b);           //true
```

##### 6、some()

判断数组中是否存在满足条件的项，**只要有一项满足条件**，就会返回true。

```javascript
var arr = ["Tom","abc","Jack","Lucy","Lily","May"];
var a = arr.some(function(value,index,self){
    return value.length > 3;
})
console.log(a); //true
```

## 2-5、数组扁平化(多维-> 一维)

在前端面试中有详细的

## 2-6、数组去重

### 2-6-1、ES5（利用indexOf）

```js
var arr = [5, 3, 5, 4, 5, 2, 2]
const unique2 = arr => {
    const res = [];
    for (let i = 0; i < arr.length; i++) {
        if (res.indexOf(arr[i]) === -1) res.push(arr[i]);
    }
    return res;
}
console.log(unique2(arr));//[ 5, 3, 4, 2 ]
```

### 2-6-2、include

```js
var arr = [5, 3, 5, 4, 5, 2, 2]
const unique2 = arr => {
    const res = [];
    for (let i = 0; i < arr.length; i++) {
        if (!res.includes(arr[i])) res.push(arr[i]);
    }
    return res;
}
console.log(unique2(arr));//[ 5, 3, 4, 2 ]
```

### 2-6-3、filter + indexOf

```js
var arr = [5, 3, 5, 4, 5, 2, 2]
const unique4 = arr => {
    return arr.filter((item, index) => {
      return arr.indexOf(item) === index;
    });
  }
console.log(unique4(arr));//[ 5, 3, 4, 2 ]
```

### 2-6-4、Set

```js
var arr = [5, 3, 5, 4, 5, 2, 2]
const res1 = new Set(arr)
console.log(res1);//Set(4) { 5, 3, 4, 2 }
const res2 = Array.from(new Set(arr))
console.log(res2);//[ 5, 3, 4, 2 ]
```

### 2-6-5、Map

```js
var arr = [5, 3, 5, 4, 5, 2, 2]
let map = new Map();
function unique(arr) {
    let res = []
    for (let i = 0; i < arr.length; i++) {
        if (!map.has(arr[i])) {
            map.set(arr[i], true)
            res.push(arr[i]);
        }
    }
    return res
}
console.log(unique(arr));//[ 5, 3, 4, 2 ]
```





# 3、对象Object

​			对于事物我们可以把他们看作是一个对象，而**每一个事物都有自己的表示的属性和对于某一信息作出的相应的操作**。而这些东西就变成了事物的属性和方法

### 3-1、对象的创建

#### 		3-1-1、对象字面量

​		对象字面量是对象定义的一种简写形式，目的在于简化创建包含大量属性的对象的过程。也就是说，第一种和第二种方式创建对象的方法其实都是一样的，只是写法上的区别不同。

缺点：**它们都是用了同一个接口创建很多对象，会产生大量的重复代码**

```javascript
var obj = {
    name: 'cn',
    getName: function() {
        return this.name
    }
}
console.log(obj);			//{ name: 'cn', getName: [Function: getName] }
console.log(obj.name);		//cn
console.log(obj.getName);	//[Function: getName]
```

#### 	3-1-2、new Object()

​	创建了Object引用类型的一个新实例，然后把实例保存在变量obj中；

​	缺点：**它们都是用了同一个接口创建很多对象，会产生大量的重复代码**

```javascript
var obj = new Object();

obj.name = "cn";
obj.getname = function(){
   ...
}
```

#### 	3-1-3、构造函数创建

```javascript
var Obj = function (name) {
    this.name = name;
    this.getname = function () {
        return this.name;
    }
}
var cnobj = new Obj("cn");
console.log(cnobj)	//Obj { name: 'cn', getname: [Function (anonymous)] }
```

**对比工厂模式，我们可以发现以下区别：**

- ​	1.没有显示地创建对象
- ​	2.直接将属性和方法赋给了this对象
- ​	3.没有return语句
- ​	4.终于可以识别的对象的类型。对于检测对象类型，我们应该使用`instanceof`操作符，我们来进行自主检测：

优点：实例可以识别为一个特定的类型

缺点：每次创建实例时，每个方法都要被创建一次

#### 3-1-4、工厂模式

缺点：对象无法识别，都指向一个原型

```javascript
var createObj = function (name) {
    var obj = new Object();
    obj.name = name;
    obj.getName = function (){
        return obj.name;
    }
    return obj;
}
var cnObj = createObj("cn");
console.log(cnObj)	//{ name: 'cn', getName: [Function (anonymous)] }
```

#### 3-1-5、Object.create() 

​			`ECMAScript 5`中新增的方法，这个方法用于创建一个新对象。被创建的对象继承另一个对象的原型，在创建新对象时可以指定一些属性

```javascript
var obj = Object.create({
    getname: function(value) {
        return value.toString();
    }
})
obj.name = 'cn';
console.log(obj);//{ name: 'cn' }
```

#### 3-1-6、绑定在原型上

==--->==   使用原型创建对象的方式，可以让所有对象实例共享它所包含的属性和方法

优点：可以通过constructor属性找到所属构造函数

缺点：1.所有的属性和方法都共享，2.不能初始化参数

```javascript
function Person() {}
Person.prototype.name = 'Nike';
Person.prototype.age = 20;
Person.prototype.jbo = 'teacher';

Person.prototype.sayName = function () {
    console.log(this.name);
};

var person1 = new Person();
person1.name ='Greg';
console.log(person1.name); //'Greg' --来自实例

var person2 = new Person();
console.log(person2.name); //'Nike' --来自原型
```

#### 3-1-7、（最好的方式）

组合使用构造函数模式和原型模式创建对象

优点：该共享的共享，该私有的私有，使用最广泛的方式

缺点：分开写，不是最佳封装

```javascript
function Person(name, age, job) {
    this.name = name;
    this.age = age;
    this.job = job;
}
Person.prototype = {
    constructor: Person,
    sayName: function () {
        console.log(this.name);
    }
}
var person1 = new Person('Nike', 20, 'teacher');
console.log(person1);//{ name: 'Nike', age: 20, job: 'teacher' }
```

### 3-2、对象遍历的方法(5种)

#### 		3-2-1、for in

​	(循环遍历对象自身的和继承的可枚举属性(循环遍历对象自身的和继承的可枚举属性(不含Symbol属性).)

```javascript
var obj = {
    name: "孙悟空",
    age: 1800,
    gander: "花果山",
};

for (var n in obj) {
    console.log("属性名" + n+"--"+"属性值" + obj[n]);
}
//属性名name--属性值孙悟空
//属性名age--属性值1800
//属性名gander--属性值花果山
```

#### 3-2-2、Object.keys/Object.values

 (返回一个数组,包括对象自身的(不含继承的)所有可枚举属性(不含Symbol属性).)
**--->>>**Object.keys方法只返回可枚举的属性

```javascript
var obj = {
    name: "孙悟空",
    age: 1800,
    gander: "花果山",
};
console.log(Object.keys(obj));//[ 'name', 'age', 'gander' ]

console.log(Object.values(obj));//[ '孙悟空', 1800, '花果山' ]
```

#### 3-2-3、`Object.getOwnPropertyNames(obj)`

返回一个数组,包含对象自身的所有属性(不含Symbol属性,但是包括不可枚举属性)

==`Object.getOwnPropertyNames`==方法还能返回不可枚举的属性名

```javascript
var obj = {
    name: "孙悟空",
    age: 1800,
    gander: "花果山",
};
Object.getOwnPropertyNames(obj).forEach(function(key){
    console.log(key,obj[key]);
});

//name 孙悟空
//age 1800
//gander 花果山
```

#### 3-2-4、`Object.getOwnPropertySymbols(obj)`

返回一个数组，包含对象自身的所有Symbol属性。

#### 3-2-5、`Reflect.ownKeys(obj)`

### 3-3、对象的方法

#### 	3-3-1、find(根据id查找)

-  接收一个方法作为参数，方法内部返回一个条件
-  会遍历所有的元素，执行你给定的带有条件返回值的函数
- 符合该条件的元素会作为 find 方法的返回值
- 如果遍历结束没有符合条件的返回值，返回undefined

```javascript
const detailData = [
      { id: "1", content: "张三", age: 12 },
      { id: "2", content: "李四", age: 47},
      { id: "3", content: "王五", age: 23 }
];
//查找id对应的数据
const fileResult = detailData.find((obj) => {
     return obj.id === this.props.match.params.id
})
```



### 3-4、`Globa`全局对象

#### 3-4-1、定义：

- `global` 和`Math`都是`JavaScript`中两个内置对象的其中一个
- `global` 作为`js`的全局对象，但其是无法直接访问的，但是在浏览器中浏览器是将这个对象当做是window对象的一部分，即Date 等Global的属性使用`window.Date` 可访问到

### 3-5、对象的取值方式

```js
var obj = {
	abc:"ss",
    nn:90
};
var v1 = obj.abc;//使用点的方式
var v2 = obj["abc"];//使用中括号的方式
```

### 3-6、Object - ＡＰＩ

for in （遍历）

hasOwnProperty（检查属性是不是对象自有的，排除从原型链找到的属性）





# 4、正则表达式

### 1、方法

##### 	1-1、test(判定)

```shell
变量名.**test**( “字符串” );	//如果给定的字符串和正则表达式定义的规则一直 返回 true，否则 false
```

##### 	1-2、split(截取)

```javascript
var reg1 = "1a2b3c4d5";
console.log(reg1.split(/[A-z]/));//[ '1', '2', '3', '4', '5' ]
console.log(reg1.split(/[0-9]/));//[ '', 'a', 'b', 'c', 'd', '' ]	(有弊端)
```

##### 	1-3、search(检索)

```javascript
var str = "abc";
console.log(str.search(/b/));	//1
```

##### 	1-4、match

```javascript
var str = "abc";
console.log(str.match(/a/));	//[ 'a', index: 0, input: 'abc', groups: undefined ]
```

### 2、创建正则表达式

​	2-1、var 变量名 = new RegExp(  定义规则  );

```javascript
var reg = new RegExp(/a{2}/);
console.log(reg.test("12aa"));	//true
```

​	2-2、var str = /a{2}/;

```javascript
var reg = new RegExp(/a{2}/);
console.log(reg.test("12aa"));	//true
```

### 3、匹配规则

```javascript
var str = /a/i;  //忽略大小写(a,A,aA)
var str = /a/g;  //全局匹配

var str = /^a/;		//以 a 开头(a,ab,ac....)
var str = /a$/;		//以 a 结尾 (a,ba,ca...)
var str = /^ab$/;	//本身 (ab)

var str = /a{m}/;	//有m个a
var str = /a{m,}/;	//不少于m个a以上
var str = /a{m,n}/;	//不少于m 不多于n

var str = /ab+/;	//至少有ab (ab,abb,abbb...)
var str = /ab*/;	//只要有一个a (a,ab,ba...)
var str = /a?b/;    //有 0 个或者1个a,相当于{0, 1} (b,ab,bb,asad,bb..)

var str = /a[0-9]/; 	 //a后面跟的是数字0~9即可（a1,a11111111111111......）
var str = /a[0-9]{1,2}/; //a后面跟的是数字0~9即可（a1,a11111111111111......）
......
```







# 5、BOM(浏览器对象模型)

### 	1、定义

​			`BOM`：Browser Object Model 是浏览器对象模型，浏览器对象模型 提供了 独立与内容的、可以与浏览器窗口进行互动的对象结构，`BOM`由多个对象构成，其中代表浏览器窗口的window对象是	`BOM`的顶层对象，其他对象都是该对象的子对象

### 2、思维导图

<img src="https://images2015.cnblogs.com/blog/449064/201509/449064-20150901201202388-1759134225.png" alt="img" style="zoom: 80%;" />

### 3、`BOM`对象

##### 5-1、window(顶层对象)

###### 5-1-1、定义

-  `BOM`的核心对象是window，它表示浏览器的一个实例。在浏览器中，window对象有双重角色，它既是通过`javascript`访问浏览器窗口的一个接口，又是`ECMAScript`规定的Global对象。
- window对象不用new，直接进行使用即可。

###### 5-1-2、属性

```css
<body style="height: 12px; width: 230px; background-color: red;"></body>
```

```javascript
console.log(document.body.clientHeight)//返回body的高度
console.log(document.body.clientWidth)//返回body的宽度

console.log(document.documentElement.clientWidth)//返回浏览器窗口可见的宽度（页面视图的宽度）
console.log(document.documentElement.clientHeight)//返回浏览器窗口可见的高度（页面视图的高度）

console.log(window.innerWidth)//返回浏览器窗口可见的宽度（页面视图的宽度）
console.log(window.innerHeight)//返回浏览器窗口可见的高度（页面视图的高度）

console.log(window.outerWidth)//返回窗口本身的宽度大小
console.log(window.outerHeight)//返回窗口本身的高度大小
```

###### 5-1-3、常用的方法

**window（可省略）**

- alert('提示信息')
- confirm("确认信息")
- prompt("弹出输入框")
- open("url地址"，“打开的方式（可以是-self或-black）”，“新窗口的大小”）注：如果url为空，则默认打开一个空白页面，如果打开方式为空，则默认为新窗口方式打开页面。返回值为：返回新打开窗口的window对象
- close()  关闭当前的网页。 注：存在兼容性问题：FF：禁止设置关闭浏览器的代码

- `window.moveTo`() - 移动当前窗口
- `window.resizeTo`() - 调整当前窗口的尺寸

**定时器，清除定时器。**

- `setTimeout`(函数，时间) 只执行一次
  `setInterval`(函数，时间) 无限执行
- `clearTimeout`/`clearInterval`(定时器名称) 清除定时器



##### 5-2、document(文档对象)



##### 5-3、location ( 浏览器当前URL信息)

###### 5-3-1、定义

​			`window.location`对象：用于获得当前页面的地址 (URL)，并把浏览器重定向到新的页面。在编写时可不使用 window 这个前缀；

###### 5-3-2、方法

```javascript
console.log(window.location.hash); //地址栏上#及后面的内容

console.log(window.location.port);//端口号
console.log(window.location.hostname);//主机名
console.log(window.location.host);//主机名及端口号

console.log(window.location.pathname);//文件的路径---相对路径

console.log(window.location.protocol);//协议

console.log(window.location.search);//搜索的内容
```



##### 5-4、navigator(浏览器本身信息)

###### 5-4-1、定义

`window.navigator` 对象包含有关访问者浏览器的信息。在编写时可不使用 window 这个前缀

###### 5-4-2、方法

```javascript
navigator.platform：    操作系统类型；
navigator.userAgent：   浏览器设定的User-Agent字符串。
navigator.appName：     浏览器名称；
navigator.appVersion：  浏览器版本；
navigator.language：    浏览器设置的语言；
navigator.userAgent     是最常用的属性，用来完成浏览器判断
```



##### 5-5、screen(客户端屏幕信息)

###### 5-5-1、定义

`window.screen` 对象包含有关用户屏幕的信息



##### 5-6、history(浏览器访问历史信息)

###### 5-6-1、定义

​	对象包含浏览器的历史。为了保护用户隐私，对 JavaScript 访问该对象的方法做出了限制。

###### 5-6-2、方法

```javascript
alert(history.length);//返回当前浏览器历史列表中的 URL 数量(个数)。

history.back();//返回上一个

fhistory.forward();//可以将当前的网页面返回前一个页面  和  （浏览器的回退按钮效果一样）

history.go(1);//加载 history 列表中的某个具体页面,history.go(1)  相当于  history.forward()
```

## 4、document的属性和方法

- `document.title` //设置文档标题等价于HTML的title标签
- `document.bgColor` //设置页面背景色
- `document.fgColor` //设置前景色(文本颜色)
- `document.linkColor` //未点击过的链接颜色
- `document.alinkColor` //激活链接(焦点在此链接上)的颜色
- `document.vlinkColor `//已点击过的链接颜色
- `document.URL` //设置URL属性从而在同一窗口打开另一网页
- `document.fileCreatedDate `//文件建立日期，只读属性
- `document.fileModifiedDate` //文件修改日期，只读属性
- `document.charset` //设置字符集 简体中文:`gb2312`
- `document.fileSize` //文件大小，只读属性
- `document.cookie` //设置和读出cookie

### 4-1、常用对象方法

1. `document.write()` //动态向页面写入内容
2. `document.createElement(Tag) `//创建一个`html`标签对象
3. `document.getElementById(ID)` //获得指定ID值的对象
4. `document.getElementsByName(Name) `//获得指定Name值的对象
5. `document.body.appendChild(oTag)`

### 4-2、body-主体子对象

- `document.body `//指定文档主体的开始和结束等价于body>/body>
- `document.body.bgColor `//设置或获取对象后面的背景颜色
- `document.body.link `//未点击过的链接颜色
- `document.body.alink `//激活链接(焦点在此链接上)的颜色
- `document.body.vlink `//已点击过的链接颜色
- `document.body.text `//文本色
- `document.body.innerText `//设置body>…/body>之间的文本
- `document.body.innerHTML `//设置body>…/body>之间的HTML代码
- `document.body.topMargin` //页面上边距
- `document.body.leftMargin` //页面左边距
- `document.body.rightMargin `//页面右边距
- `document.body.bottomMargin` //页面下边距
- `document.body.background` //背景图片
- `document.body.appendChild(oTag) `//动态生成一个HTML对象

### 4-3、常用的属性

- `document.documentElement.clientHeight`  -  获取屏幕的可见高度
- `element（元素）.offsetTop`                              -  获取元素相对于文档顶部的高度
- `document.documentElement.scrollTop`        -  获取浏览器窗口滚动条到窗口顶部的距离



# 6、DOM（文档对象模型）

### 1、定义

- DOM 是 Document Object Model（文档对象模型）的缩写；
- 任意的文档都可以绘制成树状结构，在DOM树上，每个元素都可与看做一个对象，每个对象都叫做一个节点(node)。
- `docunment`就是一个对象，这个对象指代的是这个文档
- 文档对象模型 (DOM) 是HTML和XML文档的编程接口。它提供了对文档的结构化的表述，并定义了一种方式可以使从程序中对该结构进行访问，从而改变文档的结构，样式和内容。
- DOM 将文档解析为一个由节点和对象（包含属性和方法的对象）组成的结构集合。简言之，它会将web页面和脚本或程序语言连接起来。

​		***浏览器对象模型*:**

![preview](https://pic1.zhimg.com/v2-3ca668efbe3dccd52bba0d97e4df20fc_r.jpg)

### 2、选择器

```html
<p class="p_class" id="p_id" name="p_name">DOM</p>
<p class="p_class" id="p_id" name="p_name">DOM123123123</p>
```

```javascript
//id选择器
var p_id =  document.getElementById("p_id");//（一个）

//类选择器
var p_class = document.getElementsByClassName("p_class")[0];//（一个）
var p_class = document.getElementsByClassName("p_class");//（多个，伪数组）

//name选择器
var p_name = document.getElementsByClassName("p_name")[0];//（第一个）
var p_name = document.getElementsByClassName("p_name");//（多个，伪数组）

//标签选择器(获取相同标签的名字 input\p\h2\button)
var p_data = document.getElementsByTagName("p")[0];	//（第一个）
var p_data = document.getElementsByTagName("p");//（多个，伪数组）

```

### 3、常用的方法操作

```html
<ul id="city">
	<li id="bj">北京</li>
	<li>海口</li>
	<li>定安</li>
	<li>首尔</li>
</ul>
```

##### 3-1、创建节点\文本

```javascript
var li = document.createElement("li"); //将会根据标签名创建标签对象，相当于创建了一个<li></li> 

var hntext = document.createTextNode("广州");//将会根据标签名创建文本对象

//方法向节点添加最后一个子节点(可以是文本、标签)
li.appendChild(hntext);
var city = document.getElementById("city");
city.appendChild(li);//将li放置在该city div中
```

##### 3-2、插入节点

```javascript
var bj = document.getElementById("bj");
var city = document.getElementById("city");

city.insertBefore(li, bj);//(新节点,旧节点 ) 可以在指定的子节点前插入新的子节点
```

##### 3-3、替换节点

```javascript
var bj = document.getElementById("bj");
var city = document.getElementById("city");	
city.replaceChild(li, bj);//(新节点，  旧节点)可以将指定的将其替换掉
```

##### 3-4、删除节点

```javascript
var bj = document.getElementById("bj");
var city = document.getElementById("city");
city.removeChild(bj);//父节点.removeChild(子节点)，删除指定的子节点
```

##### 3-5、读取html代码

```javascript
//innerHTML
var city = document.getElementById("city");
alert(city.innerHTML);
```

3-6、元素高度\宽度

```javascript
元素名称.offsetHeight
元素名称.offsetWidth
```

##### 3-7、返回元素的父节点

```shell
元素名称.parentNode
```

##### 3-8、返回元素的子节点

|              |                    |          |      |
| ------------ | ------------------ | -------- | ---- |
| child        | 获取所有子节点     | 推荐使用 |      |
| `firstChild` | 获取首个子节点     | 推荐使用 |      |
| `lastChild`  | 获取最后一个子节点 | 推荐使用 |      |

##### 3-9、返回元素的兄弟节点

|                          |                |
| ------------------------ | -------------- |
| `previousElementSibling` | 返回上一个节点 |
| `nextElementSibling`     | 返回下一个节点 |
|                          |                |

### 4、滚动条事件

|                                                 |                                  |
| ----------------------------------------------- | -------------------------------- |
| `onscroll`                                      | 当元素的滚动条滚动时触发的事件   |
| `scrollTop`                                     | 元素滚动条内的顶部隐藏部分的高度 |
| `scrollHeight`                                  | 元素滚动条内的内容高度           |
| `scrollHeight` - `scrollTop` ==  `clientHeight` | 说明垂直滚动条拖拽到底           |
| `scrollWidth` - `scrollLeft` == `clientWidth`   | 说明水平滚动条拖拽到底           |







# 7、Class类

### 7-1、类的实现思路

JavaScript 通过构造函数实现类的概念，通过原型链实现继承。





# 8、回调函数

最简单的回调函数：

```javascript
1、
function f1(fn){
    fn();
}
function f2(){
    console.log("a")
}
f1(f2());		//输出：a

2、
function f3(){
    return 100
}
console.log(f3()); //输出：100

3、
function f4(){
    console.log("f4调用了");
	return function(){
        console.log("我是一个匿名函数");
    }
}
var fun = f4();
fun(); //输出：f4调用了   我是一个匿名函数
```

- 定义：回调是一个在另一个函数完成执行后所执行的函数——故此得名“回调”
- 复杂地说：在 JavaScript 中，函数是对象。因此，函数可以将函数作为参数，并且可以由其他函数返回。执行此操作的函数称为高阶函数。任何作为参数传递的函数都称为回调函数。

```javascript
function first(){ 
	// 模拟代码延迟
  setTimeout( function(){
    console.log(1);
  }, 500 );
}
function second(){
  console.log(2);
}
first();
second();
//输出结果
//2
//1
```

​	凡事需要得到一个函数内部异步操作的结果

- setTimeout
- readFile
- writeFile
- ajax
- ....

都必须通过 回调函数的方式获取

```javascript
function add(x,y,callback) {
    console.log(1);
    setTimeout(function(){
        var ret = x+y;
        callback(ret);
    },1000)
}
add(10,20,function(ret) {console.log("函数的执行结果"+ret);})

//相当于
//var x = 10; 
//var y = 20;
//var callback = functio(){ console.log(ret) }
```





# 9、回调地狱

### 					9-1、定义：

​							在使用JavaScript时，为了实现某些逻辑经常会写出层层嵌套的回调函数，如果嵌套过多，会极大影响代码				可读性和逻辑，这种情况也被成为回调地狱。比如说你要把一个函数 A 作为回调函数，但是该函数又接受一个函				数 B 作为参数，甚至 B 还接受 C 作为参数使用，就这样层层嵌套，人称之为回调地狱。

```shell
var sayhello = function (name, callback) {
  setTimeout(function () {
    console.log(name);
    callback();
  }, 1000);
}
sayhello("first", function () {
  sayhello("second", function () {
    sayhello("third", function () {
      console.log("end");
    });
  });
});
//输出： first second third  end
```

### 			9-2、解决回调地狱的方法

- Promise 
- Generator 
- `async` 

#### 9-2-1、promise（承诺、保证）

为了解决异步函数带来的回调地狱等诸多问题，所以在`EcmaScript6`中新增了一个`API` `promise`, 构造函数它只有一个任务，处理待定任务，只能产生 处理成功后的结果 或者 处理失败后的结果。 

```javascript
var fs = require('fs');
let p1 = new Promise((resolve, reject) => {
    fs.readFile('读取文件的路径','utf-8',function(err,data) {
        if(err) {
            //读取失败，把容器中的pending状态变为reject 
            reject(err);
        } else {
            //读取成功，把容器中的pending状态变为resolve（也就是p1.then()执行的函数操作）
            resolve(data);
        }        
    })
});
let p2 = new Promise((resolve, reject) => {
    fs.readFile('读取文件的路径','utf-8',function(err,data) {
        if(err) {
            //读取失败，把容器中的pending状态变为reject 
            reject(err);
        } else {
            //读取成功，把容器中的pending状态变为resolve（也就是p1.then()执行的函数操作）
            resolve(data);
        }        
    })
});
p1.then( function(data_p1) {
    	console.log(data_p1);
    	return p2;		//当读取p1成功时，返回 p2
	},function(err) {
    	console.log(err)
	})
	//执行p2
	.then( function(data_p2) {
    	console.log(data_p2)
	})

```





# 10、Set

### 10-1、定义

`ES6`提供了新的数据结构Set。它类似于数组，但是==成员的值都是唯一的，没有重复的值==。Set本身是一个构造函数，用来生成Set数据结构。

### 10-2、应用

#### 10-2-1、数组去重



```js
//方法1
var arr = [5, 3, 5, 4, 5, 2, 2]
var s = new Set(arr);
console.log(s); //Set(4) { 5, 3, 4, 2 }
//console.log[...Set(arr)]

//方法2 - 转化成Array
var arr = [5, 3, 5, 4, 5, 2, 2]
function dedupe(array) {
    return Array.from(new Set(array));
}
console.log(dedupe(arr));//[ 5, 3, 4, 2 ]
```

#### 10-2-2、`set.has()`

思想： 利用set（）的内置方法 `has（）`，判断所带参数是不是set的内部元素成员。是:ture，不是:false

```js
var s = new Set([1,2,3,2,2,3,5]);
console.log(s.has(1))// true
console.log(s.has(8))// false
```

#### 10-2-3、扩展运算符

```js
let arr = [3, 5, 2, 2, 5, 5];
let unique = [...new Set(arr)];
console.log(unique);//[ 3, 5, 2 ]
```

#### 10-2-4、filter(过滤处理)

```js
let set = new Set([1, 2, 3, 4, 5]);
set = new Set([...set].filter(x => (x % 2) == 0));
// 返回Set结构：{2, 4}
```

#### 10-2-5、并集、交集和差集

```js
let a = new Set([1, 2, 3]);
let b = new Set([4, 3, 2]);

// 并集
let union = new Set([...a, ...b]);
// Set {1, 2, 3, 4}

// 交集 (利用has 判断是否含有相同的元素，有-> 放到intersect)
let intersect = new Set([...a].filter(x => b.has(x)));
// set {2, 3}

// 差集 (利用has 判断是否含有相同的元素，没有-> 放到intersect)
let difference = new Set([...a].filter(x => !b.has(x)));
// Set {1}
```

### 10-3、Set实例四个遍历方法

- `keys()`：返回键名的遍历器
- `values()`：返回键值的遍历器
- `entries()`：返回键值对的遍历器
- `forEach()`：使用回调函数遍历每个成员

```js
let set = new Set(['red', 'green', 'blue']);

for (let item of set.keys()) {
  console.log(item);// red,green,blue
}

for (let item of set.values()) {
  console.log(item);// red,green,blue
}

for (let item of set.entries()) {
  console.log(item);//  ["red", "red"],["green", "green"], ["blue", "blue"]
}
```





# 11、Map

### 11-1、map是什么

Map数据结构。它类似于对象，也是==键值对==的集合，但是“键”的范围不限于字符串，各种类型的值（包括对象）都可以当作键。也就是说，Object结构提供了“字符串—值”的对应，Map结构提供了“值—值”的对应，是一种更完善的Hash结构实现。

### 11-2、Map的创建

```js
var map = new Map([
    ['name', '张三'],
    ['title', 'Author']
]);
console.log(map.size)// 2   打印map成员的总数
console.log(map.has('name')) // true
console.log(map.has('title')) // true
console.log(map.get('name')) // "张三"
console.log(map.get('title')) // "Author"

var map1 = new Map();
var k1 = ['a'];
var k2 = ['a'];
map1
.set(k1, 111)
.set(k2, 222);
console.log(map1.get(k1)) // 111
console.log(map1.get(k2))// 222
```

### 11-3、属性

- `size` - 属性返回Map结构的成员总数;
- `set` - 方法设置`key`所对应的键值，然后返回整个Map结构。如果`key`已经有值，则键值会被更新，否则就新生成该键;
- `get` - 方法读取`key`对应的键值，如果找不到`key`，返回undefined;
- `has` - 方法返回一个布尔值，表示某个键是否在Map数据结构中;
- `delete` - 方法删除某个键，返回true。如果删除失败，返回false;
- `clear `- 方法清除所有成员，没有返回值;

### 11-4、遍历(4种)

1. `keys()`：返回键名的遍历器。
2. `values()`：返回键值的遍历器。
3. `entries()`：返回所有成员的遍历器。
4. `forEach()`：遍历Map的所有成员。

### 11-5、Map实现过滤

```js
let map = new Map();
map.set(1,100);
map.set(2,200);
map.set(3,300);
map.set(4,400);

console.log( [...map].filter(([k, v]) => k < 3)); //[ [ 1, 100 ], [ 2, 200 ] ]
console.log([...map].map(([k, v]) => [k * 2, '_' + v]));//[ [ 2, '_100' ], [ 4, '_200' ], [ 6, '_300' ], [ 8, '_400' ] ]
```





# 12、Proxy

### 12-1、概述

proxy: 称为==代理==。目标对象之前架设一层“拦截”，外界对该对象的访问，都必须先通过这层拦截，因此提供了一种机制，可以对外界的访问进行过滤和改写。

### 12-2、参数

当Proxy当做==构造函数==使用的时候，也就是 `let  _proxy = new Proxy();`  Proxy()接收两个参数

Proxy(所要代理的目标对象，配置对象)

> ==var proxy = new Proxy(obj, handler());==如果配置对象不设置拦截，同于直接通向原对象

### 12-3、Proxy实例的方法

#### 12-3-1、get()

拦截某个属性的==读取操作==

<img src="C:\Users\cn\AppData\Roaming\Typora\typora-user-images\image-20210920144433842.png" alt="image-20210920144433842" style="zoom:67%;" />

...

#### 12-3-2、set()

拦截某个属性的==赋值操作==

场景1：判断实例.key === age （是小于200的整数）

<img src="C:\Users\cn\AppData\Roaming\Typora\typora-user-images\image-20211008151512688.png" alt="image-20211008151512688" style="zoom:67%;" />

场景二：只要读写的属性名的第一个字符是下划线，一律抛错，从而达到禁止读写内部属性的目的

<img src="C:\Users\cn\AppData\Roaming\Typora\typora-user-images\image-20210920151649875.png" alt="image-20210920151649875" style="zoom:67%;" />

#### 12-3-3、apply()

==拦截函数的调用、call和apply操作==

接收三个参数：1、目标对象。2、目标对象的上下文对象（`this`）。3、目标对象的参数数组。

```js
//变量p是Proxy的实例，当它作为函数调用时（p()），就会被apply方法拦截，返回一个字符串
var target = function () {
    return 'I am the target';
};
var handler = {
    apply: function () {
        return 'I am the proxy';
    }
};
var p = new Proxy(target, handler);
console.log(p());   //I am the proxy
```

```js
var twice = {
    apply(target, ctx, args) {
        return Reflect.apply(...arguments) * 2;
    }
};

function sum(left, right) {
    return left + right;
};
var proxy = new Proxy(sum, twice);
console.log(proxy(1, 2));// 6
console.log(proxy.call(null, 5, 6)); // 22
console.log(proxy.apply(null, [7, 8])) // 30
```

#### 12-3-4、......





# 13、Iterator（迭代器）

### 13-1、迭代器是什么

是一种机制，它是一种接口，为==各种不同的数据结构==提供统一的访问机制。任何数据结构只要部署Iterator接口，就可以完成遍历操作（即依次处理该数据结构的所有成员）

### 13-2、ES6中的四种数据结构接口

数组（Array）、对象（Object）、Map、Set

### 13-3、Iterator的遍历过程

1. 创建一个指针对象，指向当前数据结构的起始位置。也就是说，遍历器对象本质上，就是一个指针对象。
2. 第一次调用指针对象的`next`方法，可以将指针指向数据结构的第一个成员。
3. 第二次调用指针对象的`next`方法，指针就指向数据结构的第二个成员。
4. 不断调用指针对象的`next`方法，直到它指向数据结构的结束位置。

### 13-4、数据结构的默认Iterator接口

有三类数据结构原生具备Iterator接口：==数组、某些类似数组的对象、Set和Map结构==

案例1：数组

```js
let arr = ['a', 'b', 'c'];
let iter = arr[Symbol.iterator]();

iter.next() // { value: 'a', done: false }
iter.next() // { value: 'b', done: false }
iter.next() // { value: 'c', done: false }
iter.next() // { value: undefined, done: true }
```





# 14、迭代器

### 14-1、迭代和遍历有什么区别

- ==遍历==：对不同数据结构进行循环遍历（并不要求依次、连续）
- ==迭代==：让 目标元 进行==依次、连续的遍历操作==

### 14-2、ES6 - 迭代的数据类型

通过==for of==进行遍历，因为这个数据类型的原型上都含有==Symbol.iterator==这个方法（迭代器），当这几个数据类型进行遍历的时候，会调用原型上的==Symbol.iterator==（迭代器对象），调用（迭代器对象的==next()==进行遍历），调用到done = true时，停止遍历

- Array
- String
- Map
- Set
- TypeArray
- arguments
- Nodelist

### 14-3、Object类型不能一步遍历

因为使用Object进行==for of==进行遍历的时候，并不清楚，首先遍历那个，后遍历那个。说直接的就是object原型上没有==Symbol.iterator==





# 15、Generator生成器(==产生迭代器==*关键字)

### 15-1、作用

生成器对象是由一个generator function返回的，并且它符合可迭代规范，具备可迭代性。 生成器函数用function* 来定义，例如 function* fn(){} 普通函数与生成器函数的区别：

- 普通函数是Function的实例，普通函数.__ proto__===Function.prototype
- 生成器函数是GeneratorFunction 的实例，生成器函数.__ proto__ = GeneratorFunction.prototype;GeneratorFunction.prototype.__ proto__ = Function.prototype
- 生成器函数具有IsGenerator属性，值为true
- 生成器函数内部的this并不是指向生成器的实例，而是指向window
- 生成器函数不允许被new，直接当做普通函数调用则会创建实例
  - 当做普通函数调用，其内部的代码并不会执行
  - 当后续调用next才会执行代码，并且每一次执行next遇到一个yield就结束
  - 每一次返回的结果是符合迭代器规范的
  - {done: true/false, value:yield后面的值或者函数的返回值}

==生成迭代器对象；==

假设没有使用生成器object数据结构可以进行遍历的操作（==相当的麻烦==）

```js
/**
 * 思想： 通过给Obj定义一个 可遍历的Symbol.iterator的方法
 *       利用Map数据结构，利用...map.entries() 获取键值对数据   
 */ 
var obj = {
    a:1,
    b:2,
    c:3,
    [Symbol.iterator](){
        var index = 0;
        let map = new Map([["a",1],["b",2],["c",3]]);
        return {
            next() {
                var mapEntries = [...map.entries()];
                if(index < map.size) {
                    return {
                        value: mapEntries[index++],
                        done: false
                    }
                } else{
                    return {
                        value: undefined,
                        done: true
                    }
                }
            }
        }
        
    }
}
var iter = obj[Symbol.iterator]();
console.log(iter.next());   //{ value: [ 'a', 1 ], done: false }
console.log(iter.next());   //{ value: [ 'b', 2 ], done: false }
console.log(iter.next());   //{ value: [ 'c', 3 ], done: false }
console.log(iter.next());   //{ value: undefined, done: true }

for(let i of obj){
    console.log(i);//[ 'a', 1 ] [ 'b', 2 ][ 'c', 3 ]
}
```

### 15-2、怎么利用生成器生成迭代器呢？

在函数function 后面 添加一个 *

```js
function* dome(){
    yield 'hello';
    yield 'world';
}
//调用generator函数，生成遍历器对象
let hw = dome();
console.log(hw.next());     //{ value: 'hello', done: false }
console.log(hw.next());     //{ value: 'world', done: false }
console.log(hw.next());     //{ value: undefined, done: true }
```

### 15-3、使用生成器遍历Obj

==是不是简练了许多==

```js
var obj = {
    a:1,
    b:2,
    c:3,
    [Symbol.iterator]: function* (){
        var index = 0;
        let map = new Map([["a",1],["b",2],["c",3]]);
        var mapEntries = [...map.entries()];
        while(index < mapEntries.length){
           yield mapEntries[index++];
        } 
    }
}

for(let i of obj){
    console.log(i);//[ 'a', 1 ] [ 'b', 2 ][ 'c', 3 ]
}
```





# 16、Promise

### 16-1、异步的解决方案-==事件轮询==

1. 由于JavaScript是一种单线程的设计模式，有很多时候，一个任务的操作时间会很长，导致后面的任务必须等待前面一个任务结束之后，才能进行下一个任务的执行。此时，就衍生与异步任务。
2. 事件轮询：是一种执行机制。
3. 比如下面这段代码：定时器是一个异步任务，js的事件执行机制，会将定时器这个任务压入到异步线程中。定时器时间到了之后，会将对应的这个回调函数放到==事件队列（消息队列）==当中，当同步事件执行完毕，JS通过轮询的方式，去查看==事件队列==当中函数的任务，也就是`consoleo.log(2)`，这就是异步任务通过轮询的方式执行的机制。

<img src="C:\Users\cn\AppData\Roaming\Typora\typora-user-images\image-20210906173829438.png" alt="image-20210906173829438" style="zoom: 80%;" />

### 16-2、Promise静态方法race all

==all:==方法用于处理多个Promise对象实例。

场景：两个Promise实例，经过2秒后，将两个实例的结果，通过Promise.all()，返回一个新的Promise对象p3.

```js
let p1 = new Promise((resolve,reject) => {
    setTimeout(() => {
        resolve(1)
    })
},1000)
let p2 = new Promise((resolve,reject) => {
    setTimeout(() => {
        resolve(2)
    })
},2000)
let p3 = Promise.all([p1,p2]);
p3.then(res => console.log(res));//[1,2]
```

==race:==那个先到那个先执行

场景：两个Promise实例，经过2秒后，将两个实例的结果，通过Promise.all()，返回一个新的Promise对象p3.

```js
let p1 = new Promise((resolve,reject) => {
    setTimeout(() => {
        resolve(1)
    })
},1000)
let p2 = new Promise((resolve,reject) => {
    setTimeout(() => {
        resolve(2)
    })
},2000)
let p3 = Promise.race([p1,p2]);
p3.then(res => console.log(res));//1
```







# 17、Promise最终产物==async\await==

`async` 是异步的意思，而 `await` 是 `async wait`的简写，即异步等待

### 17-1、为什么有Async/Await？

`Promise`虽然跳出了异步嵌套的怪圈，用链式表达更加清晰，但是我们也发现如果有大量的异步请求的时候，流程复杂的情况下，会发现充满了屏幕的`then`，看起来非常吃力，而ES7的Async/Await的出现就是为了解决这种复杂的情况

### 17-2、基于Promise的Async/await

**async/await是一对好基友，缺一不可，他们的出生是为Promise服务的**。可以说async/await是Promise的爸爸，进化版。

### 17-3、async的本质

**async声明的函数的==返回本质上是一个Promise==**。

```js
async function demo() {
  return "1"
}
console.log(demo()); //Promise { '1' }
```

### 17-4、相对于 Generator 而言 Async 的特性



1. Async内置执行器，Generator函数需要手动执行；
2. yield命令无约束；
3. 返回promise，更简洁，通过`then`回调可以拿到`async`内部的`return`返回语句；
4. 调用`async`函数后，返回的promise对象必须等待内部所有`await`对应的promise执行完，才会发生状态变化，除非中途遇到`return`语句；
5. 



# 18、module(四种模块规范)

### 18-1、前言-作用

#### 18-1-1、前言

​			在 ES6 之前，社区制定了一些模块加载方案，最主要的有 CommonJS 和 AMD 两种。前者用于服务器，后者用于浏览器。ES6 在语言标准的层面上，实现了模块功能，而且实现得相当简单，完全可以取代现有的 CommonJS 和 AMD 规范，成为浏览器和服务器通用的模块解决方案。

#### 18-1-2、==作用:==

​			对项目来讲，js的编写会很多，这个时候就需要module模块化的思想，将这些js代码分为多个模块，这些模块可能是独立的、也有可能是你引用了我的那个变量、函数.....又或者我引用了别的模块的什么什么。

​				所以module的作用就是，给这些模块化的js文件之间是如何建立起练习，做一个==桥梁==，

### 18-2、CommonJS方案

#### 18-2-1、概述

- CommonJS 方案：以==同步==的方式加载，解决服务器端的加载。但是如果在浏览器端，由于莫夸的加载是使用网络请求，因此使用异步加载的方式更合适。
- Node应用采用CommonJS模块开发。每个文件就是一个模块，有自己的作用域

#### 18-2-2、特点

- 所有代码都运行在模块作用域中，不会污染全局作用域；
- 模块可以多次加载，但是只会在第一次加载时运行一次。然后运行结果被缓存，以后再次加载，就直接读取缓存结果，要想让模块再次加载，必须清楚缓存；
- 模块加载的顺序，按照其在代码出现的顺序；

```js
//导出.js
var firstName = 'Michael';
var lastName = 'Jackson';
module.exports = {
    firstName, 
    lastName,
    foo() {
        console.log(123)
    }
}

//----------------
//导入.js
let {firstName, lastName} = require("./commonJs-export.js")
console.log(firstName,lastName);//Michael Jackson
```

### 18-3、AMD 方案

​		AMD：是以==异步==的方式进行模块的加载。模块的加载不影响后面语句的执行，所有依赖这个模块的语句都定义在一个回调函数里，等到加载完成后再执行回调函数。require.js 实现了 AMD 规范.

​		应用于浏览器环境。

### 18-4、CMD方案

​		CMD 方案，这种方案和 AMD 方案都是为了解决==异步==模块加载的问题，sea.js 实现了 CMD 规范。它和require.js的区别在于模块定义时对依赖的处理不同和对依赖模块的执行时机的处理不同。

### 18-5、ES6提出的方案

​		使用import和export的形式来导入导出模块。

使用这种`import`命令的时候，用户需要只带所要加载的变量名或者函数名，否则无法加载。

```js
//导出.js
export function area(radius) {
    return Math.PI * radius * radius;
}
export function circumference(radius) {
    return 2 * Math.PI * radius;
}
//-------------------
//导入.js
import { area, circumference } from './es6-export.js';
console.log('圆面积：' + area(4));  //圆面积：50.26548245743669
console.log('圆周长：' + circumference(14));//圆周长：87.96459430051421
```

​		export default - （可以为该匿名函数指定任意名字）

```js
//导出
export default function () {
  console.log('foo');
}
//导入
import customName from './export-default';
customName(); // 'foo
```



### 18-6、CommonJs和ES6两模块的差异

- CommonJS 输出的是一个值的拷贝，ES6模块输出的是值的引用。
- CommonJS 是运行是加载，ES6模块 是编译是输出接口；
- ES6模块是动态引用，并不会缓存值。



# 19、ajax

​		对 ajax 的理解是，它是一种异步通信的方法，通过直接由 js 脚本向服务器发起 http 通信，然后根据服务器返回的数据，更新网页的相应部分，而不用刷新整个页面的一种方法。

### 19-1、注意

1. 在后端当中是==不可以直接==使用ajax的
2. 所有的Ajax的通讯数据格式是==json==

### 19-2、干嘛用的？

利用JavaScript通过Ajax单独向服务器发送http请求的技术

### 19-3、Ajax的实现方式

Ajax的实现方式是基于==XHR（XMLHttpResquest）这个对象实现的==

### 19-4、使用的步骤

- 创建XHR对象；==(解决兼容性)==

  ```js
  var xhr = window.XMLHttpRequest ? new XMLHttpRequest() : new ActiveXObject('Microsoft.XMLHTTP');
  ```
  
- 发送Http ==（超文本传输协议）==请求：

  ```js
  xhr.open("请求的方式get\post","请求的地址",true);	//异步请求（参数3）
  xhr.open("请求的方式get\post","请求的地址",false);//同步请求（参数3）
  ```

  

- 接收服务响应的结果；

- 处理服务器返回的结果； 

- Jquery写法

  ```js
   	$.ajax({
            type:'post',
            url:'',
            async:ture,//async 异步  sync  同步
            data:data,//针对post请求
            dataType:'jsonp',
            success:function (msg) {
  
            },
            error:function (error) {
  
            }
  	})
  ```

### 19-5、get请求、post请求

==get和post请求的区别==：

- post更安全：post请求的参数，不会作为url的一部分，不会被缓存、保存在服务器日志和浏览器的记录之中；
- post发送的数据量更大，（get请求有url长度限制）；
- post请求发送更多的数据类型（何种类型的文件）；
- get请求只能发送ASCLL字符

==为什么现在除了get和post这两个请求之外，其他的不常用了？==

​		  p s: 因为现在很多都已经实现了前后端分离，数据通过网络传输，如果将所有的请求都按照功能划分，比如delete请求（删除数据），可能会存在而已篡改的风险。



# 20、数据结构 

### 20-1、栈

特点：后进先出，出栈的那一位必定是对顶上的，也就是栈顶出栈。是一种有序的数据集合

![image-20211004163928697](C:\Users\cn\AppData\Roaming\Typora\typora-user-images\image-20211004163928697.png)

简单的栈：==存在漏洞：s._arr.push(10) ，也可以进行push操作==

```js
class Stack {
    constructor() {
        this._arr = [];
    }
    //新增
    pushEl(el) {
        this._arr.push(el)
    }
    //移除栈顶元素
    popEl() {
        return this._arr.pop();
    }
    //返回栈顶的元素
    peekEl() {
        return this._arr[this._arr.length - 1]
    }
    //是否为空
    isEmpty() {
        return this._arr.length === 0;
    }
    //移除所有元素
    clear() {
        return this._arr = [];
    }
    //元素的个数
    size() {
        return this._arr.length;
    }
}
var s = new Stack();
s.pushEl(1);
s.pushEl(3);
s.pushEl(5);
s.pushEl(7);
s.popEl();
console.log(s.peekEl())
console.log(s._arr)
```

定义复杂的栈：==私有--WeakMap（）--==

```js
var Stack = (function () {
    var _arr = new WeakMap();
    return class Stack {
        constructor() {
            _arr.set(this, [])
        }
        //新增
        pushEl(el) {
            _arr.get(this).push(el)
        }
        //移除栈顶元素
        popEl() {
            return _arr.get(this).pop();
        }
        //返回栈顶的元素
        peekEl() {
            return _arr.get(this)[_arr.get(this).length - 1]
        }
        //是否为空
        isEmpty() {
            return _arr.get(this).length === 0;
        }
        //移除所有元素
        clear() {
            return _arr.get(this) = [];
        }
        //元素的个数
        size() {
            return _arr.get(this).length;
        }
    }
})();

var s = new Stack();
s.pushEl(1);
s.pushEl(3);
s.pushEl(5);
s.pushEl(7);
s.popEl();
console.log(s.peekEl()); //5
console.log(s.size()); //3
```



### 20-2、链表

链表分为：

1. 单向链表：

   — 线性的数据结构，通过对每个节点的指针找到下一个指针节点的列表，二终止于最后一个纸箱NULL的指针。

2. 双向链表：

   — 它的每个数据结点中都有两个指针，分别指向直接后继和直接前驱。所以，从双向链表中的任意一个结点开始，都可以很方便地访问它的前驱结点和后继结点。

   <img src="C:\Users\cn\AppData\Roaming\Typora\typora-user-images\image-20210926170351242.png" alt="image-20210926170351242" style="zoom:67%;" />

```js
class Node {
    constructor(element) {
        this.element = element;
        this.next = null;
    }
}

class LinkedList {
    constructor() {
        this.size = 0;
        this.head = null;
    }

    //找到当前处理节点的前一位
    getNode(index) {
        //如果传入的Index＜0或者≥链表的长度（跑出异常）
        if (index < 0 || index >= this.size) {
            throw new Error("out range");
        }
        //否则 返回最后一个节点
        let cur = this.head;
        for (var i = 0; i < index; i++) {
            cur = cur.next;
        }
        return cur;
    }

    //增加节点
    append(element) {
        //新增一个节点
        let node = new Node(element);
        /*
            - 如果：链表为空（就将该节点放在head上）
            - 否则：获取到链表的最后一个节点，将该节点放在最后一个节点上
        */
        if (this.head === null) {
            this.head = node;
        } else {
            let cur = this.getNode(this.size - 1); //获取最后一个节点
            cur.next = node; //最后一个节点的next 指向新增的节点
        }
        this.size++;
    }
    //增加指定位置的节点
    appendAt(position, element) {
        //判断如果插入的节点索引小于0或者大于链表长度（报错）
        if (position < 0 || position > this.size) {
            throw new Error("position out range");
        }
        let node = new Node(element);
        //如果插入的节点为第一位，直接讲this.head指向
        if (position === 0) {
            node.next = this.head; //把新增节点的next指向 当前节点原来head指向的节点
            this.head = node; //把head指向新增节点的后面
        } else {
            let pre = this.getNode(position - 1);
            node.next = pre.next; //把新增节点的next指向 当前节点原来next指向的节点
            pre.next = node; //把插入位置的原来的节点的next指向新增的Node后面
        }
        this.size++
    }
    //删除链表
    remove(position) {
        if (position < 0 || position >= this.size) {
            throw new Error("position out range");
        }
        let cur = this.head; //this.head 指向的就是第一位(做一个标识)
        //删除第1位（）
        if (position === 0) {
            this.head = cur.next; //将this.head 指向 第一位的next的指向，也就是第二位
        } else {
            let pre = this.getNode(position - 1);
            cur = pre.next; //删除节点的上一位的next指向为cur删除的节点
            pre.next = cur.next; //删除节点的上一位的next指向为删除的节点的next
        }
    }
    //查找指定元素的索引
    indexOf(element) {
        let cur = this.head;
        for (var i = 0; i < this.size; i++) {
            if (cur.element === element) {
                return i;
            }
            cur = cur.next;
        }
        return -1;
    }
}

let li = new LinkedList();
li.append(1);
li.append(2);
li.append(3);
// li.appendAt(2,5)
// li.appendAt(2,6)
// li.remove(2)
console.log(li.indexOf(1)); //0
console.log(li.indexOf(2)); //1
console.log(li.indexOf(3)); //2
// console.log(li.size);//4
// console.dir(li,{depth:100})
console.log(JSON.stringify(li))
```

### 20-3、队列

==队列：先进先出原则。队列在尾部添加新元素，并从顶部移出元素，最新添加的元素必须排在队列的末尾==

![image-20211004172303242](C:\Users\cn\AppData\Roaming\Typora\typora-user-images\image-20211004172303242.png)

```js
class Queue {
    constructor() {
        this._arr = new Array();
        this.front = 0;
        this.count = 0;
    }
    //查看队列头部元素
    peek() {
        return this._arr[this.front]
    }
    //判断队列是否为空
    isEmpty() {
        return this.count - this.front === 0;
    }
    //查看队列长度
    size() {
        return this.count - this.front;
    }
    //清除队列长度
    clear() {
        this.count = 0;
        this.front = 0;
        this._arr = []
    }
    //入队列
    enQueue(el) {
        this._arr[this.count] = el;
        this.count++
    }
    //出队列
    deQueue() {
        if (this.isEmpty()) {
            console.log("队列为空");
            return false;
        }
        let res = this._arr[this.front];
        delete this._arr[this.front];
        this.front++;
        return res;
    }
}
let queue = new Queue(5);
console.log(queue.isEmpty())
queue.enQueue(1)
queue.enQueue(2)
queue.enQueue(3)
queue.deQueue()
queue.deQueue()
console.log(queue)
console.log(queue.size())
```



### 20-4、循环队列

==循环队列：首位相连的队列，也含有队列的先进先出的特点==

<img src="C:\Users\cn\AppData\Roaming\Typora\typora-user-images\image-20211004172407137.png" alt="image-20211004172407137" style="zoom:50%;" />

```js
class CircleQueue {
    constructor(len) {
        this._arr = new Array(len + 1);
        this.front = 0; //首指针
        this.rear = 0; //尾指针
    }
    //判断队列是否为空(首尾指针重合了)
    isEmpty() {
        return this.front === this.rear;
    }
    //判断队列是否满()
    isFull() {
        return (this.rear + 1) % this._arr.length === this.front;
    }

    //入列操作
    enQueue(elem) {
        if (this.isFull()) {
            console.log("23:队列已满");
            return false;
        }
        this._arr[this.rear] = elem;
        this.rear = (this.rear + 1) % this._arr.length;
    }
    //出列操作
    deQueue() {
        if (this.isEmpty()) {
            console.log("队列为空");
            return false;
        }
        let item = this._arr[this.front];
        this._arr[this.front] = undefined;
        this.front = (this.front + 1) % this._arr.length;
        return item;
    }

    toString() {
        return this._arr
    }
}
var queue = new CircleQueue(5);
queue.enQueue(1);
queue.enQueue(2);
queue.enQueue(3);
queue.enQueue(4);
queue.enQueue(5);
console.log(queue.deQueue()); //1
console.log(queue.deQueue()); //2
console.log(queue.deQueue()); //3
queue.enQueue(6);
queue.enQueue(7);
queue.enQueue(8);
console.log(queue)
```



# 21、严格模式

ES6 的模块==自动==采用严格模式，不管你有没有在模块头部加上`"use strict";`。

严格模式主要有以下限制。

- 变量必须声明后再使用
- 函数的参数不能有同名属性，否则报错
- 不能使用`with`语句
- 不能对只读属性赋值，否则报错
- 不能使用前缀0表示八进制数，否则报错
- 不能删除不可删除的属性，否则报错
- 不能删除变量`delete prop`，会报错，只能删除属性`delete global[prop]`
- `eval`不会在它的外层作用域引入变量
- `eval`和`arguments`不能被重新赋值
- `arguments`不会自动反映函数参数的变化
- 不能使用`arguments.callee`
- 不能使用`arguments.caller`
- 禁止`this`指向全局对象
- 不能使用`fn.caller`和`fn.arguments`获取函数调用的堆栈
- 增加了保留字（比如`protected`、`static`和`interface`）



# 22、JSON中的两个内置对象方法

### 22-1、JSON.stringify(对象转化为字符串)

==任何把 JavaScript 变成 Json ，就是把这个对象序列化为Json字符串==

```js
JSON.stringify( {} , [ ] , "")
//参数一 ：要序列化的数据（object）
//参数二 ：控制对象的键值，只想输出指定的属性，传入一个数组
//参数三 ：序列化后，打印输出的格式（一个Tab ，可以更直观查看json）
```

### 22-2、JSON.parse(字符串转换为对象)

==如果我们收到一个JSON格式的字符串，只需要把它反序列化成一个JavaScript对象，就可以在JavaScript中直接使用这个对象了==



# 23、JS中隐式转化

### 23-1、介绍

​			在JavaScript的机制中，运算符的两边数据类型不统一，编译器会自动进行数据类型的转化；

​			例如：1 > "0", 编译器会自动将右边的字符“0” -> 转成Number 0

### 23-2、隐式转化规则

#### 23-2-1. 对象和布尔值比较

对象和布尔值进行比较时，对象先转换为字符串，然后再转换为数字，布尔值直接转换为数字

```
[] == true;  //false  []转换为字符串'',然后转换为数字0,true转换为数字1，所以为false
```

#### 23-2-2. 对象和字符串比较

对象和字符串进行比较时，对象转换为字符串，然后两者进行比较。

```
[1,2,3] == '1,2,3' // true  [1,2,3]转化为'1,2,3'，然后和'1,2,3'， so结果为true;
```

#### 23-2-3. 对象和数字比较

对象和数字进行比较时，对象先转换为字符串，然后转换为数字，再和数字进行比较。

```
[1] == 1;  // true  `对象先转换为字符串再转换为数字，二者再比较 [1] => '1' => 1 所以结果为true
```

#### 23-2-4. 字符串和数字比较

字符串和数字进行比较时，字符串转换成数字，二者再比较。

```
'1' == 1 // true
```

#### 23-2-5. 字符串和布尔值比较

字符串和布尔值进行比较时，二者全部转换成数值再比较。

```
'1' == true; // true 
```

#### 23-2-6. 布尔值和数字比较

布尔值和数字进行比较时，布尔转换为数字，二者比较。

```
true == 1 // true
```





# 24、正则

### 24-1、正则是用来搞什么的？

正则：是用来处理（匹配）字符串的语法体系，

### 24-2、正则匹配的方法

#### 24-2-1、test()  

在字符串中查找符合正则的内容，若查找到返回true,反之返回false。用法：正则.test(字符串)

#### 24-2-2、search()  

在字符串搜索符合正则的内容，搜索到就返回出现的位置（从0开始，如果匹配的不只是一个字母，那只会返回第一个字母的位置）， 如果搜索失败就返回 -1

#### 24-2-3、match() 

在字符串中搜索复合规则的内容，搜索成功就返回内容，格式为数组，失败就返回null

#### 24-2-4、replace() 

查找符合正则的字符串，就替换成对应的字符串。返回替换后的内容

#### 24-2-5、 exec()

和match方法一样，搜索符合规则的内容，并返回内容，格式为数组。



### 24-3、字符规则

#### 24-3-1、元字符

有着特殊语义的字符==.   []  [^]  ? *  +  {min,max} ^  $  ()  \1\2  |==

#### 24-3-2、转义字符  \

用来转化元字符的，因为元字符是有特殊语义的，当我们需要用元字符以 ==字符串==的 方式匹配，此时就可以用转义字符来处理

#### 24-3-3、范围-字符组 ==[]==

```js
console.log(/[1-9]/.test("12"));//true
console.log(/[1-9]/.test("0"));//false
console.log(/[a-z]/.test("b")); //true
console.log(/[1-9a-zA-Z]/.test("B"));//true
// - 表示匹配的字符规则（1~9）的字符
```

#### 24-3-3、范围取反-非字符组 ==[^]==

```js
console.log(/[^1-9]/.test("1")); //false
console.log(/[^1-9]/.test("0")); //true
console.log(/[^1-9]/.test("b")); //true
console.log(/[^1-9]/.test("B")); //true
```

#### 24-3-4、字符组的简写

```js
//1、    \d  -   [0-9]
console.log(/\d/.test("9"));	//true

//2、    \D  -   [^0-9]
console.log(/\D/.test("9"));//false
console.log(/\D/.test("a"));//true

//3、    \w  -   [0-9A-Za-z]
console.log(/\w/.test("a"));//true

//4、    \W  -   [^0-9A-Za-z]
console.log(/\W/.test("a"));//false
console.log(/\W/.test("%"));//true

//5、    \s  -   [\f\n\r\t...](非打印字符)
console.log(/\s/.test("\f"));//false

//6、    \S  -   [^\f\n\r\t...](空白字符)
console.log(/\S/.test("a"));//true
```

#### 24-3-5、量词

```js
//1-表示 \d的字符规则要出现 -- 6位
console.log(/\d{6}/.exec("1234567")); //123456
console.log(/\d{6}/.exec("123")); //null

//2-表示 \d的字符规则要出现 -- 6位到9位
console.log(/\d{6,9}/.exec("123456")); //123456
console.log(/\d{6,9}/.exec("12345678910")); //123456789

//3-表示 \d的字符规则要出现 -- 6位及6位以上
console.log(/\d{6,}/.exec("123456")); //123456
console.log(/\d{6,}/.exec("12345678")); //12345678
```

#### 24-3-6、量词-简写方式(贪婪模式) - 默认

==贪婪模式:**让正则表达式尽可能多的匹配，直到匹配失败**==

``` js
//1 ->    ?  :  {0,1} (0次或者1次)
//2 ->    *  :  {0,}  (0次或者多次)
//3 ->    +  :  {1,}  (无穷次)

console.log(/a?/.exec("a"));	 //[ 'a', index: 0, input: 'a', groups: undefined ]
console.log(/a*/.exec("aaa"));	 //[ 'aaa', index: 0, input: 'aaa', groups: undefined ]
console.log(/a+/.exec("aaa")) 	 //[ 'aaa', index: 0, input: 'aaa', groups: undefined ]
```

#### 24-3-7、量词-简写方式(非贪婪模式)

==非贪婪模式:让正则表达式尽可能少的匹配，也就是说一旦成功匹配不再继续尝试==

```js
console.log(/a??/.exec("a"));	 //[ '', index: 0, input: 'a', groups: undefined ]
console.log(/a*?/.exec("aaa"));  //[ '', index: 0, input: 'aaa', groups: undefined ]
console.log(/a+?/.exec("aaa"))   //[ 'a', index: 0, input: 'aaa', groups: undefined ]
```

#### 24-3-8、任意字符==.==

```js
console.log(/./.test("asd231"));//true
console.log(/./.test("\r"));//false
```

#### 24-3-9、括号的用法1-分组

```js
console.log(/ab{2}/.test("abb"));//true（量词修饰前面一个元素b）
//需求：让ab出现两次（也就是说量词修饰整一个ab）
console.log(/(ab){2}/.exec("abab"));//true
```

==应用：利用正则取出日期的年月日==

<img src="C:\Users\cn\AppData\Roaming\Typora\typora-user-images\image-20210930175915526.png" alt="image-20210930175915526" style="zoom: 80%;" />

#### 24-3-10、括号的用法2-引用





# 25、&& 、 ||和!! 运算符

- `&&` 叫逻辑与，==都为真==
- `||` 叫逻辑或，==只要一个为真==
- `!!` 运算符可以将右侧的值强制转换为布尔值，这也是将值转换为布尔值的一种简单方法。



# 26、数组和字符串的原生方法

<img src="C:\Users\cn\AppData\Roaming\Typora\typora-user-images\image-20211015163501179.png" alt="image-20211015163501179" style="zoom: 67%;" />

<img src="C:\Users\cn\AppData\Roaming\Typora\typora-user-images\image-20211015163517643.png" alt="image-20211015163517643" style="zoom: 50%;" />

# 27、V8引擎的垃圾回收机制



# 28、SCMAScript（ES6）新增的特性

- 块作用域
- 类
- 箭头函数
- 模板字符串
- 加强的对象字面
- 对象解构
- Promise
- 模块
- Symbol
- 代理（proxy）Set
- 函数默认参数
- rest 和展开

# 29、类数组转成数组的方式

```js
//一、Array.from 
Array.from(document.getElemenByClassName("li"));

//二、Array.prototype.slice.call()
Array.prototype.slice.call(document.getElemenByClassName("li"));

//三、扩展运算符
[...document.getElemenByClassName("li")];

//四、concat
Array.prototype.concat.apply([],document.getElemenByClassName("li"));
```

