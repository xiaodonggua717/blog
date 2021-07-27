# ES6基础知识  2021.5.19

## let

### 块级作用域

与var相比 let声明的变量只在所处于的块级内有效，即let的关键字声明的变量具有块级作用域。

```js
if(true){
    let b = 10;
    console.log(b); //10
    if(true){
        let c = 30;
    }
    console.log(c); // ReferenceError
}
console.log(b); // ReferenceError
```

可以防止循环变量变为全局变量

```js
for (let i = 0; i < 2; i++) {

}
console.log(i); // ReferenceError
```

### 不存在变量提升

let 不存在变量提升

```js
console.log(a); //ReferenceError
let a = 'hello'; 
```

### 暂时性死区

只要块级作用域内存在`let`命令，它所声明的变量就“绑定”（binding）这个区域，不再受外部的影响。

```js
var tmp =123;
if(true){
    tmp='hello';  // ReferenceError
    let tmp
}
```

### 题目

此时输出为  2  2 原因是此时的i虽然是循环变量但是由于是var定义的变量所以是全局变量,当循环结束时i已经变成了2,所以当循环结束时再去调用function()可以直接使用全局变量i 所以输出的都是2。

```js
var arr = [];
for (var i = 0; i < 2; i++) {
    arr[i] = function () {
        console.log(i);
    }
}
arr[0](); //2
arr[1](); //2
```

而把var改为let时 不同的i处于不同的块级作用域中 当函数执行时，函数内部没有自己的i变量 就会向上寻找，函数的上一级作用域就是循环产生的块级作用域。所以输出的就是对应块级作用域中的i值

```js
let arr = [];
for (let i = 0; i < 2; i++) {
    arr[i] = function () {
        console.log(i);
    }
}
arr[0]();  // 0 
arr[1]();  // 1
```

![image-20210519205759768](C:\Users\ASUS\AppData\Roaming\Typora\typora-user-images\image-20210519205759768.png)

## const

声明常量，常量就是值（内存地址）不能变化的量。

const实际上保证的，并不是变量的值不得改动，而是变量指向的那个内存地址所保存的数据不得改动。对于简单类型的数据，值就保存在变量指向的那个内存地址，因此等同于常量。但对于复合类型的数据（对象和数组），变量指向的内存地址，保存的只是一个指向实际数据的指针，`const`只能保证这个指针是固定的，即它指向的地址不会发生改变，至于它指向的数据结构是不是可变的，就完全不能控制了。

和let一样具有块级作用域，具有暂时性死区，但const在声明时必须赋初值。

const在声明常量之后，常量的值不可更改。

## 

![image-20210519210816325](C:\Users\ASUS\AppData\Roaming\Typora\typora-user-images\image-20210519210816325.png)

## 六种声明变量的方法

ES5 ：	var	function

ES6 ：	 let	const	import	class

## 关于顶层对象属性

顶层对象，在浏览器环境指的是`window`对象，在 Node 指的是`global`对象。ES5当中顶层对象的属性和全局变量是等价。

ES6 规定：

var命令和function命令声明的全局变量，依旧是顶层对象的属性；

let命令、const命令、class命令声明的全局变量，不属于顶层对象的属性。。

## 解构赋值

ES6允许从数组和对象中提取值来对变量赋值。

### 数组解构赋值

按照模式匹配来进行赋值

```js
let [a,b,c] = [1,2,3];
console.log(a); //1
console.log(b); //2
console.log(c); //3

let [foo, [[bar], baz]] = [1, [[2], 3]];
foo // 1
bar // 2
baz // 3

let [ , , third] = ["foo", "bar", "baz"];
third // "baz"

let [x, , y] = [1, 2, 3];
x // 1
y // 3

let [head, ...tail] = [1, 2, 3, 4];
head // 1
tail // [2, 3, 4]

let [x, y, ...z] = ['a'];
x // "a"
y // undefined
z // []
```



如果赋值数组的对应位置发生了缺失，那么被赋值数组缺失位置的变量等于undefined。

如果等号左边的模式，只匹配一部分的等号右边的数组。这种情况下，解构依然可以成功。

```js
let [x, y] = [1, 2, 3];
x // 1
y // 2

let [a, [b], d] = [1, [2, 3], 4];
a // 1
b // 2
d // 4
```

### 对象的解构赋值

对象的解构赋值中变量必须与属性同名，才能取到正确的值。

```js
let person = {name:'tk'}
let {name:myName} = person;
console.log(myName); //tk
```

实际上对象的解构赋值是下面形式的简写

```js
let { foo: foo, bar: bar } = { foo: 'aaa', bar: 'bbb' };
```

即对象结构赋值的内部机制是先找到同名属性,然后再赋给对应的变量。

即被赋值的其实是后者。

### 默认值

