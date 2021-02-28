## ES6版本过渡历史

### babel将es6转成es5

```javascript
npm init
npm i babel-preset-env babel-cli --save-dev
新建.babelrc  {"presets":["babel-preset-env"]}
package.json->'script'->
"build":"babel index.js -out-file bundle.js(文件)"或
		:"babel src -d lib(文件夹下的文件)"
npm run build
```

### 执行index.js

```javascript
package.json -> scripts -> "script-name":"babel-node/src/index.js"
npm run script-name
cd src 
node index.js
```

## 块级作用域与嵌套、let、暂行性死区

KISS(keep it simple and stupid)原则 

解决变量污染：**函数提纯**

### let块级作用域

```javascript
if(){}else{}
for(){}
{}函数内部
```

1. 在同一作用域下不可重复声明
2. 不会变量提升，会产生暂时性死区（Temproal dead zone）
3. 只在当前作用域生效
4. 能够防止变量泄露

let本质上是为了给JS增加一个块级作用域

不建议在块级作用域中用函数声明的方式来声明函数，而是用函数表达式声明

块级作用域没有变量接收返回值，所以没有返回值



## let进阶、const、全部变量与顶层对象

### const定义常量

1. 一旦定义必须赋值
2. 有块级作用域
3. 不能变量提升，会产生暂时性死区
4. 同一作用域下不可重复声明



const obj=[ ] 定义的数据是**引用值**，**栈内存**中保存的是指向堆内存的地址不变，但存储在**堆内存**中的数据可以改动

解决办法：通过Object.**freeze**(obj) 冻结



## 解构赋值、函数默认值、数组解构、对象解构

### 函数默认值

```javascript
function foo(x,y) {
	var x = x || 1;
} //当x为0时，会取||后的数
```

#### 解决办法：

##### ES5：

```javascript
var a = typeof(argument[0]!=='undefined'? argument[0]:1)
```

##### ES6:

```javascript
function foo(x=1, y=2) {
	...
}
```

相当于在独立作用域中let x=1 let y =2



### 解构赋值

```javascript
let [a,b,c] = [1,2,3]
```

**模式匹配**，结构化赋值

- 解构失败：变量个数大于值，没有值的变量为undefined
- 不完全结构：变量个数小于值



解构赋值可传默认值，默认值可以为函数

```javascript
function foo(){console.log(1)};
let [a = foo()] = [] 
// 输出 1
// 再输出undefined  因为函数返回值为undefined
```



### ES6对象的简写

```javascript
var name = 'leah',
	age = 20;
var person = {
	name,
	age，
	eat(){...}
}
//当属姓名与属性值相同时可简写
//方法也可简写
```

### 对象属性拼接

```javascript
var fname = 'leah',
	lname = 'zheng',
	age = 20;
let person = {
	[fname + lname]:age
}
//{'leah zheng':20}
```

### 对象的解构

相同属性名

```javascript
let {a,b,c} = {a:1,b:2,c:3}

var person = {
    son:{
        name:'leah',
        son:{
            name:'mike'
        }
    }
}
var {son:{son}} = person // son:{name:'mike'} 
var {son:{son:son1}} = person //son1:{name:'mike'} 
```

```javascript
let a1 = [1,2,3],obj2 = {};
[obj2.a,obj2.b,obj.c] = a1
//给对象的属性声明并赋值，但没有单独声明变量
```

用let，var声明解构赋值加（）会报错

```javascript
let a;
({a}={a:1}) //变成表达式
//a = 1 不报错

//报错
let ({a}={a:1})
let {(a)}={a:1}
let {a}={(a:1)}
```

函数的参数不能加（）

```javascript
function foo(([a])){
	...
} //报错 函数的形参相当于let ([a]),而let不能加[]
```

###  数组的解构赋值

数组是特殊的对象，也能进行解构赋值

```javascript
let arr = [1,2,3]
let {0:first,[arr.length-1]:last} = arr;
//first:1 last:3
```



## 隐式转换、函数参数解构、解构本质、()用法

### 变量的值的交换

