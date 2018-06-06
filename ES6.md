## es6

###字符串和正则表达式

#####codePointAt()方法

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

