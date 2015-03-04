# 前端指南

# HTML

### 语义

HTML5为我们提供了大量语义化元素来准确地描述网页内容。相信你会从它丰富的词汇中受益

```html
<!-- bad -->
<div id="main">
  <div class="article">
    <div class="header">
    
      <h1>Blog post</h1>
      <p>Published: <span>21st Feb, 2015</span></p>
    </div>
    <p>…</p>
  </div>
</div>

<!-- good -->
<main>
  <article>
    <header>
      <h1>Blog post</h1>
      <p>Published: <time datetime="2015-02-21">21st Feb, 2015</time></p>
    </header>
    <p>…</p>
  </article>
</main>
```

请确保你理解了所使用的元素的语义，错误地使用语义元素比起保守地中立更糟糕。

```html
<!-- bad -->
<h1>
  <figure>
    <img alt=Company src=logo.png>
  </figure>
</h1>

<!-- good -->
<h1>
  <img alt=Company src=logo.png>
</h1>
```

### 简洁性

保持代码的简洁，忘掉那些陈旧的 XHTML 书写习惯。

```html
<!-- bad -->
<!doctype html>
<html lang=en>
  <head>
    <meta http-equiv=Content-Type content="text/html; charset=utf-8" />
    <title>Contact</title>
    <link rel=stylesheet href=style.css type=text/css />
  </head>
  <body>
    <h1>Contact me</h1>
    <label>
      Email address:
      <input type=email placeholder=you@email.com required=required />
    </label>
    <script src=main.js type=text/javascript></script>
  </body>
</html>

<!-- good -->
<!doctype html>
<html lang=en>
  <meta charset=utf-8>
  <title>Contact</title>
  <link rel=stylesheet href=style.css>

  <h1>Contact me</h1>
  <label>
    Email address:
    <input type=email placeholder=you@email.com required>
  </label>
  <script src=main.js></script>
</html>
```

### 可读性

不要把可读性放在最后考虑，改进网站不需要你是一名WCAG（网页内容亲和力方针）的专家，马上动手做些小改动能给你带来非凡的意义，如下：

* 恰当地使用 'alt' 属性
* 保证按钮和链接像这样标记（不要简单粗暴地使用 `<div class=button>`）
* 不要专门依赖颜色值来表达信息
* 明确地为表单控件提供label标记

```html
<!-- bad -->
<h1><img alt="Logo" src="logo.png"></h1>

<!-- good -->
<h1><img alt="My Company, Inc." src="logo.png"></h1>
```

### 语言

当可以定义语言和字符编码时，建议总是在文档级别声明这两项，尽管它们在HTTP头部中已经指定。比起其他的字符编码，我们更加青睐于使用UTF-8。

```html
<!-- bad -->
<!doctype html>
<title>Hello, world.</title>

<!-- good -->
<!doctype html>
<html lang=en>
  <meta charset=utf-8>
  <title>Hello, world.</title>
</html>
```

### 性能

除非有正当理由要在网页内容前加载脚本，否则不要阻塞页面渲染的过程。如果样式表非常庞大，请将页面最初加载时绝对需要的那些样式分离出来，把次要的样式声明放到独立的样式表中延迟加载。两条HTTP请求显然比一条要慢，但加载速度快慢是否可以觉察才是最关键的因素。

```html
<!-- bad -->
<!doctype html>
<meta charset=utf-8>
<script src=analytics.js></script>
<title>Hello, world.</title>
<p>...</p>

<!-- good -->
<!doctype html>
<meta charset=utf-8>
<title>Hello, world.</title>
<p>...</p>
<script src=analytics.js></script>
```

## CSS

### 分号

尽管技术上说CSS中的分号是作为分隔符，但请总把它当成终止符使用。

```css
/* bad */
div {
  color: red
}

/* good */
div {
  color: red;
}
```

### 盒模型

理想情况中盒模型在整个文档中应当保持一致。全局设置 `* { box-sizing: border-box; }` 是个好主意,但在可以避免的情况下请不要改变特定元素的默认盒模型。

```css
/* bad */
div {
  width: 100%;
  padding: 10px;
  box-sizing: border-box;
}

/* good */
div {
  padding: 10px;
}
```

### 文档流

在可以避免的情况下不要改变一个元素的默认行为。尽可能让元素处于正常的文档流中。比如说，移除图片下方的空白不应该通过改变它的默认显示方式来实现：