```javascript
let a = 1,b = 2;
[a , b] = [b , a];
```

### 模式匹配可以匹配同源属性

```javascript
let {a = x,a = y} = {a :1}
console.log(x,y)// 1,1
```

### 函数传参解构赋值

```javascript
function foo([x,y]){
	console.log(x,y)
}

foo([]) //undefined undefined
foo({x:1,y:2}) // 1 2
```

### 函数传参默认值

```javascript
function foo({x=10}={},{y}={y=10}){
	console.log(x,y)
}
foo()  //10 10
foo({},{}) // 10 undefined
foo({x:2},{y:3}) // 2 3
```

### 解构赋值隐式转换

undefined和null不能

```javascript
const [a,b,c,d,e,f] = 'hello'; => 类数组
const {length:len} = 'hello' =>类数组
	console.log(len) // 5
let {toString:s} = 123; 
	console.log(s === Number.prototype.toString());
```

函数的形参一旦给了默认值，形参和实参的映射关系不复存在

## this指向、箭头函数基本形式、rest运算符

### this指向

1.  默认绑定规则  window （严格模式下undefined
2.  隐式绑定：谁调用指向谁
3.  显示绑定：call apply bind
4.  new指向实例化对象

### 箭头函数表达式

```javascript
let f = (a,b) => a + b //语句只有一条且return执行结果时可简写
```

#### 结合解构赋值

```javascript
const full = ({fitst,last}={}){
	return first + " " + last;
}
console.log(full({first:1,last:2}))  // 1 2
```

#### sort排序

```javascript
var arr1 = arr.sort((a,b)=>a-b); 
```

```javascript
const sortNum = (...args) => args.sort((a,b)=> a-b)
```



**箭头函数不能使用arguments**

### rest运算符(展开或收集)

```javascript
var sum = (...args) => {
	console.log(args[0],args[1])
}
sun(1,2,3)  //1,2  //收集

let fn = (a,b,...c)=>{ //收集 rest必须是最后一个参数
    console.log(a,b,c)
}
fn(1,2,3,4,5,6,7) 
```

```javascript
function foo(x,y,z) {
	console.log(x,y,z);
}
foo(...[1,2,3]) // 1，2，3 //展开
```

## 箭头函数的实质、箭头函数的使用场景

### 箭头函数的实质

1. this指向由外层函数作用域决定
2. 箭头函数不能作为构造函数来使用，不能使用call，apply，bind
3. 没有argument对象，用rest拓展运算符代替
4. 在generator函数中，yield命令不生效

this的指向是固化的，箭头函数内部并没有自己的this，只能通过父级作用域获取this(闭包产生的this)

因为箭头函数本质上是不通过function定义的，而是通过=>旁箭头定义的



**闭包**：一个函数的执行导致另一个函数的定义

### 箭头函数的使用场景

1. 简单的函数表达式，得出唯一的return的计算值

2. 函数内部没有this的引用，没有递归，事件绑定

3. 内层函数表达式，需要调用this，如bind(this)确保this指向的时候

4. 引用Array.prototype上的方法时，用...代替

   const sortNum = (...args) =>args.sort((a,b)=>a-b)



```javascript
let insert = (value) => ({
	intro:array => ({
		after:afterVal=>{
			array.splice(array.indexOf(afterVal)+1,0,value)
		}
	})
})
//箭头函数返回值为对象时要加()
inset(5).intro([1,2,3,4,6,7]).after(4)

```

## 函数名/对象拓展、描述符、getter/setter

### 获取函数的名称

function.name  / (new Function).name

```javascript
foo.bind({}).name  // bound foo
foo.call({}) // 报错
```

### 对象属性名可以拼接

```javascript
let a = 'hh',b = 'xx';
let obj = {
	[a + b]:123
}
//对象的属性名为字符串
```

当对象的属性名为对象时，会调用Object.prototype.toString方法，属性名就会变成[object Object]

### es5属性描述符

```javascript
Object.getOwnPropertyDescriptor(obj,'name') //获取对象属性

Object.defineProperty(obj,'a',{
    value:1,
    configurable:true, //可配置的
    enumberable:true, //可枚举的
    writable:true  //可写
})
```

