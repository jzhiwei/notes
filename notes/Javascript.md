# JavaScript

## 数据类型
#### 基本数据类型

- Undefined

	在使用 var 声明变量但并未对其初始化，这个变量的值就是 undefined

	undefined 派生自 null，null == undefined 结果为 true

- Null

	表示一个空对象指针，如果定义的变量准备在将来用于保存对象，那么最好将该变量初始化为 null， 方便对后面的判断（直接判断对象是否为 null）

- Boolean

	任何数据类型的值调用 Boolean() 函数总会返回一个 Boolean 值

	|类型|转换值为true|转换值为false|
	|:-:|:-:|:-:|
	|Boolean|true|false|
	|String|任何非空字符串|""(空字符串)|
	|Number|任何非零数值(包括∞)|0 和 NaN|
	|Object|任何对象|null|
	|Undefined|N/A(Not Applicable)|undefined|

- Number

	- 八进制
	
		字面量以 0 开头，然后是八进制数字序列(0 ~ 7)，如果超出了范围，0 将被忽略并且被当做十进制数值解析

		严格模式不支持八进制字面量

		```
		var octalNum1 = 070;	// 56
		var octalNum2 = 079;	// 79
		var octalNum3 = 08; 	// 8
		```

	- 十六进制

		以 0x 开头

	- 浮点数

		使用基于IEEE754数值计算

		```
		0.1 + 0.2 = 0.30000000000000004
		```

	- 最大值和最小值

		如果想要确定一个数值是不是在最大和最小值之间，可以使用 isFinite() 函数，如果是返回 true，否则返回 false

		如果超出范围将被转成 Infinity

		```
		最大值: Number.MAX_VALUE
		最小值: Number.MIN_VALUE
		```

	- NaN

		表示一个要返回数值的操作未能返回数值的情况（避免了抛出错误）

		任何涉及 NaN 的操作都会返回 NaN

		NaN 与任何值都不相等，包括 NaN 本身

			使用 isNaN() 函数可以判断参数是否“不是数值”。isNaN() 也适用于对象，基于对象调用该函数首先会调用对象的 valueOf()方法，然后确定该方法返回值是否可以转换为数值。如果不能，则基于这个返回值再调用 toString() 方法，再测试返回值。
			
	- 数值转换方法

		- Number()

			1. 如果是 Boolean 值，true 和 false 转换为 1 和 0
			2. 如果是数字，返回该数字
			3. 如果是 null 值，返回 0
			4. 如果是 undefined，返回 NaN
			5. 如果是字符串

				- 如果字符串只包含数字（含浮点数值），则将其转换为十进制数值（忽略前导零）
				- 如果字符串包含有效的十六进制格式，则将其转换为相同大小的十进制整数值
				- 如果是空字符串，则将其转换为零
				- 如果包含除上述格式之外的，则转换成NaN
			6. 如果是对象，先调用 valueOf()，依照前面的规则转换，如果返回结果是 NaN，在调用 toString()，再次依照前面的规则进行转换

		- Number.parseInt()

			使用该函数时提供第二个参数，可以按进制进行转换
			```
			parseInt("10",2);	// 2
			parseInt("10",8);	// 8
			parseInt("10",10);	// 10
			parseInt("10",16);	// 16
			parseInt("AF"); 	// NaN
			```

		- Number.parseFloat()

			只能解析十进制数值，没有第二个参数

			如果可解析的数是整数（没有小数点，或者小数点后面都是零），该方法会返回整数

- String

	字符串一旦创建，值就不能改变

	- toString()

		把值转成字符串的方法，null 和 undefined 没有该方法。调用该方法可以传递一个参数，表示输出进制格式的字符串

		```
		var num = 10;

		num.toString();		// 10
		num.toString(2);	// 1010
		num.toString(8);	// 12
		num.toString(10);	// 10
		num.toString(16);	// a
		```
	
	- String()

		转型函数，将任何类型的值转为字符串

		1. 如果有 toString()，调用并返回结果
		2. 如果是 null，返回 "null"
		3. 如果是 undefined，返回 "undefined"

#### 引用数据类型

- Object

	- constructor()

		用于创建当前对象的函数

	- hasOwnProperty(propertyName)

		检查属性在当前对象实例中（而不是实例的原型）是否存在

	- isPrototypeOf(object)

		检查传入的对象是否是当前对象的原型

	- propertyIsEnumerable(propertyName)

		检查给定的属性是否可以使用 for-in 来枚举

	- toLocalString()

		返回对象的字符串表示，与执行环境的地区对应

	- toString()

		返回对象的字符串表示

	- valueOf()

		返回对象的字符串、数值或布尔值表示

- Array

- - -
### DOM

- event.screenX

	鼠标距离屏幕左边的距离（针对整个屏幕，而不是浏览器）

- event.screenY

	鼠标距离屏幕上边的距离