```css
/* bad */
img {
  display: block;
}

/* good */
img {
  vertical-align: middle;
}
```

同样地，避免让一个元素脱离文档流。

```css
/* bad */
div {
  width: 100px;
  position: absolute;
  right: 0;
}

/* good */
div {
  width: 100px;
  margin-left: auto;
}
```

### 定位

用CSS定位元素的方法有很多，请按以下优先级顺序的属性/值对规范自己的写法：

```
display: block;
display: flex;
position: relative;
position: sticky;
position: absolute;
position: fixed;
```

### 选择器

简化选择器使其和DOM紧密联系，考虑一下给想要匹配的元素添加一个class，而你的选择器中包含超过三个伪类选择器，后代选择器或相邻兄弟选择器。

```css
/* bad */
div:first-of-type :last-child > p ~ *

/* good */
div:first-of-type .info
```

除非必要，否则不要让选择器过载。


```css
/* bad */
img[src$=svg], ul > li:first-child {
  opacity: 0;
}

/* good */
[src$=svg], ul > :first-child {
  opacity: 0;
}
```

### 特殊性

不要书写难以覆盖的值和选择器。最小化id选择器的使用，避免使用 `!important`。

```css
/* bad */
.bar {
  color: green !important;
}
.foo {
  color: red;
}

/* good */
.foo.bar {
  color: green;
}
.foo {
  color: red;
}
```

### 样式覆盖

如果可能请不要对样式进行覆盖，那样会使选择器难以阅读并且增加调试难度。

```css
/* bad */
li {
  visibility: hidden;
}
li:first-child {
  visibility: visible;
}

/* good */
li + li {
  visibility: hidden;
}
```

### 继承

不要重复书写可以继承的样式声明。

```css
/* bad */
div h1, div p {
  text-shadow: 0 1px 0 #fff;
}

/* good */
div {
  text-shadow: 0 1px 0 #fff;
}
```

### 简洁性
保持代码的简洁，除非需要，否则请使用速记属性，避免使用多重属性。

```css
/* bad */
div {
  transition: all 1s;
  top: 50%;
  margin-top: -10px;
  padding-top: 5px;
  padding-right: 10px;
  padding-bottom: 20px;
  padding-left: 10px;
}

/* good */
div {
  transition: 1s;
  top: calc(50% - 10px);
  padding: 5px 10px 20px;
}
```

### 语言

多用英文表达式，少用数学表达式。

```css
/* bad */
:nth-child(2n + 1) {
  transform: rotate(360deg);
}

/* good */
:nth-child(odd) {
  transform: rotate(1turn);
}
```

### 厂商前缀

大胆地扔掉那些废弃的厂商前缀。如果一定要使用，请在标准属性前插入它们。

```css
/* bad */
div {
  transform: scale(2);
  -webkit-transform: scale(2);
  -moz-transform: scale(2);
  -ms-transform: scale(2);
  transition: 1s;
  -webkit-transition: 1s;
  -moz-transition: 1s;
  -ms-transition: 1s;
}

/* good */
div {
  -webkit-transform: scale(2);
  transform: scale(2);
  transition: 1s;
}
```

### 动画

尽量使用transitions而不是animations，除了`opactiy`和`transform`之外的其他属性避免使用动画。

```css
/* bad */
div:hover {
  animation: move 1s forwards;
}
@keyframes move {
  100% {
    margin-left: 100px;
  }
}

/* good */
div:hover {
  transition: 1s;
  transform: translateX(100px);
}
```

### 单位

如果可以不用书写单位，那就无需书写。使用相对单位时多用`rem`，多用秒（s），少用毫秒（ms）。

```css
/* bad */
div {
  margin: 0px;
  font-size: .9em;
  line-height: 22px;
  transition: 500ms;
}

/* good */
div {
  margin: 0;
  font-size: .9rem;
  line-height: 1.5;
  transition: .5s;
}
```

### 颜色值

需要透明度时请用`rgba`，除此以外请总是使用十六进制格式颜色值。

```css
/* bad */
div {
  color: hsl(103, 54%, 43%);
}

/* good */
div {
  color: #5a3;
}
```

### 绘图

在资源可以很简单地用CSS实现时，请这样做减少HTTP请求。

```css
/* bad */
div::before {
  content: url(white-circle.svg);
}

/* good */
div::before {
  content: "";
  display: block;
  width: 20px;
  height: 20px;
  border-radius: 50%;
  background: #fff;
}
```