注：当writable：false时，**delete** obj.a 还是能删除，同时设置configurable：false才能阻止被删除

定义多个属性defineProperties

查看多个属性描述 getOwnPropertyDescriptors

### getter/setter

访问器属性：一组设置和获取值的函数，

getter负责获取值，不带任何参数，

setter负责设置值，在它的函数体中一切的return都是无效的

```javascript
var obj = {
	a:3,
	get val(){
		return this.a
	},
	set val(n){
		this.a = n
	}
}
console.log(obj.val)  // 3
obj.val = 100;
console.log(obj.val)  // 100
```

在对象内设置了存取器属性，如果某一变量只声明了**getter**方法，那么它仅仅只**可读不可写**，如果只声明了**setter**方法，那么该变量永远为**undefined**

### 获取访问器属性的getter和setter方法的属性

```javascript
var discriptor = Object.getOwnPrppertyDescriptor(obj,'val');

console.log(discriptor.get.name)
```

## 对象密封4种方式、assign、取值函数的拷贝

### 对象密封4种方式

##### 阻止拓展，不能添加

```javascript
var obj = {a:2}
Object.preventExtensions(obj);
console.log(Object.isExtensible(obj)) //false
//这两个方法都在Object原型上
```

##### 设置属性描述符

```javascript
obj.b = 2 //该情况下，属性描述符全是true

Object.defineProperty(obj,'a',{
	value:2
}) //该情况下，属性描述符全是false
```

##### 对象的密封

```javascript
//configurable：false不能配置
Object.seal(obj)
console.log(Object.isSealed(obj)) //查看密封情况
```

##### 对象的冻结

```javascript
Object.freeze(obj)
console.log(Object.isFreeze(obj)) //查看冻结状况
```

深度冻结

```javascript
function deepFreeze(obj){
	Object.freeze(obj);
	for(var key in obj){
		if((typeOf (obj[key])==='object')&&obj[key]!==null){
			deepFreeze(obj[key])
		}
	}
}
```



### assign

```javascript
Object.is(NaN,NaN)  //true
Object.is(-0,+0)  //false
```

#### 可枚举对象的拷贝enumerable:true

```javascript
Object.assign(tar(目标对象),obj，...(被拷贝对象，可添加多个，重复值会覆盖))  //浅拷贝
```

#### 特殊目标对象

```javascript
var test = Object.assign(1,{a:1}) 
//包装类 Number(1,{a:1})
//注：undefined，null不能包装类，作为目标对象时会报错
```

#### 特殊被拷贝对象

```javascript
const test1 = 'abc',test2 = 10,test3 = false;
Object.assign({},test1,test2,test3) 
// {0:'a',1:'b',2:'c'}
//字符串转成类数组能够枚举，而数字和布尔值不行
```

assign的特性：

- assign不能拷贝继承属性和不可枚举属性

- Symbol类型的值也能拷贝

- 同名属性替换是将全部属性值替换

- 数组的替换

  Object.assign([1,2,3],[4,5])   // [4,5,3]

#### 利用assign配置默认参数

```javascript
const Default={host:'www.baidu.com'};
function test(option){
	option = Object.assign({},default,option)
}
//若有传入参数option，那么会覆盖Default默认值
```

#### 获取访问器属性的属性描述

```javascript
//Object.assign 无法拷贝
const sourse = {
	set foo(value){
		console.log(value)
	}
}
const tar = {};
Object.defineProperties(tar,Object.getOwnPropertyDescriptors(sourse));

console.log(Object.getOwnPropertyDescriptors(tar,'foo'));
```

#### 克隆obj

```javascript
var obj = {
	a:1,
	b:2,
	c:3
}
const clone = obj =>{
	Object.getPrototypeOf(obj),
	Object.getOwnPropertyDescriptors(obj)
}

const obj2 = clone(obj)
```

### 三种对象部署方式

```javascript
const obj = Object.create(prototype);
obj.foo = 123;
```

