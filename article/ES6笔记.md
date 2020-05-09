# ES6速查
## 块作用域声明
- let 声明变量
- const 声明常量
- 以上均不存在变量提升的问题
- 全局变量和块级变量相同，则以块级变量有限，暂时性死区
- 不允许重复声明
- var命令和function命令声明的全局变量，依旧是顶层对象的属性
- let命令、const命令、class命令声明的全局变量，不属于顶层对象的属性
- 浏览器里面，顶层对象是window， Node 里面，顶层对象是global


## spread/rest
- ...对象
- ...数组

## 默认参数值

```
function foo(x = 1, y = 2) {
    ...
}
```

## 解构
- 对象解构

```
let a = {
    aa: 123,
    bb: 123
}

const { aa, bb } = a;
const { aa:aa, bb:bb } = a;
const { XX:aa, YY:bb } = a;
```

- 数组解构

```
let a = [1, 2, 3];

const [x, y, z] = a;
```
- 字符串解构

```
const [a, b, c, d, e] = 'hello';
```
- 数值和bool值解构

```
let {toString: s} = 123;
s === Number.prototype.toString // true

let {toString: s} = true;
s === Boolean.prototype.toString // true
```
- 函数解构
```
function add([x, y]){
  return x + y;
}

add([1, 2]);
```
用途：
- 交换变量值：[x, y] = [y, x]
- 返回函数多个值：const [x, y, z] = Func()
- 定义函数参数：Func([1, 2])
- 提取JSON数据：const { name, version } = packageJson
- 定义函数参数默认值：function Func({ x = 1, y = 2 } = {}) {}
- 遍历Map结构：for (let [k, v] of Map) {}
- 输入模块指定属性和方法：const { readFile, writeFile } = require("fs")

## 字符串扩展
- Unicode表示法：
```
"\u{20BB7}"
// "𠮷"

"\u{41}\u{42}\u{43}"
// "ABC"

let hello = 123;
hell\u{6F} // 123

'\u{1F680}' === '\uD83D\uDE80'

//JavaScript 共有 6 种方法可以表示一个字符。
'\z' === 'z'  // true
'\172' === 'z' // true
'\x7A' === 'z' // true
'\u007A' === 'z' // true
'\u{7A}' === 'z' // true
```
- 字符串的遍历器接口
```
for (let codePoint of 'foo') {
  console.log(codePoint)
}
```
- 模板字符串

```
const a = `${aaa}`
```

## 字符串的新增方法
- String.fromCharCode()
```
String.fromCharCode(0x20BB7)
// "ஷ"
```
- String.fromCodePoint()
```
//可以识别大于0xFFFF的字符，弥补了String.fromCharCode()方法的不足。在作用上，正好与下面的codePointAt()方法相反
String.fromCodePoint(0x20BB7)
// "𠮷"
String.fromCodePoint(0x78, 0x1f680, 0x79) === 'x\uD83D\uDE80y'
// true
```
- String.raw()
```
//方法可以作为处理模板字符串的基本方法，它会将所有变量替换，而且对斜杠进行转义，方便下一步作为字符串来使用
// `foo${1 + 2}bar`
// 等同于
String.raw({ raw: ['foo', 'bar'] }, 1 + 2) // "foo3bar"

```
- codePointAt()
```
//返回一个字符的码点
let s = '𠮷a';

s.codePointAt(0) // 134071
s.codePointAt(1) // 57271

s.codePointAt(2) // 97
```
- includes()：返回布尔值，表示是否找到了参数字符串
- startsWith()：返回布尔值，表示参数字符串是否在原字符串的头部
- endsWith()：返回布尔值，表示参数字符串是否在原字符串的尾部
- repeat()

```
//返回一个新字符串，表示将原字符串重复n次
//如果repeat的参数是负数或者Infinity，会报错。
//参数NaN等同于 0
//如果repeat的参数是字符串，则会先转换成数字
//参数如果是小数，会被取整
'x'.repeat(3) // "xxx"
'hello'.repeat(2) // "hellohello"
'na'.repeat(0) // ""
```
- padStart(), padEnd()
```
//padStart()用于头部补全，padEnd()用于尾部补全
'x'.padStart(5, 'ab') // 'ababx'
'x'.padStart(4, 'ab') // 'abax'

'x'.padEnd(5, 'ab') // 'xabab'
'x'.padEnd(4, 'ab') // 'xaba'
```
- trimStart(), trimEnd()
- matchAll()方法返回一个正则表达式在当前字符串的所有匹配