如果数组或对象中存在默认值，那么如果它没有被赋值则仍为默认值，如果被赋值则会被替代为被赋予的值。（即如果你希望默认值生效，那么条件是，对象的属性值严格等于undefined）

**应该注意的是：**如果按照以下的方式去解构赋值则会出错：

```js
// 错误的写法
let x;
{x} = {x: 1};
// SyntaxError: syntax error
```

因为JavaScript引擎会将{x}理解成一个代码块从而发生语法错误。

## 箭头函数

箭头函数是用来简化函数定义语法的

```js
() => {}
const fn = () => {}
```

可以给变量声明为箭头函数，通过调用变量的方式来调用箭头函数。

如果函数体里面只有一句代码并且代码的执行结果就是函数的返回值，那么函数体的大括号可以省略

如 

```js
const fn = (n1,n2) = > n1+n2; 
```



 如果形参只有一个，那么（）也可以省略

即

```js
const fn = v => v;
//等同于
const fn = function fn1 (v){
    return v;
}
```

箭头函数不绑定this关键字，箭头函数的this指向的是函数定义位置的上下文this

```js
const obj = {name :"tk"}
function fn (){
    console.log(this);  //obj
    return () => {
        console.log(this);  //obj
    }
}
const resFn = fn.call(obj);
resFn();
```

### 题目

```js
var obj = {
    age = 20,
    say: () => {
        console.log(this.age);
    }
}
obj.say(); //输出的是undefined
```

因为箭头函数没有自己的this,此时this指向的是obj,obj是一个对象不能产生作用域.所以this指向了全局作用域 window 弹出的就是undefined 

### 剩余参数

剩余参数语法允许我们将一个不定数目的参数表示为一个数组

箭头函数中无法使用argument[]

```js
fuction sum (first,...args) 
{
    console.log(first);    //10 
    console.log(args);     //[20,30]
}
sum(10,20,30)
```

```js
const sum = (...args) => {
    let total = 0;
    args.forEach(item => total+= item)
    return total;
}
console.log(sum(10,20,30)) //60
```

## Array扩展方法

### 扩展运算符

扩展运算符是 三个点(...) 类似于rest参数的逆运算,将一个数组转为用逗号分隔的参数序列

```js
let ary = ["a","b","c"]; //ary = "a","b","c";
console.log(ary) // console.log("a","b","c");  此时用于分隔的逗号被视为是参数分割符  所以输出的是 a b c

console.log(...[1, 2, 3])
// 1 2 3

console.log(1, ...[2, 3, 4], 5)
// 1 2 3 4 5

[...document.querySelectorAll('div')]
// [<div>, <div>, <div>]
```

扩展运算符可用于合并数组

```js
方法1:
let ary1= [1,2,3];
let ary2= [2,3,4];
let ary3 = [...ary1,...ary2];
//ary3 = 1,2,3,2,3,4

方法2:
let ary1= [1,2,3];
let ary2= [2,3,4];
let ary3 = ary1.push(...ary2);
```

扩展运算符可以将伪数组转为真正的数组

### 构造函数方法: Array.from()

```js
let arrayLike = {
    '0' : 'a';
    '1' : 'b';
}
let arr1 = Array.from(arrayLike);
```

### 数组实例方法 find()

用于找出第一个符合条件的数组成员 若没找到则返回undefined

```js
[1, 5, 10, 15].find(function(value, index, arr) {
  return value > 9;
}) // 10
```

findIndex()方法与find非常类似,但是它返回的是第一个符合条件的数组成员的位置,如果没找到就返回-1

与indexOf()方法相比,这两种方法全部都可以借助`Object.is`方法找到NaN;

```javascript
[NaN].indexOf(NaN)
// -1

[NaN].findIndex(y => Object.is(NaN, y))
// 0
```

### 数组实例方法 inclues()

该方法返回一个布尔值，表示某个数组是否包含给定的值，与字符串的`includes`方法类似。

```javascript
[1, 2, 3].includes(2)     // true
[1, 2, 3].includes(4)     // false
[1, 2, NaN].includes(NaN) // true
```

该方法的第二个参数表示搜索的起始位置，默认为`0`。

如果第二个参数为负数，则表示倒数的位置，如果这时它大于数组长度（比如第二个参数为`-4`，但数组长度为`3`），则会重置为从`0`开始。

```javascript
[1, 2, 3].includes(3, 3);  // false
[1, 2, 3].includes(3, -1); // true
```

与includes()方法相比,indexOf()有两个缺点:

1. 不够语义化
2. 不能发现NaN

但是includes()方法不一定会受当前环境支持,如果不支持的话可以部署一个简易的替代版本

```javascript
const contains = (() =>
  Array.prototype.includes? (arr, value) => arr.includes(value) : (arr, value) => arr.some(el => el === value)
)();
contains(['foo', 'bar'], 'baz'); // => false
```