```javascript
const obj = Object.assign(Object.create(prototype),{foo:123});
```

```javascript
const obj = Object.create(prototype,Object.getOwnPropertyDescriptors({foo:123}))
```



### 更改原型

person.__ proto __ = {...} 

缺点：1.语义化，内部属性 2.访问效率慢  3.所有继承自该属性的对象都会影响到

```javascript
Object.getPrototypeOf(读取)
Object.create(原型,{对象属性}) //生成
Object.setPrototypeOf(obj,prototype) //直接修改obj的原型
```

### 可枚举属性

```javascript
Object.keys(obj) //自身可枚举的键名(不含继承属性)
Object.values(obj) //自身可枚举的键值(不含继承属性)
Object.entires(obj) //自生可枚举的键值对(不含继承属性)
//返回的都是数组
//obj为字符串时转包装类
```



## super、4种遍历方式、原型、symbol遍历

### super

指向对象的原型，相当于this

只在对象的简写方法中生效 foo(){...}

### symbol原始值

创建一个独一无二的值(并不是字符串)

解决对象属性重名的问题

```javascript
Symbol(obj) // Symbol([object Object]) 调用toString
Symbol(undefined) //Symbol()
Symbol(null) // Symbol(null)
```

Symbol不能通过Number转，

显示转换可以通过String、Boolean，

隐式转换限于boolean         ！Symbol // false

Symbol不是构造函数

Symbol原型上的方法： toString()   for()   keyfor()

#### 设置Symbol属性

```javascript
let name = Symbol(), eat = Symbol();
const person = {};
let person = {
	[name]:'leah',
	[eat](){
		console.log(this[name])
	}
}

person[eat]() // leah
```

#### for和keyfor

```javascript
Symbol.for('foo') === Symbol.for('foo')  //true 
Symbol('foo') === Symbol.for('for') //false

Symbol.keyfor('foo')  // 'foo'
//获取唯一标识符
```

注：

1. Symbol作为对象属性名时，不能用点运算符(点运算符后总是字符串)
2. 在对象内部时使用Symbol定义属性时，Symbol值必须放在**方括号**之中，方括号中的属性名代表了Symbol值
3. Symbol值作为属性名时，该属性还是公开属性

#### 属性循环

- for...in遍历自身和继承的可枚举属性(不包含Symbol类型)
- Object.keys 遍历自身可枚举属性，不包含Symbol类型
- Object.getOwnPropertySymbols 遍历自身的Symbol类型值，不论是否可枚举
- Object.assign({},obj) 遍历并拷贝自身可枚举的，包含Symbol类型





## interator迭代器

对数据结构读取的一种方式，有序的连续的，基于拉取的一种消耗数据的组织方式

已部署iterator的数据类型：array、number、Map、Set、weakMap、weakSet、argument、nodeList、TypeArray

```javascript
let arr = [1,2,3,4];
let iter = arr[Symbol.interator]();
iter.next()// {value:1,done:false}
iter.next()// {value:2,done:false}
iter.next()// {value:3,done:false}
iter.next()// {value:4,done:false}
iter.next()// {value:undefined,done:true}
```

```javascript
function makeInterator(arr){
	var nextIndex = 0;
	return {
		next:function(){
			return nextIndex >arr.length ?
				   {value:arr[nextIndex++],done:false}:
				   {value:undefined,done:true};
		}
	}
}
```

给没有interator的数据类型，如对象，自行添加iterator

```javascript
var obj = {
	start:[1,2,3],
	end:[4,5,6],
	[Symbol.interator](){
		let index = 0 ,
			arr = [...this.start,...this.end],
			len = arr.length;
		return {
			next(){
				if(index < len){
					return {value:arr[index++],done:false};
				}else{
					return {value:undefined,done:true};
				}
			}
		}
	}
}
```

foo instanceof Foo  //  判断Foo是否为foo的构造函数

Foo[Symbol.hasInstance] (foo)  // 判断Foo是否为foo的构造函数



for...of适用于遍历数组、map、set等拥有迭代器对象的集合，但不能遍历对象，因为对象没有迭代器

