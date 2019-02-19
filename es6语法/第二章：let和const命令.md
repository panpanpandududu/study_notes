# let 和 const 命令

### 1.let命令

#### 基本用法

es6新增的let命令。用来声明变量，类似于var,但是**let声明的变量**，只能在let命令所在的**代码块中有效**。

例如for循环的计数器，就很适合let，ef：

```javascript
for (let i = 0; i < 10; i++) {
  // ...
}

console.log(i);
```

下面的代码如果使用`var`，最后输出的是`10`

```javascript
var a = [];
for (var i = 0; i < 10; i++) {
  a[i] = function () {
    console.log(i);
  };
}
a[6](); // 10
```

###### 解析：此时为什么不是6？

因为变量i是var命令声明的，在**全局范围内都有效**，所以全局只有一个变量i。每一次循环，变量i的值都会发生改变，而**循环内被赋给数组a的函数内部的`console.log(i)`,里面的i指向的就是全局的i**,也就是说，**所有数组a的成员里面的i,指向的都是同一个i,导致运行时输出的是最后一轮的i的值**，也就是10.

如果使用`let`，声明的变量仅在块级作用域内有效，最后输出的是 6。

```javascript
var a = [];
for (let i = 0; i < 10; i++) {
  a[i] = function () {
    console.log(i);
  };
}
a[6](); // 6
```

#### 不存在变量提升

var命令会发生变量提升现象，即变量可以在声明之前使用，值为`undefined`。但是let所声明的变量一定要在声明后使用，否则报错。

```javascript
// var 的情况
console.log(foo); // 输出undefined
var foo = 2;

// let 的情况
console.log(bar); // 报错ReferenceError
let bar = 2;
```

上面代码中，变量`foo`用`var`命令声明，会发生变量提升，即脚本开始运行时，变量`foo`已经存在了，但是没有值，所以会输出`undefined`。变量`bar`用`let`命令声明，不会发生变量提升。这表示在声明它之前，变量`bar`是不存在的，这时如果用到它，就会抛出一个错误。

#### 暂时性死区

只要块级作用域内存在let命令，它所声明的变量就“绑定”这个区域，不再受外部的影响

```javascript
var tmp = 123;
if (true) {
  tmp = 'abc'; // ReferenceError
  let tmp;
}
```

上面代码中，存在全局变量`tmp`，但是块级作用域内`let`又声明了一个局部变量`tmp`，导致后者绑定这个块级作用域，所以在`let`声明变量前，对`tmp`赋值会报错

ES6 明确规定，如果区块中存在`let`和`const`命令，这个区块对这些命令声明的变量，从一开始就形成了封闭作用域。凡是在声明之前就使用这些变量，就会报错。

总之，在代码块内，使用`let`命令声明变量之前，该变量都是不可用的。这在语法上，称为“暂时性死区”（temporal dead zone，简称 TDZ）

```javascript
if (true) {
  // TDZ开始
  tmp = 'abc'; // ReferenceError
  console.log(tmp); // ReferenceError

  let tmp; // TDZ结束
  console.log(tmp); // undefined

  tmp = 123;
  console.log(tmp); // 123
}
```

上面代码中，在`let`命令声明变量`tmp`之前，都属于变量`tmp`的“死区”。

“暂时性死区”也意味着`typeof`不再是一个百分之百安全的操作。

```javascript
typeof x; // ReferenceError
let x;
```

上面代码中，变量`x`使用`let`命令声明，所以在声明之前，都属于`x`的“死区”，只要用到该变量就会报错。因此，`typeof`运行时就会抛出一个`ReferenceError`。

作为比较，如果一个变量根本没有被声明，使用`typeof`反而不会报错。

```javascript
typeof undeclared_variable // "undefined"
```

上面代码中，`undeclared_variable`是一个不存在的变量名，结果返回“undefined”。所以，在没有`let`之前，`typeof`运算符是百分之百安全的，永远不会报错。现在这一点不成立了。这样的设计是为了让大家养成良好的编程习惯，变量一定要在声明之后使用，否则就报错。

有些“死区”比较隐蔽，不太容易发现。

```javascript
function bar(x = y, y = 2) {
  return [x, y];
}

bar(); // 报错
```

