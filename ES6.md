# ES6

### 字符串和正则表达式

##### codePointAt()方法

这个方法接受编码单元的位置而非字符位置作为参数，返回与字符串中给定位置对应的码位。

##### String.fromCodePoint()

这个方法根据指定的码位生成一个字符

##### normalize()方法

它可以提供unicode的标准形式，这个方法接受一个可选的字符串

```
let  arr = [2,5,3,7,8,4];
let normalized = arr.map(function(text){
	return text.normalize();
})
normalized.sort(function(first,second){
	if(first < second){
		return 1;
	}else if(first === second){
		return 0;
	}else{
		return 3;	
	}
})
```

##### 正则表达式u修饰符

当一个正则表达式添加了u修饰符时，它就从编码单元操作模式切换为字符模式。

```
let text = "吉";
console.log(/^.$/.test(text));  //false
console.log(/^.$/u.test(text)); //true
```

##### 判断引擎是否支持u修饰符

```
function hasRegExp(){
	try{
		var pattern = new RegExp(".","u");
		console.log('true');
	}catch(ex){
		console.log('false');
	}
}
hasRegExp();
```

##### 其他字符串变更

###### 字符串中的子串

includes()方法，如果字符串中检测到指定文本返回true，否则返回false;

startsWith()方法，如果在字符串的 起始部分检测到指定文本则返回true，否则返回false;

endsWith()方法，如果在字符串的结束部分检测到指定文本泽恩返回true，否则返回false;

以上方法都可以传3个参数：第一个参数指定要搜索的文本；第二个参数可选，如果给定了第二个参数，includes()方法和startsWith()方法会从这个索引值的 位置开始匹配，endsWith()方法则从字符串长度减去这个索引值的位置开始匹配；如果不指定第二个参数，includes()方法和startsWith()方法会从字符串起始位置开始匹配，则endsWith()方法会从末尾的位置开始匹配。

```
let msg = "Hello world";
console.log(msg.startsWith("Hello")); //ture
console.log(msg.endsWith("world")); //ture
console.log(msg.includes("Hello")); //ture

let msg = "Hello world!";
console.log(msg.startsWith("o",4)); //ture
console.log(msg.endsWith("o",8)); //ture
console.log(msg.includes("o",8)); //false
```

repeat()方法，其接受一个number类型的参数，表示该字符串重复多少次

```
console.log("www".repeat(3)); //wwwwwwwww
```

##### 其他正则表达式语法变更

正则表达式y修饰

##### 正则表达式复制

```
var re1 = /ab/i;
re2 = new RegExp(re1,"g");
console.log(re2)
```

```
var re1 = /ab/i;
re2 = new RegExp(re1,"g");
console.log(re2.toString());	// /ab/g
console.log(re1.toString());	// /ab/i
```

##### flags属性

```
let re = /ab/i;
console.log(re.source)	//"ab"
console.log(re.flags)	//g
```

##### 模板字面量``

##### 多行字符串 \

```
var msg = "this \
String";
console.log(msg)	//this String
```

```
var msg = "this \n\
String";
console.log(msg)	// this 
					//String
```

##### 字符串占位符${}

```
let name = "lisi";
message = `hello , ${name}`
console.log(message)	//hello , lisi
```

### 函数

#### ES5中的默认参数

```
function mark(url, timeout, callback){
  timeout = time || 2000;
  callback = callbaxk ||function(){};
}
```

```
function(url, timeout, callback){
  timeout = (typeof timeout !== "undefined") ? timeout : 2000;
  callback = (typeof callback !== "undefined") ? timeout : function(){};
}
```

#### ES6中的默认参数

```
function mark(url, timeout = 2000, callback = function(){}){
  
}
```

#### 默认参数对arguments(参数)对象的影响

```
function mixArgs(first, second){
  
}
```

#### 处理无名参数

##### ES5中的无名参数

##### ES6中添加不定参数

```
let result = Object.create(null)	//声明一个空对象
let result = new Object		//声明一个空对象
function(object, ...keys){
  
}
```

##### 不定参数的限制

不定参数有两条限制

1.每一个函数只能声明一个不定参数

2.而且要放在所有参数的末尾

##### 不定参数对arguments的影响

```
function pick(...keys){
	console.log(keys.length);
	console.log(arguments.length);
    console.log(keys[0], arguments[0]);
    console.log(keys[1], arguments[1]);

}
pick('a','b')

2
2
a a
b b
```

#### 增强的 Function构造函数

```
var add = new function("first", "second = first", "return first + second")
console.log(add(1,1));	//2
console.log(add(1));	//2
```

#### 展开运算符(...)

##### ES5中取较大的数

```
let values = [25, 50, 75, 100];
console.log(Math.max.apply(Math,values));
```

##### ES6中取最大的数

```
let values = [25, 50, 75, 100];
console.log(Math.max(...values));
```

#### name属性

ES6中函数的name属性都有一个合适的值

```
function doSomething(){
  
}
var doAnotherSthing(){
  
}
console.log(doSomething.name);	//doSomething
console.log(doAnotherSthings.name);	//doAnotherSthing
```

#### 明确函数的多重用途

#### 元属性（metaproperty）new.target

为了解决判断函数是否是通过new的关键字调用的问题，ES6中引入new.target这个元属性，元属性指非对象的属性