### Hacks

不要使用Hacks。

```css
/* bad */
div {
  // position: relative;
  transform: translateZ(0);
}

/* good */
div {
  /* position: relative; */
  will-change: transform;
}
```

## JavaScript

### 性能

基本上讲JavaScript不会成为你的性能瓶颈，因此比起性能应当更多考虑可读性，准确性和代码质量。进行如图片压缩，可访问性和DOM重绘等优化工作来取代。如果你只能记住本文档中的一条指南，那记住这条吧。

```javascript
// bad (albeit way faster)
const arr = [1, 2, 3, 4];
const len = arr.length;
var i = -1;
var result = [];
while (++i < len) {
  var n = arr[i];
  if (n % 2 > 0) continue;
  result.push(n * n);
}

// good
const arr = [1, 2, 3, 4];
const isEven = n => n % 2 == 0;
const square = n => n * n;

const result = arr.filter(isEven).map(square);
```

### 无状态性

尝试保持干净的函数代码。一切函数在理想情况下不会产生副作用，不要使用外部数据并且返回新的对象，而不是改变那些已有的对象。

```javascript
// bad
const merge = (target, ...sources) => Object.assign(target, ...sources);
merge({ foo: "foo" }, { bar: "bar" }); // => { foo: "foo", bar: "bar" }

// good
const merge = (...sources) => Object.assign({}, ...sources);
merge({ foo: "foo" }, { bar: "bar" }); // => { foo: "foo", bar: "bar" }
```

### 原生

尽可能地依靠原生方法。

```javascript
// bad
const toArray = obj => [].slice.call(obj);

// good
const toArray = (() =>
  Array.from ? Array.from : obj => [].slice.call(obj)
)();
```

### 强制转换

隐式强制类型转换如果有用，那么尽情的拥抱它吧，不要搞“货物崇拜”。

```javascript
// bad
if (x === undefined || x === null) { ... }

// good
if (x == undefined) { ... }
```

### 循环

如果循环强迫你使用可变对象，请不要使用它，应该使用`array.prototype`方法。

```javascript
// bad
const sum = arr => {
  var sum = 0;
  var i = -1;
  for (;arr[++i];) {
    sum += arr[i];
  }
  return sum;
};

sum([1, 2, 3]); // => 6

// good
const sum = arr =>
  arr.reduce((x, y) => x + y);

sum([1, 2, 3]); // => 6
```

如果无法实现，或者说使用`array.prototype`方法无疑是一种滥用的做法时，可以使用递归

```javascript
// bad
const createDivs = howMany => {
  while (howMany--) {
    document.body.insertAdjacentHTML("beforeend", "<div></div>");
  }
};
createDivs(5);

// bad
const createDivs = howMany =>
  [...Array(howMany)].forEach(() =>
    document.body.insertAdjacentHTML("beforeend", "<div></div>")
  );
createDivs(5);

// good
const createDivs = howMany => {
  if (!howMany) return;
  document.body.insertAdjacentHTML("beforeend", "<div></div>");
  return createDivs(howMany - 1);
};
createDivs(5);
```

### Arguments

忘掉`arguments`对象吧，其余的参数才是更好的选择，原因如下：

1.拥有命名，因此它可以让人对函数所期望的参数有个更好的了解
2.实际意义上的数组，使用更加方便

```javascript
// bad
const sortNumbers = () =>
  Array.prototype.slice.call(arguments).sort();

// good
const sortNumbers = (...numbers) => numbers.sort();
```

### Apply方法

忘掉`apply()`方法，用展开操作符（spread operator）代替。

```javascript
const greet = (first, last) => `Hi ${first} ${last}`;
const person = ["John", "Doe"];

// bad
greet.apply(null, person);

// good
greet(...person);
```

### Bind方法

有更符合习惯的方法时不要使用`bind()`方法。

```javascript
// bad
["foo", "bar"].forEach(func.bind(this));

// good
["foo", "bar"].forEach(func, this);
```
```javascript
// bad
const person = {
  first: "John",
  last: "Doe",
  greet() {
    const full = function() {
      return `${this.first} ${this.last}`;
    }.bind(this);
    return `Hello ${full()}`;
  }
}

// good
const person = {
  first: "John",
  last: "Doe",
  greet() {
    const full = () => `${this.first} ${this.last}`;
    return `Hello ${full()}`;
  }
}
```

### 高阶函数