## String扩展方法

### 模板字符串

 这有些类似于c语言

```js
let name = 'tk';
let myName = `hello,我的名字叫${name}`
```

### startsWith()和endsWith()

startsWith()表示参数字符串是否在原字符串的头部,返回布尔值

endsWith()表示参数字符串是否在原字符串的尾部,返回布尔值

### repeat()

表示将原来的字符串重复n次, 返回一个新字符串

```js
let y ='x'.repeat(3);
console.log(y) //xxx
```

## Set数据结构

类似于数组,是一组数据的结合,但是它没有重复的值

### set的方法

`add(value)`：添加   返回set结构本身

set函数可以接受一个数组来作为参数用以初始化 另外 两个空的对象不相等,会被视为两个值

`delete(value)`： 删除一个值返回布尔值 表明是否删除成功

`has(value)`：返回一个布尔值表示该值是否为set的成员

`clear()`：清除所有成员

### set遍历

set的实例有四个遍历方法

- `Set.keys()`：返回键名的遍历器

- `Set.values()`：返回键值的遍历器

  由于 Set 结构没有键名，只有键值（或者说键名和键值是同一个值），所以`keys`方法和`values`方法的行为完全一致。

- `Set.entries()`：返回键值对的遍历器

- `Set.forEach()`：使用回调函数遍历每个成员

```javascript
let set = new Set(['red', 'green', 'blue']);

for (let item of set.keys()) {
  console.log(item);
}
// red
// green
// blue

for (let item of set.values()) {
  console.log(item);
}
// red
// green
// blue

for (let item of set.entries()) {
  console.log(item);
}
// ["red", "red"]
// ["green", "green"]
// ["blue", "blue"]
```

## Map

Map其实是也是一种键值对的集合(HASH结构) ,传统的Object只可以用字符串来当作键。这就会产生很大的限制

Map“键”的范围不限于字符串，各种类型的值（包括对象）都可以当作键。也就是说，Object 结构提供了“字符串—值”的对应，Map 结构提供了“值—值”的对应，是一种更完善的 Hash 结构实现。

```javascript
const m = new Map();
const o = {p: 'Hello World'};

m.set(o, 'content')
m.get(o) // "content"

m.has(o) // true
m.delete(o) // true
m.has(o) // false
```

作为构造函数，Map 也可以接受一个数组作为参数。该数组的成员是一个个表示键值对的数组。

```javascript
const map = new Map([
  ['name', '张三'],
  ['title', 'Author']
]);

map.size // 2
map.has('name') // true
map.get('name') // "张三"
map.has('title') // true
map.get('title') // "Author"
```

**注**：只有对同一个对象的引用，Map 结构才将其视为同一个键。这一点要非常小心。

```javascript
const map = new Map();
map.set(['a'], 555);
map.get(['a']) // undefined
```

```javascript
let map = new Map();

map.set(-0, 123);
map.get(+0) // 123

map.set(true, 1);
map.set('true', 2);
map.get(true) // 1

map.set(undefined, 3);
map.set(null, 4);
map.get(undefined) // 3

map.set(NaN, 123);
map.get(NaN) // 123
```

### map实例的属性和操作方法

size属性 ：`size`属性返回 Map 结构的成员总数。

**Map..set(key, value)**  ：`set`方法设置键名`key`对应的键值为`value`，然后返回整个 Map 结构。如果`key`已经有值，则键值会被更新，否则就新生成该键。

```javascript
const m = new Map();

m.set('edition', 6)        // 键是字符串
m.set(262, 'standard')     // 键是数值
m.set(undefined, 'nah')    // 键是 undefined
```

可以采用链式写法

```javascript
let map = new Map()
  .set(1, 'a')
  .set(2, 'b')
  .set(3, 'c');
```

**Map.prototype.get(key)**

`get`方法读取`key`对应的键值，如果找不到`key`，返回`undefined`。

**Map.prototype.has(key)**

`has`方法返回一个布尔值，表示某个键是否在当前 Map 对象之中。

**Map.prototype.delete(key)**

`delete`方法删除某个键，返回`true`。如果删除失败，返回`false`。

**Map.prototype.clear()**

`clear`方法清除所有成员，没有返回值。

### Map的遍历方法

- `Map.prototype.keys()`：返回键名的遍历器。
- `Map.prototype.values()`：返回键值的遍历器。
- `Map.prototype.entries()`：返回所有成员的遍历器。
- `Map.prototype.forEach()`：遍历 Map 的所有成员。

## WeakSet 和WeakMap

与set和map相比有两点区别：

weak只接受对象作为键名

且weak为弱引用，不能遍历，且不会计入垃圾回收机制，不能清空

`WeakMap`的设计目的在于，有时我们想在某个对象上面存放一些数据，但是这会形成对于这个对象的引用。请看下面的例