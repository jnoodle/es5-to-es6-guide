# Quick Guide of Convert ES5 code into ES6/7

推荐使用最新的 ES6/7 来优化过时的 Javascript 代码，这是简单的转换指南，欢迎补充和指出疏漏。喜欢的话给个 Star，么么哒~

**目录**

TBD


## 箭头函数 Arrow Functions

箭头函数可以简化代码，**注意 this 对象的指向，是定义时所在的对象，而不是使用时所在的对象。**


**ES5**

```js
[1, 2, 3].map(function(n) { return n * 2; });
```


**→ ES6**

```js
[1, 2, 3].map(n => n * 2);
```


## 模板字符串 Template Literals

模板字符串可以很方便的用来定义多行字符串，或者在字符串中嵌入变量。**注意所有的空格和缩进都会被保留在输出中。**

**ES5**

```js
console.log('string text line 1'
  + 'string text line 2'
  + 'total: ' + total);

```

**→ ES6**

```js
console.log(`string text line 1
string text line 2
total: ${total}`);
```


## 计算属性 Computed Property Names

**注意属性名表达式如果是一个对象，会被自动转为字符串 `[object Object]`，这里有坑。**

**ES5**

```js
var prefix = 'foo';
var myObject = {};

myObject[prefix + 'bar'] = 'hello';
myObject[prefix + 'baz'] = 'world';
```

**→ ES6**

```js
let prefix = 'foo';
let myObject = {
  [prefix + 'bar']: 'hello',
  [prefix + 'baz']: 'world'
};
```

## 解构赋值 Destructuring Assignment

解构（Destructuring）对数组、对象、字符串等都有效，可以大大简化赋值操作。

**ES5**

```js
let a = 1;
let b = 2;
let c = 3;
```

**→ ES6**

```js
let [a, b, c] = [1, 2, 3];
```


## 参数默认值 Default Parameters

使用参数默认值可以简化很多空值的判断。

**ES5**

```js
function greet(msg, name) {
  (msg === undefined) && (msg = 'hello');
  (name === undefined) && (name = 'world');
  console.log(msg, name);
}
```

**→ ES6**

```js
function greet(msg = 'hello', name = 'world') {
  console.log(msg, name);
}
```

## 类 Classes

Class 是个语法糖，让JS的写法更接近传统语言，清晰明了，也规避了一些复杂的技巧和概念。

**ES5**

```js
function Hello(name) {
  this.name = name;
}

Hello.prototype.hello = function hello() {
  return 'Hello ' + this.name + '!';
};

Hello.sayHelloAll = function() {
  return 'Hello everyone!';
};

function HelloWorld() {
  Hello.call(this, 'World');
}

HelloWorld.prototype = Object.create(Hello.prototype);
HelloWorld.prototype.constructor = HelloWorld;
HelloWorld.sayHelloAll = Hello.sayHelloAll;

HelloWorld.prototype.echo = function echo() {
  alert(Hello.prototype.hello.call(this));
};

var hw = new HelloWorld();
hw.echo();

alert(Hello.sayHelloAll());
```


**→ ES6**

```js
class Hello {
  constructor(name) {
    this.name = name;
  }

  hello() {
    return 'Hello ' + this.name + '!';
  }

  static sayHelloAll() {
    return 'Hello everyone!';
  }
}

class HelloWorld extends Hello {
  constructor() {
    super('World');
  }

  echo() {
    alert(super.hello());
  }
}

let hw = new HelloWorld();
hw.echo();

alert(Hello.sayHelloAll());
```

## 模块 Modules

之前 ES5 的一些模块加载方式可以抛弃了。

**ES5**

app.js

```js
var math = require('lib/math');
console.log('2π = ' + math.sum(math.pi, math.pi));
```

lib/math.js

```js
var pi = 3.14;
function sum(x, y) {
  return x + y;
}
exports.sum = sum;
exports.pi = pi;
```


**→ ES6**

app.js

```js
import {sum, pi} from 'lib/math';
console.log('2π = ' + sum(pi, pi));
```

lib/math.js

```js
const pi = 3.14;
const sum = function(x, y) {
  return x + y;
}

export { sum, pi };
```