尽量避免嵌套函数。

```javascript
// bad
[1, 2, 3].map(num => String(num));

// good
[1, 2, 3].map(String);
```

### 组合

避免调用多次嵌套的函数，应使用函数组合。

```javascript
const plus1 = a => a + 1;
const mult2 = a => a * 2;

// bad
mult2(plus1(5)); // => 12

// good
const pipeline = (...funcs) => val => funcs.reduce((a, b) => b(a), val);
const addThenMult = pipeline(plus1, mult2);
addThenMult(5); // => 12
```

### 缓存

对功能测试，大型数据结构以及任何开销较大的操作进行缓存。

```javascript
// bad
const contains = (arr, value) =>
  Array.prototype.includes
    ? arr.includes(value)
    : arr.some(el => el === value);
contains(["foo", "bar"], "baz"); // => false

// good
const contains = (() =>
  Array.prototype.includes
    ? (arr, value) => arr.includes(value)
    : (arr, value) => arr.some(el => el === value)
)();
contains(["foo", "bar"], "baz"); // => false
```

### 变量

优先使用`const`而不是`let`，优先使用`let`而不是`var`。

```javascript
// bad
var obj = {};
obj["foo" + "bar"] = "baz";

// good
const obj = {
  ["foo" + "bar"]: "baz"
};
```

### 条件语句

优先使用 IIFE（匿名函数自调用）和返回语句，而不是单独的if,else if,else和switch语句。

```javascript
// bad
var grade;
if (result < 50)
  grade = "bad";
else if (result < 90)
  grade = "good";
else
  grade = "excellent";

// good
const grade = (() => {
  if (result < 50)
    return "bad";
  if (result < 90)
    return "good";
  return "excellent";
})();
```

### 对象迭代

尽可能地不要使用`for...in`。

```javascript
const shared = { foo: "foo" };
const obj = Object.create(shared, {
  bar: {
    value: "bar",
    enumerable: true
  }
});

// bad
for (var prop in obj) {
  if (obj.hasOwnProperty(prop))
    console.log(prop);
}

// good
Object.keys(obj).forEach(prop => console.log(prop));
```

### Map对象

当objects的使用情况合理时，maps通常是更好更加健壮的选择，有疑惑的话，就使用`Map`吧。

```javascript
// bad
const me = {
  name: "Ben",
  age: 30
};
var meSize = Object.keys(me).length;
meSize; // => 2
me.country = "Belgium";
meSize++;
meSize; // => 3

// good
const me = Map();
me.set("name", "Ben");
me.set("age", 30);
me.size; // => 2
me.set("country", "Belgium");
me.size; // => 3
```

### 柯里化

柯里化可能在其他语言中有它的地位，但是在JavaScript中请避免这么做。通过引入其他语言的范式而且相应的用例极不常见，这样会使代码难以阅读。

```javascript
// bad
const sum = a => b => a + b;
sum(5)(3); // => 8

// good
const sum = (a, b) => a + b;
sum(5, 3); // => 8
```

### 可读性

不要使用一些看似聪明的奇技淫巧来混淆代码的实际目的。

```javascript
// bad
foo || doSomething();

// good
if (!foo) doSomething();
```
```javascript
// bad
void function() { /* IIFE */ }();

// good
(function() { /* IIFE */ }());
```
```javascript
// bad
const n = ~~3.14;

// good
const n = Math.floor(3.14);
```

### 代码复用

不要担心写出大量小巧，高可组合性和可复用的函数。

```javascript
// bad
arr[arr.length - 1];

// good
const first = arr => arr[0];
const last = arr => first(arr.slice(-1));
last(arr);
```
```javascript
// bad
const product = (a, b) => a * b;
const triple = n => n * 3;

// good
const product = (a, b) => a * b;
const triple = product.bind(null, 3);
```

### 依赖性

最小化依赖性。第三方库的代码你并不了解。不要为了仅仅几个可以轻易替代的方法加载整个完整的库。

```javascript
// bad
var _ = require("underscore");
_.compact(["foo", 0]));
_.unique(["foo", "foo"]);
_.union(["foo"], ["bar"], ["foo"]);

// good
const compact = arr => arr.filter(el => el);
const unique = arr => [...Set(arr)];
const union = (...arr) => unique([].concat(...arr));

compact(["foo", 0]);
unique(["foo", "foo"]);
union(["foo"], ["bar"], ["foo"]);
```

