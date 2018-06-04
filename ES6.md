### es6

####字符串和正则表达式

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