## 数字的扩展
- 二进制和八进制表示法，从 ES5 开始，在严格模式之中，八进制就不再允许使用前缀0表示，ES6 进一步明确，要使用前缀0o表示
- Number.isFinite()， Number.isNaN()
```
//Number.isFinite()用来检查一个数值是否为有限的（finite），即不是Infinity
Number.isFinite(15); // true
Number.isFinite(0.8); // true
Number.isFinite(NaN); // false
Number.isFinite(Infinity); // false
Number.isFinite(-Infinity); // false
Number.isFinite('foo'); // false
Number.isFinite('15'); // false
Number.isFinite(true); // false

//Number.isNaN()用来检查一个值是否为NaN
Number.isNaN(NaN) // true
Number.isNaN(15) // false
Number.isNaN('15') // false
Number.isNaN(true) // false
Number.isNaN(9/NaN) // true
Number.isNaN('true' / 0) // true
Number.isNaN('true' / 'true') // true
```
- parseInt()， parseFloat()

```
// ES6的写法
Number.parseInt('12.34') // 12
Number.parseFloat('123.45#') // 123.45
```
- Number.isInteger()

```
//由于 JavaScript 采用 IEEE 754 标准，数值存储为64位双精度格式，数值精度最多可以达到 53 个二进制位（1 个隐藏位与 52 个有效位）。如果数值的精度超过这个限度，第54位及后面的位就会被丢弃，这种情况下，Number.isInteger可能会误判
Number.isInteger(25) // true
Number.isInteger(25.1) // false
```
- Number.EPSILON

```
//表示 1 与大于 1 的最小浮点数之间的差
//Number.EPSILON实际上是 JavaScript 能够表示的最小精度。误差如果小于这个值，就可以认为已经没有意义了，即不存在误差了
0.1 + 0.2
// 0.30000000000000004

0.1 + 0.2 - 0.3
// 5.551115123125783e-17

5.551115123125783e-17.toFixed(20)
// '0.00000000000000005551'

Number.EPSILON可以用来设置“能够接受的误差范围”。比如，误差范围设为 2 的-50 次方（即Number.EPSILON * Math.pow(2, 2)），即如果两个浮点数的差小于这个值，我们就认为这两个浮点数相等

5.551115123125783e-17 < Number.EPSILON * Math.pow(2, 2)

function withinErrorMargin (left, right) {
  return Math.abs(left - right) < Number.EPSILON * Math.pow(2, 2);
}

0.1 + 0.2 === 0.3 // false
withinErrorMargin(0.1 + 0.2, 0.3) // true

1.1 + 1.3 === 2.4 // false
withinErrorMargin(1.1 + 1.3, 2.4) // true

```
- Number.isSafeInteger()
```
//引入了Number.MAX_SAFE_INTEGER和Number.MIN_SAFE_INTEGER这两个常量
//判断 JavaScript 能够精确表示的极限
Number.isSafeInteger('a') // false
Number.isSafeInteger(null) // false
Number.isSafeInteger(NaN) // false
Number.isSafeInteger(Infinity) // false
Number.isSafeInteger(-Infinity) // false

Number.isSafeInteger(3) // true
Number.isSafeInteger(1.2) // false
Number.isSafeInteger(9007199254740990) // true
Number.isSafeInteger(9007199254740992) // false

Number.isSafeInteger(Number.MIN_SAFE_INTEGER - 1) // false
Number.isSafeInteger(Number.MIN_SAFE_INTEGER) // true
Number.isSafeInteger(Number.MAX_SAFE_INTEGER) // true
Number.isSafeInteger(Number.MAX_SAFE_INTEGER + 1) // false
```
- Math.trunc(),方法用于去除一个数的小数部分，返回整数部分
- Math.sign方法用来判断一个数到底是正数、负数、还是零。对于非数值，会先将其转换为数值

```
参数为正数，返回+1；
参数为负数，返回-1；
参数为 0，返回0；
参数为-0，返回-0;
其他值，返回NaN
```
- Math.cbrt(), 法用于计算一个数的立方根
```
Math.cbrt(-1) // -1
Math.cbrt(0)  // 0
Math.cbrt(1)  // 1
Math.cbrt(2)  // 1.2599210498948732
```
- Math.clz32()方法将参数转为 32 位无符号整数的形式，然后返回这个 32 位值里面有多少个前导 0

