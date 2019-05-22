# Frontend Guidelines

## HTML

### Semantics

HTML5 provides us with lots of semantic elements aimed to describe precisely the content. Make sure you benefit from its rich vocabulary.

```html
<!-- bad -->
<div id=main>
  <div class=article>
    <div class=header>
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
      <p>Published: <time datetime=2015-02-21>21st Feb, 2015</time></p>
    </header>
    <p>…</p>
  </article>
</main>
```

Make sure you understand the semantics of the elements you're using. It's worse to use a semantic
element in a wrong way than staying neutral.

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

### Brevity

Keep your code terse. Forget about your old XHTML habits.

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

### Accessibility

Accessibility shouldn't be an afterthought. You don't have to be a WCAG expert to improve your
website, you can start immediately by fixing the little things that make a huge difference, such as:

* learning to use the `alt` attribute properly
* making sure your links and buttons are marked as such (no `<div class=button>` atrocities)
* not relying exclusively on colors to communicate information
* explicitly labelling form controls

```html
<!-- bad -->
<h1><img alt=Logo src=logo.png></h1>

<!-- good -->
<h1><img alt=Company src=logo.png></h1>
```

### Language & character encoding

While defining the language is optional, it's recommended to always declare
it on the root element.

The HTML standard requires that pages use the UTF-8 character encoding.
It has to be declared, and although it can be declared in the Content-Type HTTP header,
it is recommended to always declare it at the document level.

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

### Performance

Unless there's a valid reason for loading your scripts before your content, don't block the
rendering of your page. If your style sheet is heavy, isolate the styles that are absolutely
required initially and defer the loading of the secondary declarations in a separate style sheet.
Two HTTP requests is significantly slower than one, but the perception of speed is the most
important factor.

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

### Semicolons

While the semicolon is technically a separator in CSS, always treat it as a terminator.

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

### Box model

The box model should ideally be the same for the entire document. A global
`* { box-sizing: border-box; }` is fine, but don't change the default box model
on specific elements if you can avoid it.

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

### Flow

Don't change the default behavior of an element if you can avoid it. Keep elements in the
natural document flow as much as you can. For example, removing the white-space below an
image shouldn't make you change its default display:

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

Similarly, don't take an element off the flow if you can avoid it.

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

### Positioning

There are many ways to position elements in CSS. Favor modern layout specifications
such as Flexbox and Grid, and avoid removing elements from the normal document flow, for example
with `position: absolute`.

### Selectors

Minimize selectors tightly coupled to the DOM. Consider adding a class to the elements
you want to match when your selector exceeds 3 structural pseudo-classes, descendant or
sibling combinators.

```css
/* bad */
div:first-of-type :last-child > p ~ *

/* good */
div:first-of-type .info
```

Avoid overloading your selectors when you don't need to.

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

### Specificity

Don't make values and selectors hard to override. Minimize the use of `id`'s
and avoid `!important`.

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

### Overriding

Overriding styles makes selectors and debugging harder. Avoid it when possible.

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

### Inheritance

Don't duplicate style declarations that can be inherited.

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

### Brevity

Keep your code terse. Use shorthand properties and avoid using multiple properties when
it's not needed.

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

### Language

Prefer English over math.

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

### Vendor prefixes

Kill obsolete vendor prefixes aggressively. If you need to use them, insert them before the
standard property.

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

### Animations

Favor transitions over animations. Avoid animating other properties than
`opacity` and `transform`.

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

### Units

Use unitless values when you can. Favor `rem` if you use relative units. Prefer seconds over
milliseconds.

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

### Colors

If you need transparency, use `rgba`. Otherwise, always use the hexadecimal format.

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

### Drawing

Avoid HTTP requests when the resources are easily replicable with CSS.

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

Don't use them.

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

### Performance

Favor readability, correctness and expressiveness over performance. JavaScript will basically never
be your performance bottleneck. Optimize things like image compression, network access and DOM
reflows instead. If you remember just one guideline from this document, choose this one.

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

### Statelessness