for...in 适用于遍历对象的键名



给对象部署iterator

```javascript
let obj = {
	a:1,
	b:2,
	c:3,
	[Symbol.iterator]:function(){
		let nextIndex = 0;
		let map = new Map();
		for(let [key.value] of Object.entries(this)){
			map.set(key,value);
		}
		let mapEntries = [...map.entries()];
		return {
			next(){
				return nextIndex < mapEntries.length?
						{value:mapEntries[nextIndex++],done:false}:
						{value:undefined,done:true}
			}
		}
	}
}

for(let i of obj) {
	console.log(i)
}

//['a',1]
//['b',2]
//['c',3]
```

##  map与set

### set

```javascript
var set = new Set(参数)  //成员是唯一的"数组"
//参数是具备iterator接口的数据结构，如数组、类数组
```

```javascript
set.add() 添加值，返回set结构本身
set.size  数据结构的长度，像防御length
set.delete() 删除值，返回是否删除的布尔值
set.clear() 清空值，返回undefined
set.has()  判断是否存在值，返回布尔值
注：delete与clear实时生效，与代码上下位置无关
```

```javascript
set.keys() 返回迭代器对象，不存在键名
set.value() 返回迭代器对象，键名与键值相同
set.enrties() 返回键值对迭代器对象
Set.prototype[Symbol.iterator] === Set.prototype.values
```

```javascript
for(let value of set){
	console.log(value)
}
//遍历set的值与遍历set.values的值相同
```

##### 数组去重

```javascript
let set = new Set([1,2,3,2,4,2,3]);
res = [...set] // [1,2,3,4]
//...展开运算符展开具备iterator接口的数据结构
```

##### 数组翻倍

```javascript
let set = new Set([1,2,3])
let set1 = new Set([...set].map(val =>{val * 2}))
let set2 = new Set(Array.from(set,value => value * 2))
```

##### 过滤偶数

```javascript
let set2 = new Set([...set].filter(x => (x % 2)==0))
```

##### 交集、并集、差集

```javascript
let a = new Set([1,2,3]),b = new Set([4,3,2]);

let union = new Set([...a,...b])  //交集
let intersect = new Set(...a.filter(x => b.has(x))) //并集
let difference = new Set(...a.filter(x => !b.has(x))) //差集
```

当对象的键名为对象时，会隐式调用Object.toString(),将键名转成[object,Object],就不能实现建与值一一对应

### Map

键与值一一对应的“对象”

```javascript
let m = new Map([["name","leah"],["age",20]]) //参数为双元的数组形式，具备iterator接口的数据结构
```

##### 设置键值

```javascript
m.set('name','leah')
```

键名相同时会覆盖

##### 获取键值

```javascript
m.get(键名)
//键名为引用值时要注意，使用指针做键名(var arr= [1,2,3])
```

```javascript
map.set(-0,123);
map.get(+0,123) //123

NaN ===NaN //false
Object.is(NaN,NaN)// true
```

```javascript
m.size  //键值对的个数
m.delete(键名) //返回是否删除的布尔值
m.clear() //返回undefined
m.has(键名) //返回是否存在键值对的布尔值
m.set(键名，键值) //返回map实例，可以链式调用
注：delete与clear实时生效，与set相同
```

```javascript
m.keys() //返回键名的迭代器对象
m.values() //返回键值的迭代器对象
m.entries()//返回键值对的迭代器对象
m[Symbol.iterator] === m.entries
```

##### 模式匹配

```javascript
for(let [key,value] in m){
	console.log(key,value);
}
```

##### map结构转数组

```javascript
var arr = [...m]
```

##### map结构转对象

```javascript
//条件：键名为字符串
function strMapToObj(strMap){
	let obj = Object.create(null);
	for(let [key,value] of strMap){
		obj[key] = value
	}
	return obj;
}
```

##### 对象转成map

```javascript
function objTostrMap(obj){
	let map = new Map();
	for(let key in obj){
		map.set(key,obj[key])
	}
	return map;
}
```



## WeakMap与WeakSet、proxy与reflect

### WeakMap与WeakSet

