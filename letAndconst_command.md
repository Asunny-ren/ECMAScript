# let和const命令

## let命令

* es6新增了let命令，用来声明变量，用法类似var，但是所声明的变量只有在let命令所在的代码块内有效。
例如：
``` javascript
 {
     let a = 10;
     var b = 10;
 }
 a // ReferenceError a is not defined
 b // 10
```
for 循环的计数器就很适合let命令，例如：
``` javascript
  for(let i = 0; i < arr.length; i++){
      console.log(i);//控制台会输出最后i的值
  }
  console.log(i)
  // i is not defined
```

``` javascript
// 用var 来声明变量
  var a = [];
  for(var i = 0; i < 10; i++){
      a[i] = function () {
          console.log(i);
      }
  }
  a[6]();
  // 结果为10
```

``` javascript
  var a = [];
  for(let i = 0; i < 10; i++){
     a[i] = function () {
         console.log(i);
     }
  }
  a[6]();
  // 结果为6
```
#### let不存在变量的提升，变量一定要在声明后使用，否则会报错,例如:
``` javascript
console.log(foo); // 输出undefined
console.log(bar); // 报错ReferenceError

var foo = 2;
let bar = 2;
```

#### 暂时性死区
``` javascript
var tmp = 123;

if (true) {
  tmp = 'abc'; // ReferenceError
  let tmp;
}
//上面代码中，存在全局变量tmp，
//但是块级作用域内let又声明了一个局部变量tmp，
//导致后者绑定这个块级作用域，
//所以在let声明变量前，对tmp赋值会报错。
```

##### ES6明确规定，如果区块中存在let和const命令，这个区块对这些命令声明的变量，从一开始就形成了封闭作用域。凡是在声明之前就使用这些变量，就会报错。总之，在代码块内，使用let命令声明变量之前，该变量都是不可用的。这在语法上，称为“暂时性死区”（temporal dead zone，简称TDZ）。

### 不允许重复声明
let不允许在相同作用域内，重复声明同一个变量。
``` javascript
// 报错
function () {
  let a = 10;
  var a = 1;
}

// 报错
function () {
  let a = 10;
  let a = 1;
}

function func(arg) {
  let arg; // 报错
}

function func(arg) {
  {
    let arg; // 不报错
  }
}
```

## ES6块级作用域
第一种场景
``` javascript
var tmp = new Date();

function f() {
  console.log(tmp);
  if (false) {
    var tmp = "hello world";
  }
}

f(); // undefined

//上面代码中，函数f执行后，输出结果为undefined，
//原因在于变量提升，导致内层的tmp变量覆盖了外层的tmp变量。 //
```

第二种场景
``` javascript
var s = 'hello';

for (var i = 0; i < s.length; i++) {
  console.log(s[i]);
}

console.log(i); // 5
//上面代码中，变量i只用来控制循环，
//但是循环结束后，它并没有消失，泄露成了全局变量。
```

let为javascript新增了块级作用域

``` javascript
function f1() {
  let n = 5;
  if (true) {
    let n = 10;
  }
  console.log(n); // 5
}
//上面的函数有两个代码块，都声明了变量n，
//运行后输出5。这表示外层代码块不受内层代码块的影响
//如果使用var定义变量n，最后输出的值就是10。
```
### 块级作用域与函数声明
函数能不能在块级作用域之中声明，是一个相当令人混淆的问题。
``` javascript
// 情况一
if (true) {
  function f() {}
}

// 情况二
try {
  function f() {}
} catch(e) {
}
//在es5中是非法的
```
