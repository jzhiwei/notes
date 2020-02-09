
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