1. 不存在遍历方法
2. 成员只能是对象，weakMap的键名要为对象
3. 不计入垃圾回收机制引用次数，若引用次数不为0，垃圾回收机制就不会释放内存（弱引用）



### proxy代理

```javascript
let star = {
	name:'leah',
	age:20,
	phone:1223423
}
let agent = new Proxy(star,{
	get:function(target,key){
		if(key==='phone'){
			return 'agents phone 12223333'
		};
		if(key==='price'){
			return 10000
		}
		return target[key];
	},
	set:function(target,key,value){
		if(value < 5000){
			throw new Error('价格太低');
		}else{
			target[key] = value;
			return true;
		}
	},
	has:function(target,key){
		if(key === 'customousPrice'){
			return target[key]
		}else{
			return false;
		}
	}
	
})

console.log(agent.phone) //agents phone 12223333
console.log(agent.price) //10000
agent.customousPrice = 15000
console.log('customousPrice' in agent) //true
					
```

### reflect

Reflect上定义了一系列操作函数，映射了Proxy对象上的一系列操作方法

在目标对象与源对象中间设置了代理层，目标对象无法直接访问源对象，因此设置具有拦截功能的代理，对拦截的功能进行处理

## 类、类的继承、类的实现、类的修饰

```javascript
Object.getPrototypeOf(person) //获取实例化对象的原型
Object.getPrototypeOf(person).constructor = Person

class Person {
    constructor(name='leah',age=20){
        this.name = name;
		this.age = age;
        //私有属性  实例化的属性配置
    }
	say(){
        console.log(`my name is ${this.name}`)
    }
    //公有属性  原型上的方法
}
```

Object.keys(Person.prototype)普通构造函数的原型可枚举，而class构造函数原型上的方法(公有属性的方法)不可枚举，返回[]

```javascript
class Person{ }
new Person() 
//会默认添加上constructor
```

##### 函数表达式

```javascript
let person = new class{
	constructor(name){
		this.name = name;
	}
	say(){
		console.log(this.name);
	}
}
```

##### class不能函数提升，存在暂时性死区

##### class没有公有属性

```javascript
class Person {
	a = 1
}
//默认将a=1放入constructor变为私有属性
```

##### 公有方法私有化

- 将方法名变为Symbol类型的值，独一无二

  ```javascript
  const eat = Symbol();
  class Person {
  	[eat](){
  		console.log(1)
  	}
  }
  ```

- 将私有方法定义在class外部，公有方法可以调用该方法，但实例化对象无法调用

静态方法和属性static，作为类的属性和方法，而不是实例化对象的

##### getter和setter

```javascript
class Person(){
	get a(){
		console.log(1) //取值函数
	}
	set b(value){
		console.log(value) //存值函数
	}
}
let person = new Person()
person.a  //1
person.b = 2 //2
```

##### class内部默认严格模式

### 类的继承

```javascript
class Parent{
	constructor(name="leah"){
		this.name = name
	}
}
//派生类
class Child extends Parent{
	constructor(age=20,name='zheng'){
		super(name);//返回父级的实例，继承父类的当前属性
		//super必须在constructor内部
		this.age = age;
	}
}

console.log(new Child);
```

1. 在constructor里以函数形式来执行super
2. 当super为对象时，在对象中指代对象的原型，在静态方法中指向自己的父类



class总结：

- 暂时性死区TDZ
- 严格模式
- 不可枚举
- new
- 不传参不会报错

## 异步的开端-promise

### Js的运行原理

进程：是计算机中的程序关于数据结合上的一次运行活动，是系统进行资源分配和调度的基本单位

多进程：启动多个进程，多个进程可以一块来执行多个任务

单线程：进程内一个相对独立的、可调度的执行的单元，同一时间只能做一件事

多线程：启动一个进程，在进程内部启动多个线程，多个线程可以一块执行多个任务

浏览器是多进程的，浏览器渲染引擎是多线程的



1. JS引擎线程（单线程）     解释和执行JS代码     //1和2是互斥的
2. GUI线程：渲染用户界面
3. http网络请求线程     //3、4、5是webAPIs
4. 定时器触发线程
5. 浏览器事件处理线程