```
Math.clz32(0) // 32
Math.clz32(1) // 31
Math.clz32(1000) // 22
Math.clz32(0b01000000000000000000000000000000) // 1
Math.clz32(0b00100000000000000000000000000000) // 2
```
- Math.imul方法返回两个数以 32 位带符号整数形式相乘的结果，返回的也是一个 32 位的带符号整数,JavaScript 无法保存额外的精度，就把低位的值都变成了 0。Math.imul方法可以返回正确的值 1

- Math.fround方法返回一个数的32位单精度浮点数形式
- Math.hypot方法返回所有参数的平方和的平方根
- 指数运算符（**）
```
2 ** 2 // 4
2 ** 3 // 8
```
- BigInt(大整数)
> BigInt 对象继承了 Object 对象的两个实例方法

```
BigInt.prototype.toString()
BigInt.prototype.valueOf()
```
> 继承了 Number 对象的一个实例方法

```
BigInt.prototype.toLocaleString()
```
> Boolean()、Number()和String()这三个方法，将 BigInt 可以转为布尔值、数值和字符串类型

## 函数的扩展
- 函数的默认值
- 函数的length属性， 参数的个数，默认值Length无效
```
(function (a) {}).length // 1
(function (a = 5) {}).length // 0
(function (a, b, c = 5) {}).length // 2
```
- 只要函数参数使用了默认值、解构赋值、或者扩展运算符，那么函数内部就不能显式设定为严格模式，否则会报错

- 函数的name属性，返回该函数的函数名

```
unction foo() {}
foo.name // "foo"
```
- ES6 允许使用“箭头”（=>）定义函数

```
 (1）函数体内的this对象，就是定义时所在的对象，而不是使用时所在的对象。

（2）不可以当作构造函数，也就是说，不可以使用new命令，否则会抛出一个错误。

（3）不可以使用arguments对象，该对象在函数体内不存在。如果要用，可以用 rest 参数代替。

（4）不可以使用yield命令，因此箭头函数不能用作 Generator 函数。

// ES6
function foo() {
  setTimeout(() => {
    console.log('id:', this.id);
  }, 100);
}

// ES5
function foo() {
  var _this = this;

  setTimeout(function () {
    console.log('id:', _this.id);
  }, 100);
}
```
## 数组的扩展
- 扩展运算符（spread）是三个点（...）

```
1. 数组是复合的数据类型，直接复制的话，
只是复制了指向底层数据结构的指针，而不是克隆一个全新的数组
ES5 只能用变通方法来复制数组
const a1 = [1, 2];
const a2 = a1.concat();

a2[0] = 2;
a1 // [1, 2]

扩展运算符提供了复制数组的简便写法
const a1 = [1, 2];
// 写法一
const a2 = [...a1];
// 写法二
const [...a2] = a1;

2. 合并数组
[...arr1, ...arr2, ...arr3]

3. 与解构赋值结合
[a, ...rest] = list

4. 字符串
[...'hello']

5. 实现了 Iterator 接口的对象
let nodeList = document.querySelectorAll('div');
let array = [...nodeList];

6. Map 和 Set 结构，Generator 函数
let map = new Map([
  [1, 'one'],
  [2, 'two'],
  [3, 'three'],
]);

let arr = [...map.keys()]; // [1, 2, 3]

const go = function*(){
  yield 1;
  yield 2;
  yield 3;
};

[...go()] // [1, 2, 3]

```
- Array.from()

```
方法用于将两类对象转为真正的数组：类似数组的对象（array-like object）和可遍历（iterable）的对象（包括 ES6 新增的数据结构 Set 和 Map）

Array.from('hello')
// ['h', 'e', 'l', 'l', 'o']

let namesSet = new Set(['a', 'b'])
Array.from(namesSet) // ['a', 'b']

Array.from还可以接受第二个参数，作用类似于数组的map方法，用来对每个元素进行处理，将处理后的值放入返回的数组
Array.from(arrayLike, x => x * x);
// 等同于
Array.from(arrayLike).map(x => x * x);

Array.from([1, 2, 3], (x) => x * x)
// [1, 4, 9]
```
- Array.of方法用于将一组值，转换为数组。

```
Array.of(3, 11, 8) // [3,11,8]
Array.of(3) // [3]
Array.of(3).length // 1
```
- copyWithin()
```
Array.prototype.copyWithin(target, start = 0, end = this.length)
target（必需）：从该位置开始替换数据。如果为负值，表示倒数。
start（可选）：从该位置开始读取数据，默认为 0。如果为负值，表示从末尾开始计算。
end（可选）：到该位置前停止读取数据，默认等于数组长度。如果为负值，表示从末尾开始计算

在当前数组内部，将指定位置的成员复制到其他位置（会覆盖原有成员），然后返回当前数组。也就是说，使用这个方法，会修改当前数组
[1, 2, 3, 4, 5].copyWithin(0, 3)

```