```
function Person(name){
  if(typeof new.target !== "undefined"){
    this.name = name;
  }else{
    throw new Error("必须通过new关键字进行调用Person")
  }
}
var person = new Person('lisi')
var notAPerson = Person.call(person,'lisi')
```

#### 块级函数

```
if(true){
  console.log(typeof doSomething);
  function doSomething(){
    //空函数
  }
}
```

在es5中代码会抛出错误，在es6中会将doSomething()是做一个块级声明，从而可以定义该函数的代码块内访问和调用它

##### 块级函数的使用场景

块级函数与let函数表达式类似，一旦执行过程流出代码块，函数 定义立即被移除。二者的区别是，在代码块中，块级函数会被提升至块的顶部，而用let定义的函数表达式不会被提升

```
if(true){
  console.log(typeof doSomething);	//此时会抛出错误
  let doSomething = function (){
    //空函数
  }
  doSomething()  
}
console.log(typeof doSomething);
```

##### 严格模式

```
"use strict"
```

#### 箭头函数

- 没有this 、super、argument、new.target绑定，箭头函数中的this、surper、arguments及new.target这些值由外围最近一层非箭头函数 决定
- 不能通过new关键字进行调用  箭头函数没有[[Construct]]方法，所以不能用作为构造函数，如果new关键字调用箭头函数，程序会抛出错误
- 没有原型 由于不可以通过new关键字调用箭头函数，因而没有构建原型的需求所以箭头函数不存在prototype这个属性。
- 不可以改变this的绑定 函数内部的this值不可以改变，在函数的生命周期始终保持一致。
- 不支持arguments对象 箭头函数没有arguments绑定，所以你必须命名参数和不定参数这两种形式访问函数的 参数。
- 不支持重复命名参数  无论在严格韩式非严格模式下，都不支持重复命名参数；而在传统函数的规定中，只有严格的模式下才不能有重复命名参数。


##### 箭头函数语法

```
let reflect = value => value
let reflect = function (value) {
  return value;
}
```

```
let sum = (num1, num2) => num1 + num2;
let sum = function (num1, num2) {
  return num1 + num2;
}
```

```
let getName = () => "lisi";
let getName = function () {
  return 'lisi';
}
```

```
let sum = (num1, num2) => {
  return num1 + num2
}
let sum = function (num1,num2){
  return num1 + num2;
}
```

创建一个空函数

```
let doNoThing = () => {};
let doNoThing = function (){};
```

```
let getTempItem = id => ({ id: id, name: "Temp"})
let getTempItem = function(id) {
  return {
    id: id,
    name: Temp,
  }
}
```

#### 创建立即执行函数表达式

javascript函数是一个流行的使用方式是创建立即执行函数表达式，你可以定义一个匿名函数立即调用，自始至终不保存对函数的 引用。当你想创建一个与程序隔离的作用域时，这种模式非常方便

```
let person = function(name) {
  return {
    getName: function(){
      return name；
    }
  }
}('lisi');
console.log(person.getName());	//lisi

let person = ((name) => {
  return {
    getName: function(){
      return name；
    }
  }
})('lisi');
console.log(person.getName());	//lisi
```

##### 箭头函数中没有this

```
let pageHander = {
	id: '1234'，
	init: function(){
		document.addEventListener("click", function(){
			this.doSomething(event.type);
		},false)
	},
	doSomething: function(type){
		console.log("handing" + type + "for" + this.id);
	}
}
```

因为this绑定的是事件目标对象的引用（在这段代码中引用的是document）而没有绑定pageHander，且且由于this.doSomething()中不存在，所以无法正常执行，尝试运行这段代码会抛出错误

```
let pageHander = {
	id: '1234'，
	init: function(){
		document.addEventListener("click", (function(event){
			this.doSomething(event.type);
		}).bind(this),false)
	},
	doSomething: function(type){
		console.log("handing" + type + "for" + this.id);
	}
}
```

它的this被绑定到当前的this也就是pageHander。事实上是创建了一个函数。

```
let pageHander = {
	id: '1234'，
	init: function(){
		document.addEventListener("click", event => this.doSomething(event.type),false)
	},
	doSomething: function(type){
		console.log("handing" + type + "for" + this.id);
	}
}
```

同样，箭头函数中的this取决于该函数外部非箭头函数的 this值，且不能通过call()、apply()或者bind()方法改变this的值。

##### 箭头函数和数组

```
var result = values.sort(function(a, b){
  return a-b;
})
var result = values.sort((a,b) => a - b)
```

##### 箭头函数的辨别

```
var sum = (num1, num2) => num1 + num2;
console.log(sum.call(null, 1, 2));
console.log(sum.apply(null, [1, 2]));
var boundSum = sum.bind(null, 1, 2);
console.log(boundSum())
```

通过条用call()、apply()、bind()方法。但与其他函数不同的是，箭头函数this值不会受这些方法影响。

##### 尾调用优化

ES6中关于函数最有趣的变化是尾调用系统引擎优化，尾调用指的是函数作为另一个函数的最后一条语句被调用，

```
function doSomething() {
  return doSomethingElse();
}
```

- 尾调用不访问当前栈的 变量（也就是说函数不是一个闭包）
- 在函数内部，尾调用是最后一条语句。
- 尾调用的结构作为函数值返回。

##### 如何利用尾调用（递归函数是主要应用场景）

```
function factorial(n) {
  if(n <= 1){
    return 1;
  }else{
    return n*factorial(n-1);
  }
}
```