Js的运行原理：JS引擎线程(单线程)，同时执行异步执行(基于事件驱动)

 

任务进入执行栈，先判断同步还是异步任务，同步任务进入主线程，异步任务调用相应webAPIs线程，注册回调函数后挂起，等待事件被触发。

异步线程中的事件被触发就会进入事件队列，等主线程中的同步任务全部执行完毕，就会到事件队列中取出一个异步事件进入主线程执行，先取出微任务，再取出宏任务执行，基于先进先出原则，然后反复监听同步和异步队列



异步：

- 宏任务：script、setTimeout、setInterval
- 微任务:  Promise、process、nextTick

webApis先将微任务放入任务队列，再放入宏任务



所有的异步代码都是以回调函数的方式出现，单并不是所有的回调函数都是异步代码

### Promise

- try...catch只能捕获同步异常，难于捕获回调异常
- 回调地狱难于维护，不便拓展
- 同步并发异步代码的问题

PromiseA+规范定义了promise相关行为和方法

promise是避免回调地狱的一种解决方案

- promise对象的状态不受外界影响

  1. padding 进行中
  2. fullfill(resolve) 已成功
  3. reject 已失效

- 状态的不可逆

  promise状态固化后再对promise对象添加回调是可以直接拿到结果的，若是事件的话，错过即错过



```javascript
let promise = new Promise((resolve,reject)=>{
	setInterval(function(){
		Math.random()*100 > 60 ? resolve() : reject()
	},1000);
})
promise.then(
	()=>console.log('及格'),
	()=>console.log('不及格')
)
```

第一次then的返回值作为下一次then的执行参数，从而实现链式调用



推荐写法：

```javascript
let promise = new Promise((resolve,reject)=>{
	resoleve(a) //undefined ->reject捕获
}
promise.then(null)
	   .catch(reason=>console.log(reason))
```

##### 状态固化

```javascript
let promise = new Promise((resolve,reject)=>{
	resolve('ok') // resolve状态固化，但不会终止函数运行
	console.log(a) // 忽略 
})
//catch能够通过冒泡捕获前面的所有错误，状态固化后，无法捕获错误 
//.then没有填参数会被忽略
```

##### 状态依赖

```javascript
const p1 = new Promise((res,rej)=>{
	setTimeout(()=>{
		reject(new Error('fail'))
	},3000)
})
const p2 = new Promise((res,rej)=>{
	setTimeout(()=>{
		resolve(p1)
	},1000)
})
```

p2先执行，执行到resolve传入参数p1

p2依赖于p1的状态，等p1执行完毕后才能传入参数

p1执行后状态固化为reject，抛出错误



##### Promise原型上的方法

```javascript
Promise.all([p1,p2,p3]) //参数为iterator对象 需要所有promise成功执行，才返回成功结果的数组，用then捕获，若失败则返回第一个失败的信息
```

```javascript
Promise.rase([p1,p2,p3]) //只要有一个promise执行，不论成功或失败都会返回率先执行的promise的结果，成功用then捕获，失败用catch捕获
```

##### thenable对象转成promise对象

```javascript
let thenable = {
	then:(res,rej)=>{
		res('ok')
	}
}
let p1 = Promise.resolve(thenable)
p1.then(function(value){console.log(value)})
```

##### 异步函数promise化(避免回调地狱)

```javascript
function readFile(path){
	return new Promise((resolve,reject)=>{
		fs.readFile(path,'utf-8',(err,data)=>{
			if(data){
				resolve(data)
			}
		})
	})
}
reasFile('./name.txt')
.then(data=>readFile(data))
.then(data=>readFile(data))
.then(data=>readFile(data))
```

##### 异步函数promise化封装函数

```javascript
function promisify(func){
	return function(...arg){
		return new Promise((resolve,reject)=>{
			func(...arg,(err,data)=>{
				if(err){
					reject(err)
				}
				resolve(data)
			})
		})
	}
}
```

node已将promisify封装到util中