上面代码中，调用`bar`函数之所以报错（某些实现可能不报错），是因为参数`x`默认值等于另一个参数`y`，而此时`y`还没有声明，属于”死区“。如果`y`的默认值是`x`，就不会报错，因为此时`x`已经声明了。

```javascript
function bar(x = 2, y = x) {
  return [x, y];
}
bar(); // [2, 2]
```

另外，下面的代码也会报错，与`var`的行为不同。

```javascript
// 不报错
var x = x;

// 报错
let x = x;
// ReferenceError: x is not defined
```

上面代码报错，也是因为暂时性死区。使用`let`声明变量时，只要变量在还没有声明完成前使用，就会报错。上面这行就属于这个情况，在变量`x`的声明语句还没有执行完成前，就去取`x`的值，导致报错”x 未定义“。

es6规定暂时性死区和let，const语句不出现变量提升。

#### 不允许重复声明

`let`不允许在相同作用域内，重复声明一个变量。

```javascript
// 报错
function func() {
  let a = 10;
  var a = 1;
}

// 报错
function func() {
  let a = 10;
  let a = 1;
}
```

因此在函数内部重新声明函数

```javascript
function func(arg) {
  let arg; // 报错
}

function func(arg) {
  {
    let arg; // 不报错
  }
}
```

### 2.块级作用域

es5只有全局作用域和函数作用域，没有块级作用域，使得很多地方不合理

###### 如：内层变量可能会覆盖外层变量

```javascript
var tmp = new Date();

function f() {
  console.log(tmp);
  if (false) {
    var tmp = 'hello world';
  }
}

f(); // undefined
```

上面代码的原意是，`if`代码块的外部使用外层的`tmp`变量，内部使用内层的`tmp`变量。但是，函数`f`执行后，输出结果为`undefined`，原因在于变量提升，导致内层的`tmp`变量覆盖了外层的`tmp`变量。

###### 用来计数的循环变量泄露为全局变量

```javascript
var s = 'hello';

for (var i = 0; i < s.length; i++) {
  console.log(s[i]);
}

console.log(i); // 5
```

上面代码中，变量`i`只用来控制循环，但是循环结束后，它并没有消失，泄露成了全局变量。

#### ES6 的块级作用域 

`let`实际上为js新增了块级作用域

```javascript
function f1() {
  let n = 5;
  if (true) {
    let n = 10;
      console.log(n); //10
  }
  console.log(n); // 5
}
f1（）；
```

因为let是块级作用域，所以外层代码不受内层代码块的影响。如果使用的var,两次输出的都是10

es6允许块级作用域的任意嵌套

```javascript
{{{{{let insane = 'Hello World'}}}}};
```

上面代码使用了一个五层的块级作用域。外层作用域无法读取内层作用域的变量

```javascript
{{{{
  {let insane = 'Hello World'}
  console.log(insane); // 报错
}}}};
```

内层作用域可以定义外层作用域的同名变量。

```javascript
{{{{
  let insane = 'Hello World';
  {let insane = 'Hello World'}
}}}};
```

#### 块级作用域与函数声明

函数能不能在块级作用域之中声明呢，es5规定不可以，es6明确允许在块级作用域之中声明函数，es6规定，块级作用域之中，**函数声明语句的行为类似于`let`，在块级作用域之外不可引用**。