Try to keep your functions pure. All functions should ideally produce no side-effects, use no outside data and return new objects instead of mutating existing ones.

```javascript
// bad
const merge = (target, ...sources) => Object.assign(target, ...sources);
merge({ foo: "foo" }, { bar: "bar" }); // => { foo: "foo", bar: "bar" }

// good
const merge = (...sources) => Object.assign({}, ...sources);
merge({ foo: "foo" }, { bar: "bar" }); // => { foo: "foo", bar: "bar" }
```

### Natives

Rely on native methods as much as possible.

```javascript
// bad
const toArray = obj => [].slice.call(obj);

// good
const toArray = (() =>
  Array.from ? Array.from : obj => [].slice.call(obj)
)();
```

### Coercion

Embrace implicit coercion when it makes sense. Avoid it otherwise. Don't cargo-cult.

```javascript
// bad
if (x === undefined || x === null) { ... }

// good
if (x == undefined) { ... }
```

### Loops

Don't use loops as they force you to use mutable objects. Rely on `array.prototype` methods.

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
If you can't, or if using `array.prototype` methods is arguably abusive, use recursion.

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

Here's a [generic loop function](https://gist.github.com/bendc/6cb2db4a44ec30208e86) making recursion easier to use.

### Arguments

Forget about the `arguments` object. The rest parameter is always a better option because:

1. it's named, so it gives you a better idea of the arguments the function is expecting
2. it's a real array, which makes it easier to use.

```javascript
// bad
const sortNumbers = () =>
  Array.prototype.slice.call(arguments).sort();

// good
const sortNumbers = (...numbers) => numbers.sort();
```

### Apply

Forget about `apply()`. Use the spread operator instead.

```javascript
const greet = (first, last) => `Hi ${first} ${last}`;
const person = ["John", "Doe"];

// bad
greet.apply(null, person);

// good
greet(...person);
```

### Bind

Don't `bind()` when there's a more idiomatic approach.

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

### Higher-order functions

Avoid nesting functions when you don't have to.

```javascript
// bad
[1, 2, 3].map(num => String(num));

// good
[1, 2, 3].map(String);
```

### Composition

Avoid multiple nested function calls. Use composition instead.

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

### Caching

Cache feature tests, large data structures and any expensive operation.

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

### Variables

Favor `const` over `let` and `let` over `var`.

```javascript
// bad
var me = new Map();
me.set("name", "Ben").set("country", "Belgium");

// good
const me = new Map();
me.set("name", "Ben").set("country", "Belgium");
```

### Conditions

Favor IIFE's and return statements over if, else if, else and switch statements.

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

### Object iteration

Avoid `for...in` when you can.

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

### Objects as Maps

While objects have legitimate use cases, maps are usually a better, more powerful choice. When in
doubt, use a `Map`.

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
const me = new Map();
me.set("name", "Ben");
me.set("age", 30);
me.size; // => 2
me.set("country", "Belgium");
me.size; // => 3
```

### Curry

Currying is a powerful but foreign paradigm for many developers. Don't abuse it as its appropriate
use cases are fairly unusual.

```javascript
// bad
const sum = a => b => a + b;
sum(5)(3); // => 8

// good
const sum = (a, b) => a + b;
sum(5, 3); // => 8
```

### Readability

Don't obfuscate the intent of your code by using seemingly smart tricks.

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

### Code reuse

Don't be afraid of creating lots of small, highly composable and reusable functions.

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

### Dependencies

Minimize dependencies. Third-party is code you don't know. Don't load an entire library for just a couple of methods easily replicable:

```javascript
// bad
var _ = require("underscore");
_.compact(["foo", 0]));
_.unique(["foo", "foo"]);
_.union(["foo"], ["bar"], ["foo"]);

// good
const compact = arr => arr.filter(el => el);
const unique = arr => [...new Set(arr)];
const union = (...arr) => unique([].concat(...arr));

compact(["foo", 0]);
unique(["foo", "foo"]);
union(["foo"], ["bar"], ["foo"]);
```