- event.clientX

	鼠标距离浏览器视窗左边的距离（不包括水平滚动条距离）

- event.clientY

	鼠标距离浏览器视窗上边的距离（不包括工具栏，不包括垂直滚动条距离）

- event.pageX

	鼠标距离浏览器视窗左边的距离（包括水平滚动条的距离）

- event.pageY

	鼠标距离浏览器视窗上边的距离（包括垂直滚动条的距离）

- element.offsetLeft

	该元素距离其父元素左边框的距离

- 获取元素的 float 属性

	```
	element.style.float
	element.style.cssFloat	//FireFox
	element.style.styleFloat	//IE

	#兼容写法
	element.style["cssFloat" in this.style ? "cssFloat" : "styleFloat"] = "left";
	```

- 获取元素在CSS中设置的属性值

	```
	获取元素的 display 值
	element.currentStyle.display;	//IE
	window.getComputedStyle(element, null).getPropertyValue("display");
	window.getComputedStyle(element, null).display;
	```


- - -

	
		


### 引用类型
1. 为对象添加属性可以使用.的形式，也可以使用[]的形式；
2. 删除对象中的属性使用delete obj.attribute；
3. 遍历对象中的属性使用for in遍历
4. Object对象中的方法
	- constructor():构造函数；
	- hasOwnProperty(propertyName): 检测属性在当前对象实例中（而不是原型）是否存在；
	- isPrototype(object): 检查传入的对象是否上另外一个对象的原型；
	- propertyIsEnumerable(propertyName): 检查给定的属性是否能够使用for-in来枚举；
	- toLocalString(): 返回对象的字符串表示。该字符串与执行环境的地区对应；
	- toString(): 返回对象的字符串表示；
	- valueOf(): 返回对象的字符串、数值或布尔表示；

### Global对象
global是一个全局对象（实际是不存在的），global中的常用方法
- encodeURI(): 对url进行编码，只会转换一些特殊的字符，如空格；
- encodeURIComponent(): 对所有的符号进行编码，例如冒号、反斜杠；
- decodeURI(): 对url进行解码；
- decodeURIComponent(): 
- eval():
- parseInt():
- parseFloat():
- escape(): 对中文进行编码
- unescape(): 解码
- isNaN(): 

### 原型对象
在js中每一个函数都有一个prototype属性，该属性就是函数的原型对象，原型对象的constructor方法指向该函数对象；
每个实例对象都有一个隐式原型原型属性__proto__，指向了构造函数的原型对象，即

function Foo(){}
function Function(){}
function Object(){}
var foo = new Foo();

1. foo.__proto__ === Foo.prototype；
原型对象也是一个对象， 是通过Object对象的构造方法创建的，即
2. Foo.prototype.__proto__ === Object.prototype；
而Object的原型对象是一个特例，指向的是null，即
3. Object.prototype.__proto__ === null ；
Foo是一个函数，函数也是对象，是通过Function()对象创建的，即
4. Foo.__proto__ === Function.prototype；
Function对象也是通过Function函数创建的，即
5. Function.__proto__ === Function.prototype；
Object函数对象也是通过Function函数创建的，即
6. Object.__proto__ === Function.prototype；
Function的原型对象是通过Object的构造方法创建的，即
7. Function.prototype.__proto__ === Object.prototype；

判断实例对象的原型对象方法：isPrototypeOf()
Foo.prototype.isPrototypeOf(foo)； // true

获取实例对象的原型对象
Object.getPrototypeOf(foo)；	// 返回foo实例对象的原型对象

in操作符，使用in操作符可以判断属性是否存在于实例对象和原型对象中
in操作符和hasOwnProperty()方法可以判断属性是否存在于原型对象中，例如：
function hasPrototypeProperty( obj, attrName ) {
	return  !obj.hasOwnProperty(attrName) && attrName in obj ;
}

Object.keys(obj) 获取一个对象中的所有属性，不包括原型对象，返回一个数组

Object.getOwnPropertyNames(obj) 获取一个对象中的所有属性，无论该属性是否可以被枚举（constructor属性可枚举默认为false）

使用字面量的方式定义原型对象会覆盖原型对象原来的constructor方法，会使constructor指向Object对象
使用Object.defineProperty()方法重新设置原型的构造方法，3个参数
参数1: 重设构造器的对象
参数2: 要设置的属性
参数3: options对象
```
Object.defineProperty(Foo.prototype, ‘constructor’, { enumerable: false, value: Foo } );
```
使用字面量的方式定义原型，会把原型对象指向一个新的Object对象，如果在这之前创建了实例对象，那么实例对象的原型对象指向的还是原来的原型对象，即Foo.prototype，此时会找不到新原型对象中的属性和方法
```
function Foo(){}
var foo = new Foo();
Foo.prototype = { name: ‘foo’ }
console.log( foo.name ); 		// undefined
```