原来，如果改变了块级作用域内声明的函数的处理规则，显然会对老代码产生很大影响。为了减轻因此产生的不兼容问题，ES6 在[附录 B](http://www.ecma-international.org/ecma-262/6.0/index.html#sec-block-level-function-declarations-web-legacy-compatibility-semantics)里面规定，浏览器的实现可以不遵守上面的规定，有自己的[行为方式](http://stackoverflow.com/questions/31419897/what-are-the-precise-semantics-of-block-level-functions-in-es6)。

- 允许在块级作用域内声明函数。
- 函数声明类似于`var`，即会提升到全局作用域或函数作用域的头部。
- 同时，函数声明还会提升到所在的块级作用域的头部。

注意，上面三条规则只对 ES6 的浏览器实现有效，其他环境的实现不用遵守，还是将块级作用域的函数声明当作`let`处理。

根据这三条规则，在浏览器的 ES6 环境中，块级作用域内声明的函数，行为类似于`var`声明的变量。

```javascript
// 浏览器的 ES6 环境
function f() { console.log('I am outside!'); }

(function () {
  if (false) {
    // 重复声明一次函数f
    function f() { console.log('I am inside!'); }
  }

  f();
}());
// Uncaught TypeError: f is not a function
```

上面的代码在符合 ES6 的浏览器中，都会报错，因为实际运行的是下面的代码。

```javascript
// 浏览器的 ES6 环境
function f() { console.log('I am outside!'); }
(function () {
  var f = undefined;
  if (false) {
    function f() { console.log('I am inside!'); }
  }

  f();
}());
// Uncaught TypeError: f is not a function
```

考虑到环境导致的行为差异太大，应该避免在块级作用域内声明函数。如果确实需要，也应该写成函数表达式，而不是函数声明语句。

```javascript
// 函数声明语句
{
  let a = 'secret';
  function f() {
    return a;
  }
}

// 函数表达式
{
  let a = 'secret';
  let f = function () {
    return a;
  };
}
```

### const 命令

**const声明一个只读的常量，一旦声明就不可改变**

```javascript
const PI = 3.1415;
PI // 3.1415

PI = 3;
// TypeError: Assignment to constant variable.改变常量的值会报错
```

**const声明的比那两不得改变值，意味着const一旦声明变量，必须立即初始化，不能留到以后赋值。**

```javascript
const foo;
// SyntaxError: Missing initializer in const declaration
//const只声明不赋值就会报错
```

**`const`的作用域与let命令相同：只在声明所在的块级作用域内有效。**

```javascript
if (true) {
  const MAX = 5;
}

MAX // Uncaught ReferenceError: MAX is not defined
```

**`const`命令声明的常量也是不提升，同样存在暂时性死区，只能在声明的位置后面使用。**

```javascript
if (true) {
  console.log(MAX); //Missing initializer in const declaration
  const MAX = 5;
}//如果你要声明一个常量，必须要赋初值。否则就会报错
```

本质：

`const`实际上保证的，并不是变量的值不得改动，而是**变量指向**的那个**内存地址**所保存的**数据**不得改动。对于简单类型的数据（数值、字符串、布尔值），值就保存在变量指向的那个内存地址，因此等同于常量。**但对于复合类型的数据（主要是对象和数组），变量指向的内存地址，保存的只是一个指向实际数据的指针，`const`只能保证这个指针是固定的（即总是指向另一个固定的地址），至于它指向的数据结构是不是可变的，就完全不能控制了。因此，将一个对象声明为常量必须非常小心**

```javascript
const foo = {};

// 为 foo 添加一个属性，可以成功
foo.prop = 123;
foo.prop // 123

// 将 foo 指向另一个对象，就会报错
foo = {}; // Assignment to constant variable
```

在上述代码中，一开始声明了一个常量foo，并将其指针地址指向一个对象，此时不可变的是这个地址，但对象本身是可变的，所以依然可以为其添加新属性。

**常量为对象：**

```javascript
const foo = {};

// 为 foo 添加一个属性，可以成功
foo.prop = 123;
console.log(foo);//{prop: 123}
```

**常量为数组：**

```javascript
const a = [];
a.push('Hello'); // 可执行
a.length = 0;    // 可执行
console.log(a_arr);//["hello", lengh: 0]
a = ['Dave'];    // 报错
```

对象冻结方法：`Object.freeze`

```javascript
const foo = Object.freeze({});
//foo指向一个冻结的对象，所以新加属性不起作用
// 常规模式时，下面一行不起作用；
// 严格模式时，该行会报错
foo.prop = 123;
console.log(foo);//{}
```

除了将对象本身冻结，对象的属性也应该冻结，下面是一个将对象彻底冻结的函数

```javascript
var constantize = (obj) => {
  Object.freeze(obj);
  Object.keys(obj).forEach( (key, i) => {
    if ( typeof obj[key] === 'object' ) {
      constantize( obj[key] );
    }
  });
};
```

**ES6声明变量的六种方法**

`var ,function,let,const,import,class`

#### 顶层对象的属性

在浏览器环境指的是window对象，在Node指的是global对象。