- find, findIndex
- fill方法使用给定值，填充一个数组

```
['a', 'b', 'c'].fill(7)
// [7, 7, 7]

new Array(3).fill(7)
// [7, 7, 7]

let arr = new Array(3).fill({name: "Mike"});
arr[0].name = "Ben";
arr
// [{name: "Ben"}, {name: "Ben"}, {name: "Ben"}]

let arr = new Array(3).fill([]);
arr[0].push(5);
arr
// [[5], [5], [5]]
```
- entries()，keys()和values()
```
遍历数组。它们都返回一个遍历器对象（详见《Iterator》一章），可以用for...of循环进行遍历，唯一的区别是keys()是对键名的遍历、values()是对键值的遍历，entries()是对键值对的遍历
for (let index of ['a', 'b'].keys()) {
  console.log(index);
}
// 0
// 1

for (let elem of ['a', 'b'].values()) {
  console.log(elem);
}
// 'a'
// 'b'

for (let [index, elem] of ['a', 'b'].entries()) {
  console.log(index, elem);
}
// 0 "a"
// 1 "b"

如果不使用for...of循环，可以手动调用遍历器对象的next方法，进行遍历
let letter = ['a', 'b', 'c'];
let entries = letter.entries();
console.log(entries.next().value); // [0, 'a']
console.log(entries.next().value); // [1, 'b']
console.log(entries.next().value); // [2, 'c']
```
- includes方法返回一个布尔值，表示某个数组是否包含给定的值
- flat(), flatMap()

```
flat()默认只会“拉平”一层，如果想要“拉平”多层的嵌套数组，可以将flat()方法的参数写成一个整数，表示想要拉平的层数，默认为1

flatMap()方法对原数组的每个成员执行一个函数（相当于执行Array.prototype.map()），然后对返回值组成的数组执行flat()方法。该方法返回一个新数组，不改变原数组
flatMap()只能展开一层数组
```
- 数组的空位

```
forEach(), filter(), reduce(), every() 和some()都会跳过空位。
map()会跳过空位，但会保留这个值
join()和toString()会将空位视为undefined，而undefined和null会被处理成空字符串

Array.from方法会将数组的空位，转为undefined

扩展运算符（...）也会将空位转为undefined

copyWithin()会连空位一起拷贝

fill()会将空位视为正常的数组位置

for...of循环也会遍历空位

entries()、keys()、values()、find()和findIndex()会将空位处理成undefined
```
- Sort()
```
const unstableSorting = (s1, s2) => {
  if (s1[0] <= s2[0]) return -1;
  return 1;
};

arr.sort(unstableSorting)
```
## 对象的扩展
- 属性的简洁表示法
```
const foo = 'bar';
const baz = {foo};
baz // {foo: "bar"}

// 等同于
const baz = {foo: foo};
```



## 对象字面量扩展

```
let a = {
    x: x,
    y: y
}

let a = {
    x, 
    y
}
```

## Getter/Setter

## 计算属性名

```
x[pre + 'foo'] = function(..) {..}
```

## 设定[[Prototype]]

```
//es5
let o1 = {
    
}

let o2 = {
    proto: o1
}

//es6
Object.setPrototypeOf(o2, o1);

Object.getPrototypeOf(o2);
```

## super对象
- 继承时，可以调用父类方法
- 调用原型链方法

```
Object.setPrototypeOf(o2, o1);

o2 = {
    foo() {
        super.foo();
    }
}
```
## 模板字面量

```
const a = `${x}`;
```

## 标签模板字面量

```
function foo(strings, ...values) {
    ...
}

let a = 'hello';

foo`Every is ${a}`;

//strings => 'Every is'
//values => hello
```

## 箭头函数

```
//可以保留当前函数this的作用域

funtion foo() {
    mark() {
        return () => this.mark();
    }
}
```

## for..of循环
- for..of循环 遍历值
- for..in循环 遍历索引

## 迭代器

```
const arr = [];
const a = arr[Symbol.iterator]();
const b = arr.entries();

//迭代器方法：
//next()
//返回值： {value: null, done: false};仅当next遍历完成之后再次next， done为true
a.next();

//可选方法： return, throw 
```












