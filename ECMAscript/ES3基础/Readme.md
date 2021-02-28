# ECMAscript

## 发展史、ECMA、编程语言、变量、JS值

### 5大主流浏览器的内核

- IE	          trident
- chrome    webkit blink
- safari        webkit
- firefox       gecko                                                                                                                                                                                                
- opera        presto

### 浏览器的历史和js诞生

1. 1990    蒂姆·伯纳斯·李  超文本分享资讯的人

   world wide web 移植到C  =>libwww=>nexus

   允许别人浏览他人编写的网站

2. 1993  美国伊利诺大学NCSA组织（马克·安德森）开发了MOSIAC浏览器（图形化浏览器）能够显示图片

3. 1994  马克·安德森和吉姆·克拉克（硅图SGI）成立MOSIAC communication corporation

   MOSIAC =>伊利诺大学=>spy glass公司=>Netscape communication corporation

   网景公司=>Netscape navigator  =>2003

4. 1996  

   1. 微软的公司收购spy glass

   =>IE  1.0

   ​	IE3  JScript

   ​	2. 网景公司Brendan eich在Netscape navigator开发出了livescript(javascript前生) 

   3. SUN的JAVA有知名度，网景livescript不温不火，网景与sun合作推广和宣传产品，livescript=>javascript

5. 2001  IE6 xp诞生

   ​			JS引擎

6. 2003   Mozilla公司  firefox => 根据Netscape navigator复制

7. 2008   google基于webkit blink gears

   chrome =>V8=>JS引擎

   1. 直接翻译机器码
   2. 独立于浏览器运行

8. 2009  甲骨文oracle收购了sun公司

   ​			JS 所有权给甲骨文

### ECMA

European Computer Manufactures Association 欧洲计算机制造联合会

评估、开发、认可电信、计算机标准

ECMA-262 脚本语言规范  ECMAScript

ES5 ES6 规范化脚本语言

### 编程语言

高级语言：人能理解机器不能理解

编译器  解释器

翻译过程不同：

编译性语言：源码=>编译器=>机器语言=>可执行的文件；适合写逻辑性强的大型项目

解释性语言：源码=>解释器=>解释一行执行一行； 不需要根据不同的系统平台进行移植，速度更快一些，

.java =>javac=>.class=>JVM解释执行

C++ .cpp源码=>编译器=>.s汇编=>汇编器=>.obj目标代码=>链接器=>可执行文件

脚本语言：

​	=>脚本引擎=>解释器

javascript客户端脚本：解释器在浏览器

 php服务端脚本：解释器在服务器

### JavaScript

ECMAscript

DOM  document object model  W3C

BOM  browser object model   没有规范

JS引擎是单线程引擎

单线程：一次只能执行一个任务

​				=>如何模拟多线程  

​	**轮转时间片**：短时间之内轮流执行多个任务片段

1. 任务1 任务2...
2. 切分任务
3. 随机排列任务片段，组成队列
4. 按照这个队列顺序将任务片段送进JS进程
5. JS线程执行一个又一个的任务片段

多线程：一次能同时执行多个任务

```
<script type='text/javascript'></script>
```

编程语言必备：变量、数据结构、函数、运算能力

### 变量

```js
var a;  //变量声明
a=3;	//变量赋值
var a=3 //变量声明并赋值
```

变量命名规范：

- 不能以数字开头，能字母_$开头
- 变量里可以包含字母_$数字
- 不能以关键字、保留字命名
- 驼峰命名法 小驼峰 大驼峰

**先运算>再赋值**

### JS值

#### 原始值->基本类型（5种）

- Number 数字
- String 字符串
- Boolean 布尔值
- undefined 未被定义
- null 空值

#### 引用值

- object
- array
- function
- date
- RegExp

### 变量空间存储原始值和引用值

```js
var a = 3,
	b = a;
var a = 1;
```

原始值存储在栈内存，先进后出。重新给a赋值会开辟新的内存空间并赋值，原来的值保持不变，只是对应的名称不在了。

![](https://s1.ax1x.com/2020/08/12/ajOhKf.png)

```
var arr1 = [1,2,3,4,5],
	arr2 = arr1;
var arr1 = [1,2];
```

引用值的实际数据存储在堆内存，而栈内存中存储的只是指向堆内存的地址。将arr1的值赋值给arr2，其实就指向同一个堆内存的地址。

![](https://s1.ax1x.com/2020/08/12/ajjWB8.png)

给arr1重新赋值就是在栈内存中开启新的空间，存储指向存在堆内存中的新数据的地址。

![](https://s1.ax1x.com/2020/08/12/ajv93R.png)

## 语法、规范、运算符、判断分支、注释

### 运算符

 **// +  -  *  /  % （）**

```js
var a = 1,
	b = 2,
	d = 3;
var c = (a + b) * d;
```

声明变量c

=>变量a的值和变量b的值相加，再与变量d的值相乘得到结果

=>将该结果赋值给变量c

总结：括号运算>普通运算>赋值

**// + 数学运算**

```js
var a = 1 + 'str'  													// '1str'
var b = 'str' + undefined 											// 'strundefined'
var c = 'str' + NaN 												//'strNaN'
//任何数据类型的值+字符串都是字符串
```

**// / 除法**

```js
var a = 0 / 0;  								// NaN(not a number非数)=>数字类型
var b = 'a' / 'b' 								// NaN
var c = 1 / 0 									//infinity =>数字类型
```

**// % 取余**

```js
console.log(3 % 4)							// 3
console.log(4 % 3) 							// 1
```

**交换值的问题**

```js
var a = 1,
	b = 2;
var c = a;
a = b;
b = c;
```

```js
a = a + b;  // 3
b = a - b;  // 1
a = a - b;	// 2
```

**// ++  --**

```js
var a = 1;
console.log(a++)  // 1
console.log(a)	  // 2
console.log(++a)  // 3
```

案例题:

```js
var a = 5,
	b;
b = a++ + 1;
console.log(b, a)	// 6,6
b = ++a + 1;
console.log(b, a)   // 7,6
b = a-- + --a      
console.log(b, a)	// 8,3
b = --a + --a
console.log(b, a)	// 7,3
b = --a + a++
console.log(b, a)	// 8,5
```

**// 比较运算符 > < >= <= == === !== !=**

```js
var bool = 1 < 2 // true
var bool = 1 > 2 // false
var bool = 1 > '2' // false
//number对string=>number
var bool = 'a' > 'b' // false
var bool = '4.5'>'11' // true
//字符串相对应的ASCII码(字符相对应的十进制代码)多个字符的，从左到右依次对比，直到比较出ASCII码的大小为止
var bool = 1 == '1' // true
var bool = 1 === '1' // false
//相等不看数据类型，全等要看数据类型是否相等
var bool = 1 !== '1' //true
//不全等与全等相同，要看数据类型
var bool = NaN == NaN  //false
//NaN与包括自己在内任何东西都不相等
```

**逻辑运算符**

```js
A && B // A与B 两边都必须满足条件
A || B // A或B 其中一边满足条件即可
!A     // 非A 
```

undefined、null、NaN、""、0都是假false

除以上以外都是真 true

**逻辑运算**

```
var a = 1 && 2; 
//遇到真就往后走，
遇到假或走到最后一个就返回当前值
var b = 1 || 2;
//遇到假就往后走，
遇到真或者走到最后就返回当前值
console.log(a, b) // 2,1

//1 && 1 返回1  真
//1 && 0 返回0  假
//0 && 1 返回0  假
//0 && 0 返回0  假
//1 || 1 返回1  真
//1 || 0 返回1  真
//0 || 1 返回1  真
//0 || 0 返回0  假
```

```
var a = !1  //false
a = !a  // 取反
```



### 判断分支

**判断范围或值为多个时用if语句**

```js
if(判断条件){
...
}else{
...
}
```

**判断定值时用switch**

```js
switch(变量){
	case 值：
	语句；
	break；
	case 值：
	语句；
	break；
	...
	default 语句；
}
```

两种方法实现判断成绩等级：

```js
var score = 78；

if(score <= 100 && score >=90 ){
	console.log('A');
}else if(score >= 80) {
	console.log('B')
}else if(score >= 70){
	console.log('C')
}else if(score >= 60){
	console.log('D')
}else if(score >= 0) {
	console.log('不合格')
}else {
	console.log('成绩出现异常')
    
switch(true){
    case score <= 100 && score >=90:
        console.log('A');
        break;
    case score >= 80 && score <=90:
        console.log('B');
        break;
    case score >= 70 && score <=80:
        console.log('C');
        break;
    case score >= 60 && score <=70:
        console.log('D');
        break;
    case score >= 0 && score <=60:
        console.log('不合格');
        break;    
    default：
    	console.log('成绩出现异常')
}
```

### 注释

```js
//行注释

/*
 *块注释	
 */
```

## 循环、引用值初识、显示及隐式类型转换

### 循环

```js
for(var i = 0;i < 10; i++) {
	console.log(i)
}
```

1.  声明变量i = 0
2.  if(i < 10) { console.log(i) }
3.  i++

可以写成⬇

```js
var i = 0;
for(;i<10;){
	console.log(i);
	i++
}
```

与上面写法相似的while语句:

```js
var i = 0;
while(i < 10){
	console.log(i);
	i++;
}
```

do...while无论条件是否成立都先执行一次

```js
var i = 0;
do{ 
	console.log(i);
	i++;
}while(i<10)
```

条件一直满足就会造成死循环，需要将条件转换为false才能跳出死循环

```js
var i = 1;
for(;i;){
	console.log(1);
	i++
	if(i == 11){
		i = 0; // break
	}
}
```

从0开始做加法，加到总和小于100

```js
var sum = 0;
for(let i = 0; i < 100; i++) {
	sum += i;
	if(sum >= 100){
		break;
	}
}
```

打印100以内的数跳过可以被7整除或个位数是7的数

```js
var sum = 0;
for(let i = 0;i <= 100;i++) {
	if(i % 7 == 0 || i % 10 == 7){
		continue;
	}else{
		console.log(i)
	}
}
```

打印可以被4，5，6整除的数

```js
for(let i = 0; i <= 100; i++){
	if(i % 4==0 || i % 5 == 0 || i %6 == 0) {
		console.log(i);
	}
}
```

打印0-100的数，()只能有一句，不能写比较 {}不能出现i++ i-- 

```js
var i = 100;
for(;i--;){
	console.log(i)
}
```

10的N次方

```js
var n = 5;
var num = 1;
for(let i = 0;i < n ;i++){
	num *= 10;
}
```

n的阶乘

```js
var n = 5;
var sum = 1;
for(let i = 1;i <= n; i++){
	sum *= i;
}
```

将数字倒写

```js
var num = 123；

var a = num % 100;  //3
var b = (num - a)/10 % 10 // 2
var c = (num - a - b*10) / 100 //1

console.log(''+a+b+c) // 321
```

打印三个数中最大的数

```
var a = 3,
	b = 5,
	c = 1;
if(a>b){
	if(a>c) {
		console.log(a)
	}else{
		console.log(c)
	}
}else{
	if(b>c){
		console.log(b)
	}else{
		console.log(c)
	}
}
```

打印100以内的质数（只能被自身或1整除的数）

```js
var count = 0;
for(let i = 2;i < 100; i++){
    for(let j = 1;j<=i;j++){
        if(i % j == 0){
            count++;
        }
    }
    if(count==2){
        console.log(i)
    }
    count = 0
}
```

### 引用值初始

**//array数组**

```js
var arr = [1, 2, 3];
console.log(arr[1]) // 2
console.log(arr.length) //3
```

**//object对象**

```js
var person = {
    name:'Leah',
    //属性名/键名：属性值/键值
    age:18
}
console.log(person.name) // 'leah'
```

**typeof**

- number
- string
- boolean
- object=> object、array、null
- function
- undefined

```js
console.log(a) // 报错 引用错误 a is not defined
console.log(typeof(a)) // undefined
console.log(typeof(typeof(a))) //string
```

### **显式类型转换** 

#### number

```js
var a = '123';
console.log(Number(a)) // 123
var a = 'true'
console.log(Number(a)+'-'+typeof(Number(a))) // NaN-number
var a = true;
console.log(Number(a)+'-'+typeof(Number(a))) // 1-number
var a = null;
console.log(Number(a)+'-'+typeof(Number(a))) // 0-number
var a = undefined;
console.log(Number(a)+'-'+typeof(Number(a))) // NaN-number
var a = 'a';
console.log(Number(a)+'-'+typeof(Number(a))) // NaN-number
var a = '1a';
console.log(Number(a)+'-'+typeof(Number(a))) // NaN-number
var a = 'NaN'; 
console.log(Number(a)+'-'+typeof(Number(a))) // NaN-number
```

##### **praseInt()**

```js
var a = '123';
console.log(parseInt(a)+'-'+typeof(parseInt(a))) // 123-number
var a = true;
console.log(parseInt(a)+'-'+typeof(parseInt(a))) // NaN-number
var a = null;
console.log(parseInt(a)+'-'+typeof(parseInt(a))) // NaN-number
var a = undefined;
console.log(parseInt(a)+'-'+typeof(parseInt(a))) // NaN-number
var a = NaN;
console.log(parseInt(a)+'-'+typeof(parseInt(a))) // NaN-number
var a = '12a12';
console.log(parseInt(a)) // 12
```

```js
var a = 10
console.log(parseInt(a, 16)) // 16
var a = 'b'
console.log(parseInt(a, 16)) // 11
var a = 'abc123'
console.log(parseInt(a, 16)) // NaN
var a = '123abc'
console.log(parseInt(a, 16)) // 123
```

##### parseFloat()

```js
var a = parseFlaot('3.145926');
console.log(a.toFixed(2)) //3.14 四舍五入
```

#### String()

```js
console.log(String(123)) // '123'
console.log(123+'')  //'123'
```

##### toString()

```
console.log(undefined.toString()) //报错
console.log(null.toString()) //报错
```

#### Boolean

```js
console.log(Boolean(1)) // true
console.log(Boolean(null)) // false
undefined  null  NaN "" 0 false 
其他的都是true
```

### **隐式类型转换**

```js
console.log(typeof(1 -'1')) //number
console.log(typeof('1'-'1'))//number
console.log('a' + 1) //'a1'
// * / % - str-> number
console.log('1' > 2) //false
//> < >= <= 经过number类型转换后对比
console.log(1 == '1') //true
console.log(1 != '2') //true
console.log(1 === '1') // false数据类型不同，不进行隐式类型转换
console.log(NaN == NaN)//false 

var a1 = 2>1>3;
var a2 = 2>1==1;
console.log(a1,a2) //false,true

var a1 = undefined > 0 //false
var a2 = null > 0 //false
var a3 = undefined < 0 //false
var a4 = null < 0 //false
var a5 = undefined = 0 //false
var a6 = null = 0 //false
var a = undefined == null //true
var a = undefined === null //false

console.log(+'123':typeof(+'123'))// 123-number
console.log(-'123':typeof(-'123'))// -123-number
console.log(+'abc':typeof(+'abc'))// NaN-number
```

##### isNaN

```js
console.log(isNaN(NaN)) // true
console.log(isNaN(123)) // false
console.log(isNaN('123')) // false
console.log(isNaN('a')) // true
console.log(isNaN(null)) // false
console.log(isNaN(undefined)) // true
//Number(值)->NaN->bool
```

##### 练习题：

```js
var a = false + 1;
console.log(a)

//1
```

```js
var a = false == 1;
console.log(a)

//false
```

```js
if(typeof(a)&&(-true)+(+undefined)+''){
    console.log('通过了')
}else{
    console.log('没通过')
}
//typeof(a)->'undefined' 
//(-true)+(+undefined)+''->-1+NaN+''->'NaN'
//通过了
```

```js
console.log(!!' ' + !!'' - !!false || '未通过')
//!!' '->true
//!!'' - !!false ->0-0
//1
```

```js
window.a || (window.a = '1');
console.log(window.a)
//括号优先级最大，先赋值
//'1'
```

```js
//打印true的有哪些？
console.log(undefined==null)
console.log(undefined===null)
console.log(isNaN('100'))
console.log(parseInt('1a')==1)

//1 4
```

```js
{}=={} //false
//引用值比较存储地址
//如何使其相等？
var obj1 = {}
obj2 = obj1
obj1 == obj2
```

## 函数基础与种类、形实参及映射、变量类型

### 函数基础与种类

一个固定的功能或程序段被封装的过程，实现一个固定的功能或是程序，在这个封装体中需要一个入口和一个出口，入口就是参数，出口就是返回

编程原则：**高内聚，低耦合**

让一个模块具有强的功能性、高的独立性

​	=>模块的单一责任制

用函数能够很好的解耦合

#### 最基本的函数写法 - **函数声明**

```js
function test (形参){
	函数的执行语句；
}
test(实参)
```

#### **匿名函数表达式**  **函数字面量**

```js
var test1 = function (参数) {
	函数的执行语句;
}
------------------------------
var test1 = function test(参数) {
	函数的执行语句;
    test(); //可以在函数内部调用，但外部不可见
}
console.log(test1.name) // test 
test()  // 报错
```

#### **函数名的命名规则：**

- 不能数字开头
- 可以字母_$开头，中间可以包括数字
- 小驼峰命名法

### 形实参及映射

```
			//形式上占位->形式参数->形参
function test (a, b, c) {
	console.log(a, b, c)
	console.log(arguments.length) //实参的个数
	console.log(test.length) // 形参的个数
}
tset(1,2)
//实际参数，实参
// 1 2 undefined
```

形参和实参数量可不等，通过arguments可以获得所有实参

一个函数被调用时，累加它的实参值

```js
function sum() {
    var s = 0
	for(let i = 0;i < arguments.length; i++){
		s += arguments[i]
	}
    console.log(s)
}
sum(1,2,3,4)
```

调用函数时传入了实参，在函数内部能够更改实参的值

 形参存储在栈内存中，实参存储在堆内存，但它们之间存在一一对应的映射关系

```js
function test(name){
	return name || '您没有填写'
}
console.log(test())
```



### 函数式编程

一个固定的功能或程序段被封装的过程，实现一个固定的功能或程序，在这个封装体中需要一个入口和出口，入口就是参数，出口就是return

## 参数默认值、递归、预编译、暗示全局变量

### 参数默认值

```js
//初始化参数  默认值:undefined 
//es6 
function test(a=1,b){
	console.log(a,b)
}
test(undefined,2) //1,2
//低版本浏览器不兼容
function test(a,b){
	var a = arguments[0]||1;
    var b = arguments[1]||2;
}
//三目运算
function tset(a,b){
    var a = typeof(arguments[0])!=='undefined'? arguments[0]: 1;
}
```

实参与形参存在映射关系，谁不是undefined就选谁

### 递归

##### n的阶乘

```js
function fact(n){
	if(n == 1){
		return 1;
	}
	return n * fact(n-1);
}
```

##### 斐波那契数列

```js
function fb(){
	if(n <= 0){
		return 0
	}
	if(n <= 2){
		return 1
	}
	return fb(n-1)*fb(n-2)
}
```

### 预编译

JS引擎：1. 检查通篇语法错误

​				1.5**预编译过程**:函数执行之前的步骤

​				2.解释一行，执行一行

函数声明整体提升，变量只有声明提升、赋值不提升

**暗示全局变量**：未声明，被赋值，存在window对象中

```js
a = 1
```

在函数内部**未声明**的变量会提升到**全局作用域**。



#### AO : activation object 函数执行上下文

1. 寻找形参和变量声明
2. 实参赋值给形参
3. 找函数声明并赋值
4. 执行

```js
function test(a){
	console.log(a);
	var a = 1;
	console.log(a);
	function a(){};
	console.log(a);
	var b = function(){};
	console.log(b);
	function d(){}
}
test(2) 
//function a(){} 
//1 
//1 
//function(){}
```

```js
function test(a,b){
	console.log(a);
	c = 0;
	var c;
	a = 5;
	b = 6;
	console.log(b);
	function b(){};
	function d(){};
	console.log(b)
}
test(1)
AO:{
    a:undefined
    ->1
    ->5
    b:undefined
    ->function b(){}
    ->6
    c:undefined
    ->0
    d:function d(){}
}
//1
//6
//6
```

### GO:global object 全局执行上下文

1. 寻找变量声明
2. 寻找函数声明
3. 执行

```js
var a = 1;
function a(){
	console.log(2);
}
console.log(a)
GO:{
    a:undefined
    ->function a(){}
    ->1
}
```

```js
console.log(a,b);
function a(){}
var b = function(){}
GO:{
	a:function a(){}
	b:undefined
	->function(){}
}
//function a(){},undefined
```

##### 综合练习题：

```js
var b = 3;
console.log(a);
function a(a){
    console.log(a);
    var a = 2;
    console.log(a);
    function a (){}
    var b = 5;
    console.log(b);
}
a(1)
GO:{
    b:undefined
    ->3
    a:function a(){}
}
AO:{
    a:undefined
    ->1
    ->function a(){}
    ->2
    b:undefined
    ->5
}
//function a(){}
//function a(){}
//2
//5
```

```js
a = 1;
function test(){
    console.log(a);
    a = 2;
    console.log(a); 
    var a = 3;
    console.log(a)
}
test();
var a;
GO:{
    a:undedined
    ->1
    test:function test(){}
}
AO:{
    a:undefined
    ->2
    ->3
}
//undefined
//2
//3
```

```js
function test(){
	console.log(b);
	if(a){
		var b = 2;
	}
	c = 3;
	console.log(c);
}
var a;
test();
a = 1;
console.log(a)
GO:{
    test:function test(){}
    a:undefined
    ->1
    c:3
}
AO:{
    b:undefined
}
//undefined
//3
//1
```

```js
function test(){
	return a;
	a = 1;
	function a(){};
	var a = 2;
}
console.log(test())
AO:{
    a:undefined
    ->function a(){}
}
//function a(){}

```

```js
function test(){
    a = 1;
    function a(){}
    var a = 2;
    return a;
}
console.log(test())
AO:{
    a:undefined
    -> function a(){}
    ->1
    ->2
}
//2
```

```js
a = 1;
function test(e){
    function e(){};
    arguments[0]=2;
    console.log(e);
    if(a){
        var b = 3'
    }
    var c;
    a = 4;
    var a;
    console.log(b);
    f = 5;
    console.log(c);
    console.log(a)
}
var a;
test(1)
console.log(a);
console.log(f);
GO:{
    a:undefined
    ->1
    test:function test(){}
    f:5
}
AO:{
    a:undefined
    ->4
    b:undefined
    c:undefined
    e:1
    ->function e(){}
    ->2
}

//2
//undefined
//undefined
//4
//1
//5
```

```js
var a = '1';
function test(){
	var a = '2';
	this.a = '3';
	console.log(a)
}
test();
new test();
console.log(a);

GO = {
    a : '1'
    ->'3'
    test:fn
}
AO = {
    a:'2'
    
}
//'2' '2' '3'
```

## 作用域、作用域链、预编译、闭包基础

//函数也是一种对象类型 引用类型

//test.name test.length test.prototype

//有些属性是无法访问的，JS引擎内部固有的属性

### [[scope]]

- 函数创建时生成的一个隐式属性
- 函数储存作用域链的容器，作用域链存储AO函数执行期上下文、GO全局执行期上下文

当函数执行完成以后，AO会被销毁，也就是说每次执行函数都会生成新的AO

> AO是一个即时的存储容器
>
> 每一个函数的作用域链上都有GO

### 作用域与作用域链

```js
function a(){
    function b(){
        var b = 2;
    }
    var a = 1;
    b();
}
var c = 3;
a();
```

[![dCCHQf.png](https://s1.ax1x.com/2020/08/14/dCCHQf.png)]()
[![dCCqOS.png](https://s1.ax1x.com/2020/08/14/dCCqOS.png)]()
[![dCCoWt.png](https://s1.ax1x.com/2020/08/14/dCCoWt.png)]()
[![dCCby8.png](https://s1.ax1x.com/2020/08/14/dCCby8.png)]()
[![dCC7SP.png](https://s1.ax1x.com/2020/08/14/dCC7SP.png)]()
[![dCCjoj.png](https://s1.ax1x.com/2020/08/14/dCCjoj.png)](https://imgchr.com/i/dCCjoj)
[![dCCXwQ.png](https://s1.ax1x.com/2020/08/14/dCCXwQ.png)]()
[![dCCOeg.png](https://s1.ax1x.com/2020/08/14/dCCOeg.png)]()

### 闭包

**当内部函数被返回到外部并保存时**，就会产生闭包，闭包会使得原来的作用域链不被释放

过度的闭包可能导致内存泄漏或加载过慢

```js
function test1(){
	function test2(){
		var b = 2;
		console.log(a);
	}
	var a = 1;
	return test2();
}
var c = 3;
var test3 = test1();
test3();
```

![dCi3vV.png](https://s1.ax1x.com/2020/08/14/dCi3vV.png)
![dCiGuT.png](https://s1.ax1x.com/2020/08/14/dCiGuT.png)
![dCiJDU.png](https://s1.ax1x.com/2020/08/14/dCiJDU.png)
![dCil3q.png](https://s1.ax1x.com/2020/08/14/dCil3q.png)
![dCi1g0.png](https://s1.ax1x.com/2020/08/14/dCi1g0.png)

```js
function test1(){
    var n = 100;
    function add(){
        n++;
        console.log(n);
    }
    function reduce(){
        n--;
        console.log(n)
    }
    return [add,reduce]
}

var arr = test()
arr[0]();  //101
arr[1]();  //100
```

#### 返回数组 面包管理后台:

```js
 function breadMg () {
     var breadNum = arguments[0] || 10;
     function supply(){
         breadNum += 10;
         console.log(breadNum);
     }
     function sale (){
         breadNum--;
         console.log(breadNum);
     }
     return [supply,sale]
 }
var breadMg = breadMg(50)
breadMg[0]()  // 60
breadMg[1]()  // 59
```

#### 返回对象 周末计划：

```js
function sunSche() {
    var sunThing = '';
    var orperation = {
        setSche:function(thing){
            sunThing = thing;
        },
        showSche:function(){
            console.log('I will'+ sunThing+' in this Sunday')
        }
    }
    return orperation;
}
var sunSche = sunSche();
sunSche.setSche('sleep');
sunSche.showSche();
```

## 立即执行函数、闭包深入、逗号运算符

### 立即执行函数IIFE（初始化函数）

immeditately-invoked function expression

**自动执行**，执行完成以后**立即释放**

> 写法一：(function() { } )()

> 写法二：(function() {} () )  // W3C建议

#### **传参、返回值：**

```js
// 将返回值交给一个变量保存
var num = (function(a,b){
    return a+b; 
})(1,2)
```

### （）表达式：

（）里面包裹的内容会成表达式，函数用()包裹就变成了函数表达式

只有表达式才能被立即执行符号()执行

```js
var test = function(){}()
function test(){}() // 报错
```

#### 函数声明变为表达式之后会**忽略函数名**

```js
(function test(){ })()
(function(){ })()
```

##### 案例一：

```js
var a = 10；
if(function b(){}){
	a+= typeof(b)
}
console.log(a)

//(function b(){})视为表达式，忽略函数名
//b就是undefined
//输出'10undefined'
```



#### 函数声明变为表达式的方法:

```js
(function test(){ })()
+function test(){ }();
-function test(){ }();
!function test(){ }();
1 && function test(){ }()
0 || function test(){ }()
```



```js
function test(a,b){
	
}(1)
//不报错，JS引擎把(1)当作一个表达式
//括号里不写内容就会报错
```

### 闭包深入

##### 案例一：

```js
function test(){
    var arr = [];
    var i = 0;
    for(;i<10;){
        arr[i] = function(){
            document.write(i+' ')
        }
        i++
    }
    return arr;
}
var myArr = test();
for(var j = 0;j < 10;j++){
    myArr[j]()
}
//10 10 10 10 10 10 10 10 10 10 
// 经过10次循环，arr中装着10个匿名函数，连接着test的AO，test执行完毕将arr返回到全局，test与其AO断开连接，但arr中的10个匿名函数连接着AO还未执行，所以AO不能销毁，闭包带出的AO中的变量i，经过10次循环后已经变成了10，因此在执行每个匿名函数时输出10

//解决办法：
//方法一 立即执行
function test(){
    for(var i = 0;i<10;i++){
       (function(){
            document.write((i+1) +' ')
        })()
    }
}
//1 2 3 4 5 6 7 8 9 10

//方法二
function test(){
    var arr = [];
    for(var i = 0;i<10;i++){
        (function(j){
            arr[j] = function(){
            document.write(j+' ')
        	}
        })(i)
    }
    return arr;
}
var myArr = test();
for(var j = 0;j < 10;j++){
    myArr[j]()
}

//方法三
function test(){
    var arr = [];
    var i = 0;
    for(;i<10;){
        arr[i] = function(num){
            document.write(num +' ')
        }
        i++
    }
    return arr;
}
var myArr = test();
for(var j = 1;j < 11;j++){
    myArr[j](j)
}
```



##### 案例二：

```html
<body>
    <ul>
        <li>1</li>
        <li>2/li>
        <li>3</li>
        <li>4</li>
        <li>5</li>
    </ul>
    <script>
    var lis = document.querySelectorAll('li');
        for(var i = 0;i < lis.length;i++){
            lis[i].onclick = function(){
                console.log(i)
            }
        }
// 点击每一个li输出都是5
//改为立即执行
     var lis = document.querySelectorAll('li');
        for(var i = 0;i < lis.length;i++){
            (function(j){
                lis[j].onclick = function(){
                console.log(j)
            }
            })(i)
        }
//点击每一个li输出对应的i
    </script>
</body>


```



### 逗号运算符

()里的，是运算符，只返回逗号的最后一项

```js
console.log((4,2)) // 2
```

##### 案例一：

```js
var fn = (
	function test1(){
		return 1
	},
	function test2(){
		return '2'
	}
)()
console.log(typeOf(Fn))

//string
```



## 对象、构造函数、实例化

### 对象

```js
var obj={
	name:'leah',
	age:18,
    weight:80,
	say:function(){
		console.log('i said something')
	},
    smoke:function(){
        this.weight--;
        console.log(this.weight)
    },
    eat:function(){
        this.weight++;
        console.log(this.eat)
    }
}
```

- 增  obj.sex = 'female'
- 删  delete obj.say
- 改  obj.name = 'Anna'
- 查  obj.age

```js
var attendance={
	students:[],
	total:5,
	join:function(name){
		this.students.push(name);
		if(this.students.length == this.total) {
			console.log(name+'到课，学生已到齐')
		}else{
			console.log(name+'到课，学生未到齐')
	},
	leave:function(name){
		var i = this.students.indexOf(name);
		if(i !== -1){
			this.students.splice(i,1);
		}else{
			console.log('该班级没有此学生')
		}
		console.log(name + '早退')
	}
}
```

#### 创建对象的方式：

1. **对象字面量**：声明一个变量，将对象赋值给这个变量

   ```js
   var obj = {
       name:'leah'
   }
   ```

2. **构造函数**：系统自带的构造函数

   ```js
   var obj = new Object();
   obj.name = 'leah'
   ```

   对象是通过实例化构造函数而创建的一个对象实例

3. **自定义构造函数**

   ```js
   		//大驼峰
   function Person(opt){  //传入一个对象opt
   	this.name = opt.name;
       this.sex = opt.sex
       this.say = function(){
           console.log('i am saying')
       }
   }
   var person1 = new Person({
       name:'leah',
       sex:'female'
   });
   var person1 = new Person({
       name:'tom',
       sex:'male'
   });
   //this指向实例化对象
   //通过一个构造函数构造出的多个对象相互之间是不影响的
   ```

   

   ## 构造函数及实例化原理、包装类

### 构造函数中的this

- 没有实例化构造函数时，this指向window
- 实例化构造函数后，this指向实例化对象，不指向构造函数本身 

```js
GO = {
    Person : (function),
    p1 : {
        name:'leah',
        age:20
    }
}
AO = {
    this = {
      name : name,
      age : age
	}
}
function Person(name,age){
    //this = {
    //  name : name,
    //  age : age
	//}
	this.name = name;
	this.age = age;
    //return this;
}
var p1 = new Person('leah',20)
//当构造函数被实例化时，构造函数被执行，生成自己的AO，自动保存this,this指向实例化对象，所以通过p1.name能够访问到属性值
```

new关键字隐式给实例化对象添加了this对象和return this

new其实就是把原本指向window的this转向实例化对象了

去掉new自行添加一个对象并返回这个对象并赋值也能实现this的效果：

```js
function function Person(name,age){
    var me = {}
	me.name = name;
	me.age = age;
    return me;
}
var p1 = Person('leah',20)
```

在构造函数最后**return引用值**会覆盖掉this对象

```js
function Person(name,age){
	this.name = name;
	this.age = age;
    return {};
}
var p1 = new Person('leah',20)
p1.name // undefined
```

### 包装类

- 原始值没有自己的方法和属性 
- new Number new String new Boolean

```js
var test = new Number(undefined);
console.log(test) // Number{NaN...}
var test = new Number(null);
console.log(test) // Number{0...}
var test = new String(undefined);
console.log(test) // String{'undefined'}
var test = new String(null);
console.log(test) // String{'null'}

//undefined和null不能设置任何属性与方法
console.log(undefined.length) // 报错
console.log(null.length)  // 报错
```

### 包装类的过程

原始值没有自己的方法和属性 

```JS
var a = 123; //原始值
a.len = 3；
//new Number(123).len = 3
//delete 
console.log(a.len)
//undefined
//第一步：JS引擎隐式将原始值包装成类 new
//第二步：添加自定义属性并赋值
//第三步：没有变量接收保存不了，删除包装类
```

```js
var a = new Number(123); //包装类
a.len = 3；
```

```js
var str = 'abc'; //原始值
//String类里有length属性
// new String('abc').length
console.log(str.length) // 3
```

```js
var str = 'abcde'  //原始值
str.length = 3;
//new String('abcde').length = 3
//delete
console.log(str) //'abcde'
```

### 数组截断的方法

```js
var arr = [1,2,3,4,5]  //引用值
arr.length = 3;
console.log(arr) //[1,2,3]
```

### 例题

```js
var name = 'leah';
name += 10;  // 'leah10'
var type = typeof(name);  //'string'
if(type.length === 6){    // true
    type.text = 'string'  
    //new String(type).text = 'string' 
    //delete
}  
console.log(type.test)

//undefined

//修改：
var type = new String(typeof(name)); 
//'string' 
```

```js
function Car(brand,color) {
    this.brand = 'Benz';
    this.color = 'red';
}
var car = new Car('Mazda','blank')
console.log(car.brand)
console.log(car.color)

//'Benz'
//'red'
```

```js
function Test(a,b,c){
	var d = 1;
	this.a = a;
	this.b = b;
	this.c = c;
	function f(){
		d++;
		console.log(d)
	}
	this.g = f;
    //return this 形成闭包
    //f带走了Test的AO
}
var test1 = new Test();
var test2 = new Test();
test1.g();
test1.g();
test2.g();
//2
//3
//2
```

```js
var x = 1,
	y = z = 0;
function add(n){
	return n = n + 1;
}
y = add(x);
function add(n){
	return n = n + 3;
}
z = add(x)
console.log(x,y,z)

GO = {
    x:1
    y:0
    ->4
    z:0
    ->4
    add:function add (n){return n = n + 1}
	->function add (n){return n = n + 3}
}
//1 4 4
```

```js
//下列函数哪个能输出1，2，3，4，5？
function foo(x){
	console.log(arguments);
	return x;
}
foo(1,2,3,4,5);

function foo(x){
	console.log(arguments);
	return x;
}(1,2,3,4,5)

(function foo(x){
	console.log(arguments);
	return x;
})(1,2,3,4,5)

//第一个 第三个
```

```js
function b(x,y,a){
	a = 10;  //映射关系
	console.log(arguments[2])
}
b(1,2,3)

//10
```

##    原型、原型链、闭包立即执行函数、插件开发

### 原型prototype

prototype是定义构造函数构造出的每个对象的公共祖先。

所有被该构造函数构造出的对象都可以继承原型上的属性和方法。

一般把组件的**方法**写在其**原型**上，需要**传参配置的属性**放在**构造函数**上。

##### 通过实例化对象增删改查prototype：

```js
function Test(){}
Test.prototype.name = 'prototype';
var test = new Test();
console.log(test.name) // 查
test.num = 1;
console.log(Test.prototype,test)//不能增
delete test.name;
console.log(Test.prototype) //不能删
test.name = 'proto';
console.log(Test.prototype) //不能改
```

**构造函数的prototype上的constructor：**指向构造函数本身

```js
Test.prototype.constructor -> Test;
```

**__ proto __属于每个实例化对象**，而不是构造函数

```js
function Car(){
	var this = {
		__ proto__:Car.prototype
	}
}
Car.prototype.name = 'Benz';
var car = new Car()
console.log(car)
// 实例化之后，构造函数中隐式增加了this对象，this中增加了__ proto__指向Car.prototype
//若this中没有name属性，就会到_ proto_里的prototype找
```

在实例化之前，Car本身有prototype，里面有name ：'Banz'

实例化之后，this存在了，this里面会存有__proto _，指向构造函数的prototype，将构造函数原型里的name ：'Banz'赋值给实例对象的原型

之后再给构造函数的原型赋值不影响已经实例化的对象

```js
function Car(){
    //var this = {
    //	__proto__:Car.prototype{
    //		name ：'Banz'
    //  }
	//}
}
Car.prototype.name = 'Banz';
var car = new Car()//已经实例化
Car.prototype = { //再次重写
	name:'Mazda'
}
console.log(car.name)  // 'Banz'
```

 

### window和return

```js
function tset(){
	var a = 1;
	function add(){
		a++;
		console.log(a)
	}
	window.add = add;
}
test()
```

```js
var add = (function(){
	var a = 1;
	function add(){
		a++;
		console.log(a)
	}
	return add;
})()
add();
add();
add();
```

```js
(function(){
	var a = 1;
	function add(){
		a++;
		console.log(a)
	}
	window.add = add;
})()
add();
add();
add();
```

return必须把返回的值用一个全局变量接收，然后再执行这个全局变量；

使用window能直接在函数内部给window添加一个变量，再把需要抛到全局的值赋值给变量

### JS插件写法：

```js
;(funciton(){ //立即执行函数
	funciton Test(){};
	Test.prototype = {}
	window.Test = Test;
})();

var test = new Test()
```

防止作用域污染

## 原型与原型链深入、对象继承

原型也是对象，原型本身上有原型，原型链的顶端是Object.prototype

沿着proto去找原型里的属性，一层一层继承原型里的属性的链条叫原型链

```js
Professor.prototype.tSkill = 'Java'
function Professor(){};
var professor = new Professor();

Teacher.prototype = professor
function Teacher(){
	this.mSkill = 'js',
    this.success = {
        alibaba:28,
        tencent:30
    },
    this.students = 500
};
var teacher = new Teacher();

Student.prototype = teacher;
funciton Student(){
	this.pSkill = 'HTML/css'
}
var student = new Student()

console.log(student)
student.success.baidu = 29;
console.log(teacher,student)
//引用值可以修改
student.students++;
console.log(teacher,student)
//原始值不可以修改
//teacher的值不变
//student增加students属性赋值500并++为501
```

##### 例题

```js
function Car(){
	this.brand = 'Banz';
}
Car.prototype = {
	brand:'Mzada'
	intro:function(){
		console.log('我是'+this.brand)
	}
}
var car = new Car
car.intro()
//'我是Banz'
Car.prototype.intro()
//'我是Mzada'
//实例化this指向实例化对象
```

构造函数默认返回this，普通函数默认返回undefined

```js
function Person(){
    //this={
    //	weight = 129
	//}
    this.smoke = function(){
        this.weight--;
    }
}
Person.prototype = {
    weight:130
}
var person = new Person();
person.smoke() 
//this.weight = this.weight -1
//Person原型上的weight没有改变，实例化对象的this从原型上取到weight并添加到this对象中，  再-1
```

```js
var a = 5;
function test(){
	a = 0;
	console.log(a);
    console.log(this.a);
	var a;
	console.log(a)
}
test()
new test()

//0 5 0 
//0 undefined 0
```



### 声明对象的方法

- 对象字面量

  ```js
  var obj = {} 
  //constructor指向Object
  ```

- 构造函数

  ```js
  var obj = new Object()
  //constructor指向Object
  ```

- 自定义构造函数

  ```js
  function Obj(){}
  var obj = new Obj()
  //constructor指向自定义构造函数Obj
  ```

#### Object.create

```js
//Object.create(对象||null)创建对象
function Obj(){}
Obj1.prototype.num = 1;
var obj1 = Object.create(Obj.prototype);
var obj2 = new Obj()
//obj1与obj2实例化出的对象相同
// Object.create()可以自定义原型
```

### new

1. 实例化obj2
2. 调用构造函数Obj上的初始化属性和方法
3. 指定实例对象的原型

#### Object.prototype

不是所有的对象都能继承Object.prototype

当Object.create(null)时，不继承Object.prototype

```js
var obj = Object.create(null);
var obj1 = {
	count:2
}
obj.__proto__ = obj1;

console.log(obj) // undefined 可以自行添加__proto__属性，但没有无法实现系统内置的继承功能
```



### 包装类

undefined、null不能包装类，所以不能使用toString

原始值没有属性，但是通过包装类可以获取类原型上的属性和方法

```js
var num = 1
num.toString()
// new Number(num)
//Number的prototype上有toString()方法
```

### 对象继承

```js
var num = 1;
var obj={};
var obj2 = Object.create(null);
document.write(num) // 1
document.write(obj) //[object Object]
document.write(obj2) //报错 不能将对象转换成原始值
//obj继承Object.prototype，原型中有toString()方法
//obj2没有继承Object.prototype，也就没有toString()方法
```

### 原型方法的重写

```js
Object.prototype.toString.call(true) //[object Boolean]
Object.prototype.toString.call([1,2]) //[object Array]
Object.prototype.toString.call('a') //[object String]
Object.prototype.toString.call({}) //[object Object]
Object.prototype.toString.call(1) //[object Number]
Number.prototype.toString.call(1) //'1'
```

###  call和apply

**改变this的指向**

```js
function Car(brand,color){
    this.brand = brand;
    this.color = color;
}
var newCar = {}
Car.call(newCar,'Benz','red')
Car.apply(newCar,['Benz','red'])
```

例题

```js
function Compute(){
	this.plus = function(a,b){
		console.log(a+b)
	}
}
funciton FullCompute(){
	Compute.apply(this);
	this.minus = function(a,b){
		console.log(a-b)
	}
}
var compute = new FullCompute()
compute.plus(1,2)
compute.minus(1,2)
```

## 继承深入、call_apply、圣杯模式、模块化

### call_apply

借用其他构造函数的属性与方法             

```js
Teacher.prototype.wife = 'Ms.Liu';
function Teacher(name, mSkill){
    this.name = name;
    this.mSkill = mSkill;
}
function.Sturdent(name,mSkill,age,majer){
    Teacher.call(this,name,mSkill);
    this.age = age;
    this.majer = majer;
}
var student = new Student('leah','js',20,'computer')
console.log(student)
//借用了Teacher的属性和方法，但没有继承Teacher的原型
```

#### 练习题：

```js
function foo(){
	bar.apply(null,arguments)
}
function bar(){
	console.log(arguments) //空
}
foo(1,2,3,4,5)

//1,2,3,4,5
//bar()->bar.call(arguments)->bar(a
rguments)
```

## 对象继承——圣杯模式     

### **原型的继承和隔离**      

创建一个缓冲器(构造函数)，将被继承的构造函数的prototype赋值给缓冲器的prototype，将缓冲器new出的实例化对象赋值给继承的构造函数的prototype，这样修改继承的原型prototype就不会影响到被继承函数的prototype                                                                                

```js
function Teacher(){
    this.name = 'Mr.li';
    this.mSkill = 'JAVA';
}
Teacher.prototype = {
    pSkill:'js'
};
var t = new Teacher()
function.Sturdent(r){
    this.name = 'Wr.Wang';
}
-------------------------------
function Buffer(){}
Buffer.prototype = Teacher.prototype;
var buffer = new Buffer()
Student.prototype = buffer;
-------------------------------
Student.prototype.age = 18'
var student = new Student()
```

### 继承函数封装

```js
function inherit(Target,Origin){
	function Buffer(){};
    Buffer.prototype = Origin.prototype;
    Target.prototype = new Buffer();
    Target.prototype.constructor = Target;
    Target.prototype.super_class = Origin;
}
```

```js
var inherit = (function(){
	var Buffer = function(){};
	return function(Target,Origin){
		Buffer.prototype = Origin.prototype;
   		Target.prototype = new Buffer();
    	Target.prototype.constructor = Target;
    	Target.prototype.super_class = Origin;
	}
})()
```



### 模块化开发

防止变量的全局污染，有利于后期维护

```js
;var inherit =(function (){
	function Buffer(){}	
	rerutn function (Target,Origin){
        Buffer.prototype = Origin.prototype;
        Target.prototype = new Buffer();
        Target.prototype.constructor = Target;
        Target.prototype.super_class = Origin;
    }
})()
```

防止变量的全局污染，有利于后期维护

```js
var inherit = (function() {
    function Buffer() {};
    return function(Target, Origin) {
           Buffer.prototype = Origin.prototype;
           Target.prototype = new Buffer();
           Target.prototype.constructor = Target;
           Target.prototype.super_class = Origin;
    }
})()

var initProgrammer = (function() {
    function Programmer() {};
    Programmer.prototype = {
         work: '程序员',
         tool: '电脑',
         intro: function() {
           console.log('我是一名' + this.name + this.work + ',我用' + this.tool + '编写' + this.lang.toString());
         }
     }

    function FrondEnd() {}

    function BackEnd() {}

    inherit(FrondEnd, Programmer);
    inherit(BackEnd, Programmer)

    FrondEnd.prototype.name = '前端';
    BackEnd.prototype.name = '后端';
    FrondEnd.prototype.lang = ['js', 'css', 'html'];
    BackEnd.prototype.lang = ['node', 'sql', 'java'];

    return {
         FrondEnd: FrondEnd,
         BackEnd: BackEnd
    }
})()

var frondEnd = new initProgrammer.FrondEnd();
var backEnd = new initProgrammer.BackEnd();
console.log(frondEnd);
frondEnd.intro()
backEnd.intro()
```

不立即执行，按需执行

```js
;(function(){
	var Slider = function(opt){
		...
	}
	Slider.prototype = {
		...
	}
	window.Slider = Slider
})()

var slider = new Slider({
	...
})
```

立即执行，插件封装

##  闭包的三种形式

1. 返回普通函数

   ```js
   function test (){
   	var num = 0;
   	function compute(){
   		num++;
   	}
   	return compute
   }
   var add = test()
   ```

2. 返回对象

   ```js
   function test(){
   	var num = 0;
   	var compute = {
   		add:function(){
   			num++
   		},
   		minus|:function(){
   			num--
   		}
   	}
   	return compute
   }
   var compute = test()
   compute.add;
   compute.minus;
   ```

3. 构造函数

   实例化对象时隐式创建this对象，再return this

   ```js
   function Compute(){
   	var num = 0;
   	this.add = function() {
   		num++
   	};
   	this.minus = funciton(){
   		num--
   	}
   }
   var compute = new Compute();
   compute.add();
   compute.minus;
   ```

   ## 链式调用、对象属性遍历、this、caller_callee

###   链式操作                         

return this

```js
var sched = {
	morning:function(){
		console.log('studying');
		return this;
	},
	afternoon:function(){
		console.log('reading')
		return this;
	},
	evening:function(){
		console.log('sleeping')
		return this;
	}
}
sched.morning().afternoon().evening()
```

### 属性名拼接

```js
obj['name']===obj.name
obj['No'+num] //可以拼接属性名
```

### 对象、数组属性遍历

```js
for(var key in obj){
	//car.key ->car['key'] ->undefined
	console.log(key, obj[key])
			  // 键名   键值
}
```

```js
for(var i in arr){
	//arr.i ->car['i'] ->undefined
	console.log(i, arr[i])
			  // 键名   键值
}
```

### hasOwnProperty

判断参数是否为对象自身的属性,排除原型链上的自定义属性

```js
function Car(){
	this.brand = 'Benz'
}
Car.prototype = {
	width: 5
}
Object.prototype.name = 'Object'
var car = new Car()

for(var k in car){
	if(car.hasOwnProperty(k)){
		console.log(car[k])
		//只输出实例对象自身的属性
	}
}
```

### in

判断对象中是否有某属性,不排除原型上的属性

```js
console.log('brand' in car) 
// 属性要为字符串 car['brand']
```

### instanceof

判断该实例化对象是否为该构造函数构造出的，包括原型链上原型的构造函数（不能隐式转换）

```js
console.log(a instanceof A)
console.log([] instanceof Object) // true
console.log({} instanceof Object)  //true
console.log([] instanceof Array)  //true
```

### 判断类型

```js
var a = [];
a.constructor //Array()
a instanceof Array // true
Object.prototype.toString().call(a) //[object Array]
```

```js
var str = Object.prototype.toString(),
    trueTip = '[object Array]'
if (str.call(a) === trueTip){
	console.log('是数组')
}else{
	console.log('不是数组')
}
```

### this 指向 

- **全局this指向window**

- **普通函数里的this指向window**

- **构造函数this指向实例化对象**

  ```js
   function Test(){
   	//var this = {
   	// __proto__:Test.prototype
   	//}
   	this.name = '123'
   }
   var test = new Test()
   //AO = {
   //  this:{
   //		name:'123'
   //		__proto__:Test.prototype
   //  }
   //}
   //GO = {
   //	 Test:funciton test(){...}
   //  test:{
   //		name:'123'
   //		__proto__:Test.prototype
   //  }
   //}
  ```

- **call和apply**

### callee和caller

### callee

实参列表的属性，arguments.callee返回正在被执行的函数

callee在哪个函数中就返回哪个函数

```js
function test (a,b,c){
	console.log(arguments.callee.length);//3
	console.log(test.length) //3 形参的个数
	console.log(argument.length)//2 实参的个数
}
test(1,2)
```

##### 使用场景：

在立即执行函数或匿名函数中需要调用函数时

```js
var sum = (function (n){
	if(n<=1){
		return 1;
	}
	return n + argumnents.callee(n-1);
})(10)
```

### caller

返回调用当前函数的函数引用

```js
function test1(){
	test2();
}
test1()
function test2(){
	console.log(test2.caller)
}
```

##  三目运算、对象克隆、浅拷贝、深拷贝

### 三目运算符

```js
var str = a > 0 ? '大于0' //return
	  		    : '小于0' //return
```

```js
var str = a > 0 ? (a > 3 ? '大于3'
                   		 :'小于等于3')
	  		    		 : '小于0'
```

## 对象克隆

B复制A，如果修改A的引用值，

B也发生改变，是浅拷贝；

B不发生改变，是深拷贝

### 浅拷贝

```js
function clone(origin,target){
    var tar = target || {}
    for(var key in origin){
      if(origin.hasOwnPorperty(key)){
            tar[key] = origin[key];
        }      
    }
    return tar
}
```

```js
Object.prototype.num = 1;
ar p1 = {
	name:'张三',
	age:20,
	sex:'male'
}
var p2 = clone(p1,p2)
p2.name = '李四';
p2.sex = 'female'
```

### 深拷贝

```js
//1.剔除原型上的属性
//2.判断是否为引用值
//3.判断是数组还是对象
function deepclone(origin,target){
	var target = target||{},
		toStr = Object.prototype.toString,
		arrType = '[object Array]';
	
	for (var key in origin){
		if(origin.hasOwnProperty(key)){
			if(typeof(origin[key])==='object' && origin[key]!==null){
				if(toStr.call(origin[key])===arrType){
					target[key] = []
				}else{
					target[key] = {}
				}
				deepclone(origin[key],target[key]);
			}else{
				target[key] = origin[key];
			}
		}
	}
    return target
}
```

```js
var p1 = {
	name:'张三',
	age:20,
	sex:'male',
	children:{
		first:{
			name:'leah',
			age:20
		},
		second:{
			name:'tom',
			age:18
		}
	},
	car:['Banz','Mazd']
}

var p2 = deepClone(p1)
```

### JSON实现深拷贝

```js
var str = JSON.stringify(p1);
var p2 = JSON.parse(str);
```



## 练习题

```js
function test(){
	console.log(foo);
	var foo = 2;
	console.log(foo);
	console.log(a)
}
test()

//undefined
//2
//报错
```

```js
var name = '222';
var a = {
	name:'111',
	say:function(){
		console.log(this.name)
	}
}
var fun = a.say;
fun();                  //222
a.say()                 //111
var b = {
	name:'333',
	say:function(fun){
		fun()
	}
}
b.say(a.say);           //222
b.say = a.say;
b.say()                 //333
```

```js
function test(){
	var marty = {
		name:'marty',
		printName:function(){
			console.log(this.name)
		}
	}
	var test1 = {
		name:'test1'
	}
	var test2 = {
		name:'test2'
	}
	var test3 = {
		name:'test3'
	}
}

test3.printName = marty.printName;
marty.printName.call(test1); //test1
marty.printName.apply(test2);//test2
marty.printName();//marty
test3.printName();//test3
```

```js
var bar = {
	a :'1'
}
function test(){
 bar.a = 'a'
 Object.ptotytype.b = 'b'
 return function inner(){
 	console.log(bar.a)
 	console.log(bar.b)
 }
}
test()()
```

```js
function Foo() {
      getName = function() {
                console.log(1);
      }
      return this;
}
Foo.getName = function() {
    console.log(2);
}
Foo.prototype.getName = function() {
    console.log(3);
}
var getName = function() {
     console.log(4);
}

function getName() {
     console.log(5);
}

//GO={
//   getName:undefined
//    ->function getName() {console.log(5)}
//    ->function() {console.log(4)}
//    ->function() {console.log(1)}
//}

        Foo.getName(); // 2
        getName(); // 4
        Foo().getName(); // 1
        getName()   // 1
        new Foo.getName(); // 2
        new Foo().getName(); // 3
        new new Foo().getName() // 3
```

## 数组基础、数组方法、数组排序

### 数组声明方式

```js
var arr = [] //数组字面量
var arr = new Array(参数);//通过系统内置Array构造函数声明数组
//参数表示数组的长度
var arr = Array()//不使用
```

所有的数组都继承于Array.prototype

**稀松数组**： var  arr = [,1,2,,,5,]  最后一位没有值会忽略最后一位

### 数组方法(修改原数组)

数组方法继承于Array构造函数的prototype

#### push/unshift

在数组的最后一位后增加/在数组的第一位前增加

**返回值是执行了方法以后的数组长度**

#### 自己实现push

```js
var arr = [1, 2, 3]
        Array.prototype.mypush = function() {
            for (let i = 0; i < arguments.length; i++) {
                this[this.length] = arguments[i];
            }
            return this.length
        }
        console.log(arr.mypush(4, 5, 6)); // 6
```

#### pop/shift

剪切数组的最后一位后/剪切数组的第一位，没有参数

**返回值是被剪切的数值**

#### reverse

倒序

#### splice

```js
arr.splice(开始项的下标，剪切长度。剪切的位置添加的数据)  
var arr = ['a','b','d'];
arr.splice(2,0,'c')
arr.splice(-1,0,'c')
//['a','b','c','d']
```

```js
function splice(arr,index){
	return index += index >= 0 ? 0 : arr.length;
}

console.log(splice([1,2,3,4,5],-2)) // 3
```



#### sort

默认按照ASCII码来排序，返回排序以后的数组

**自定义排序：**

1. 两个参数a,b
2. 返回值：
   - 正值，b排前
   - 负值，a排前
   - 0 保持不动

```js
//升序
sort(function(a,b){
	if(a > b){
		return 1
	}else{
		return -1
	}
})
//降序
sort(function(a,b){
	if(a < b){
		return 1
	}else{
		return -1
	}
})
```

```js
//升序
sort(function(a,b){
	return a - b;
})
//降序
sort(function(a,b){
	return b - a;
})
```

#### 随机排序

```js
arr.sort(function(a,b){
	var rand = Math.random();
	if(rand - 0.5 > 0){
		return 1;
	}else{
		return -1
	}
})
```

```js
sort(function(a,b){
	return Math.random() - 0.5
})
```

#### 以对象的属性值排序

```js
var children = [
	{
		name:'lucy',
		age:5
	},{
		name:'tom',
		age:12
	},{
		name:'leah',
		age:8
	},{
		name:'yoo',
		age:18
	}
]

children.sort(function(a,b){
	return a.age - b.age
})
```

#### 以数值的长度排序

```js
var arr = ['12','45612','8541','5']
arr.sort(function(a,b){
    return a.length - b.length;
})
```

## 数组方法、类数组

### 数组方法

#### cancat

拼接两数组，返回新数组

```js
var arr1 = [1,2,3],
	arr2 = [4,5,6];
var arr3 = arr1.concat(arr2)
```

#### toString()

数组转成字符串，逗号隔开

#### slice()

[start,end)从start开始，到end之前截取，返回新数组  

```js
var arr = ['a','b','c','d','e','f'];
var arr1 = arr.slice(-3, 5) //['d','e']
```

#### join()

将数组中的元素组成新新的字符串，传入参数是分隔符，没传默认为逗号

```js
var arr = ['a','b','c'];
var arr1 = arr.join('-') //'a-b-c'
```

#### split()

将字符串按照第一个参数的分隔符分隔，生成新的数组，第二个参数为截取的长度

```js
var arr1 = arr.join('-') //'a-b-c';
var arr2 = arr1.split('-',2) //['a','b']
```

### 类数组

类数组是类似于数组的对象，不能使用Array上的方法

```js
var obj = {
    '0':1,
    '1':2,
    '2':3,
    '3':4, 
    '4':5,
    'length':6,
    'slice':Array.prototype.slice
    //类数组转数组的方式
}
Object.prototype.push = Array.prototype.push;
//可以将Array上的方法给类数组本身，也可以给Object，这样就可以使用数组的方法了
```

#### 自己实现push

```js
Array.prototype.push = function(ele){
	this[this.length] = ele;
	this.length ++;
}
```

##### 例题：

```js
var obj = {
    '2':3,
    '3':4, 
    'length':2,
    'push':Array.prototype.push
}
obj.push(1);
obj.push(2);
console.log(obj)
//此时length为2，在此基础上长度为3的最大索引值为2
//obj[2] = 1
//obj[3] = 2
//{
//   '2':1,
//   '3':2, 
//   'length':4,
//   'push':Array.prototype.push
//}
```

## 自定义原型方法、去重、封装typeof

### 自定义unshift函数

使用splice方法

```js
Array.prototype.myUnshift = function(){
    var pos = 0;
    for(var i = 0; i < arguments.length; i++){
        this.splice(pos,0,arguments[i]);
        pos++;
    }
    return this.length;
}
```

使用concat方法

```js
Array.prototype.myUnshift = function(){
	var arr = Array.prototype.slice.call(arguments);
	var newArr = arr.concat(this);
    return newArr.length;
}
```

### 数组按照元素的字节数排序

```js
function getBytes(str){
	var bytes = str.length;
	for(var i = 0; i < bytes; i ++){
	 if(str.charCodeAt(i) >= 256 ){
	 	bytes++;
	 }
	}
	return bytes;
}
function sortArr(arr){
	return arr.sort((a,b) =>{
		return getBytes(a) - getBytes(b);
	})
}
```



### 封装typeof

```js
function myTypeof(val) {
            var type = typeof(val);
            var toStr = Object.prototype.toString();
            var res = {
                '[object Object]': object,
                '[object Array]': array,
                '[object String]': string,
                '[object Number]': number,
                '[object Boolean]': boolean
            }
            if (val === null) {
                return 'null'
            } else if (type === 'object') {
                var ret = toStr.call(val);
                return res[ret]
            } else {
                return type;
            }
        }
```

### 数组去重

```js
var arr = [0, 0, 1, 2, 2, 1, 4, 2, 4, 'a', 'b', 'a']

        Array.prototype.unique = function() {
            var obj = {};
            var newArr = []
            for (let i = 0; i < this.length; i++) {
                if (!obj.hasOwnProperty(this[i])) {
                    obj[this[i]] = this[i];
                    newArr.push(this[i])
                };

            }
            return newArr
        }
```

### 字符串去重

```js
var str = 'fnrnfrnfhkjddmdee';
        String.prototype.unique = function() {
            var obj = {},
                newStr = '';
            for (let i = 0; i < this.length; i++) {
                if (!obj.hasOwnProperty(this[i])) {
                    obj[this[i]] = this[i];
                    newStr += this[i]
                }
            }
            return newStr
        }
        console.log(str.unique());
```

### 获取字符串中第一位只有一个的字符

```js
var str = 'hruhfrauhfuhbfrufcuhgrhf';

        function test(str) {
            var obj = {};
            for (let i = 0; i < str.length; i++) {
                if (obj[str[i]]) {
                    obj[str[i]]++;
                } else {
                    obj[str[i]] = 1;
                }
            }
            for (var key in obj) {
                if (obj[key] == 1) {
                    return key;
                }
            }
        }

        console.log(test(str));
```

## 错误信息、try_catch、严格模式

### JS错误信息类型

1. SyntaxError 语法错误

   - 变量名不规范
     - var 1ab=1
   - 关键字不可赋值
     - function = 1
   - 基本语法错误
     - var a = 5:

2. ReferenceError 引用错误

   - 变量或函数未被声明
   - 给无法赋值的对象赋值的时候

3. RangeError 范围错误

   - 数组长度赋值为负数
   - 对象方法参数超出可行范围

4. TypeError 类型错误

   - 调用不存在的方法
   - 实例化原始值

5. URIError URI错误

   URL：uniform resource identifier 统一资源标识符

   URL：uniform resource location  统一资源定位符

   ​			http://www.baidu.com/news#today

   URN:  uniform resource name  统一资源名称

   ​			www.baidu.com/news#today ->ID

   ```js
   var myUrl = 'http://www.baidu.com/name=窦靖童';
   var newUrl = encodeURI(myUrl);
   var newNewUrl = decodeURI(newUrl);
   
   var str = decodeURI('%radcrc%')//报错
   ```

6. EvalError eval函数执行错误

### 自定义实例化错误

```js
var error = new Error('代码错了');
console.log(error)

var error = new TypeError('代码错了');
console.log(error)
```



### try/catch/finally/throw

```js
try{
	console.log('正常执行');
	console.log(a) //执行报错
	console.log(b) //不执行
	console.log('正常执行2')
}catch(e){
	console.log(e.name+':'+e.message)
}finally{
	console.log('正常执行3')
}
console.log('正常执行3')
```

json字符串

```JS
var jsonStr = "";
try{
	if(jsonStr == ""){
		throw 'JSON字符串为空'
	}
	console.log('我要执行啦');
	var json = JSON.parse(jsonStr);
	console.log(json)
}catch(e){
	console.log(e);
	var errorTip = {
		name:'数据传输失败',
		errorCode:'10010'
	}
	console.log(errorTip)
}
```

### ECMAscript发展史

- 97    1.0
- 98    2.0
- 99    3.0  JS通行标准
- 07    4.0草案   只有Mozilla支持  Branden eich
- 08    4.0中止   容易改善 3.1  Harmony
- 09    5.0发布，Harmony -> 1/2 JS.NEXT  1/2JS.NEXT.NEXT
- 11     5.1   ISO国际标准
- 12     ES6 = js.next
- 13     ES6草案发布
- 15     ES6正式发布，ECMAscript2015

### 严格模式

ES5 正常模式 严格模式

IE9及以上版本

```
'use strict'

function test (){
	'use strict'
}

var test = (function(){
	'use strict'
})()
```

严格模式下不能使用with

```js
var a = 1;
var obj = {
	a:2
}
function test(){
	var a = 3;
	var b = 4;
	with(window){
		console.log(a);
		console.log(b)
	}
}
test()
```

严格模式下不能使用callee和caller

```js
function test(){
	console.log(arguments.callee)
}
test(1,2,3)
```

```
function test1(){
	test2()
}
function test2(){
	console.log(test2.caller)
}
```

严格模式下未声明变量赋值会报错包括函数内

```js
var a = b = 1

function test(){
    var a = b =1
}
test()
```

严格模式下函数未定义this指向默认为undefined

```js
function test(){
	console.log(this)
}
test() 
//test.call({})
//test.call(1) //会将原始值包装成类
//var test1 = new test()
```

严格模式下函数的参数不能重复

```js
function test(a,a){
	console.log(a)
}
test(1,2)

var obj = {
    a:1,
    a:2
}
console.log(obj.a) //不报错但不允许属性名相同
```

严格模式下不能在eval外使用其变量

```js
eval('var a = 1;console.log(a)')
console.log(a)
```

## 变量生命周期、垃圾回放原理

### 变量生命周期

全局变量的生命周期是直到浏览器关闭或程序关闭

局部变量在函数执行结束之后被回收，排除生成闭包的AO中的变量

### 垃圾回收机制

1. 找出不再使用的变量
2. 释放其占用内存
3. 固定的时间间隔运行

#### 标记清除：mark and sweep

```js
function test(){
	var a = 0//进入环境
}
test()//离开环境
var b = 0;
bar c = 1
function e(){}
```

垃圾回收执行器周期性回收，首先排除全局变量和闭包所带出的AO中的变量，剩下的变量将被视为要被删除的变量，垃圾回收执行器工作时将会销毁带有离开环境标记的变量，并回收其所有的内存空间。

#### 引用计数reference counting

记录每个引用值被记录的次数，次数为1的值会被回收

可能会导致内存泄漏

```js
function test(){
	var a = new Object();// a = 1
	var b = new Object();// b = 1
	
	var c = a; //a++  =2
	var c = b; //a--  =1
	
	//循环引用
	a.prop = b //b=2
	b.prop = a //a=2
	
    //解除引用
	a = null;
	b = null;
}
```

## 数组去重

### for循环

```js
var arr = [4,5,4,8,1,5,5,2,3,9,4,5];

function unique(arr){
	var temp = [],
	isRepeat;
		
	for(var i = 0; i < arr.length; i++){
		isRepeat = false;
		for(var j = 0; j<temp.length;j++){
			if(temp[j] == arr[i]){
				isRepeat = true;
				break;
			}		
		}
		if(!isRepeat){
			temp.push(arr[i])
		}
	}
		return temp
}
```

```js
var arr = [4,5,4,8,1,5,5,2,3,9,4,5];
function unique(arr){
    var isRepeat,
        temp = [];
    for(var i = 0; i <arr.length; i++){
        isRepeat = false;
        for(var j = i+1;j < arr.length;j++){
            if(arr[i]==arr[j]){
                isRepeat = true;
                break;
            }
        }
        if(!isRepeat){
            temp.push(arr[i]);
        }
    }
    return temp;
}
```

### filter

```js
function unique(arr){
    return arr.filter((item,index)=>{
        return arr.indexOf(item) === index
    })
}
```

### foreach

```js
function unique(arr){
    var temp = [];
    arr.forEach((item)=>{
        if(temp.indexOf(item) === -1){
            temp.push(item);
        }
    })
    return temp;
}
```

### sort

```js
function unique(arr){
	var temp = [];
    arr.sort();
    for(var i = 0; i <arr.length;i ++){
        if(arr[i] != arr[i+1]){
            temp.push(arr[i]);
        }
    }
    return temp;
}
```

```js
function unique(arr){
	var temp = [];
    arr.sort();
    for(var i = 0; i <arr.length;i ++){
        if(arr[i] != temp[temp.length-1]){
            temp.push(arr[i]);
        }
    }
    return temp;
}
```

### es6  includes

 includes与indexOf的区别

array.includes 返回 true/false 

array.indexOf 返回index/-1  NaN无效

```js
function unique(arr){
	var temp = [];
    arr.forEach(item => {
        if(!temp.includes(item)){
            temp.push(item)
        }
    })
    return temp;
}
```

### reduce

```js
function unique(arr){
    var temp = [];
	return arr.sort().reduce((prev,item)=>{
       if(temp.length === 0 || prev[temp.length - 1] !== item){
           temp.push(item);
       }
        return prev;
    },[]);
    
}
```

### object

```js
function unique(arr){
    var temp = [],
        obj = {};
    for(var i = 0;i < arr.length;i++){
        if(!obj[arr[i]]){
            obj[arr[i]] = 1;
            temp.push(arr[i]);
        }
    }
    return temp;
}
```

### Map

```js
function unique(arr){
    var temp = [],
        map = new Map();
    for(var i = 0;i < arr.length;i++){
        if(!map.get(arr[i])){
            map.set(arr[i],1);
            temp.push(arr[i]);
        }
    }
    return temp;
}
```

### set

```js
function unique(arr){
	return Array.from(new Set(arr)); //将类数组变为数组
}
```

## 数组扁平化、去重与排序

要求：编写一个程序将数组扁平化并将数组去重，最终得到一个升序并不重复的一组数组

### 数组扁平化

扁平化 -> 多维数组降维一维数组

```js
var arr = [[1,2],[3,6],[5,[2,6]],[3,5,2]];

function flatten(arr){
    var _arr = arr || [],
        fArr = [],
        len = _arr.length,
        item;
    for(var i = 0; i < len; i++){
        item = _arr[i];
        if(_isArr(item)){
            fArr = fArr.concat(flatten(item));
        }else{
            fArr.push(item);
        }
    }
    
    return fArr;
    
    function _isArr(item){
        return {}.toString.call(item) === '[object Array]'
    }
}
```

### foreach

```js
Array.prototype.flatten = function(){
	var _arr = this,
        toStr = {}.toString,
        _fArr = [];
    if(toStr.call(_arr)!=='[object Array]'){
        throw new Errow('只有数组才能调用flatten方法')
    }else{
        _arr.forEach(item => {
            toStr.call(item)==='[object array]'?
                _fArr = _fArr.concat(item.flatten():
                _fArr.push(item);
            }
        })
    }
   	return fArr;
}
```

### reduce

```js
Array.prototype.flatten = function(){
	var _arr = this,
        toStr = {}.toString;
    if(toStr.call(_arr)!=='[object Array]'){
        throw new Errow('只有数组才能调用flatten方法')
    }else{
        return _arr.reduce((prev,item)=>{
           return prev.concat(
               toStr.call(item) === 'object Array'?
               item.flatten() :  
               item
        },[]))
    }
}
```

```js
var flatten = (arr)=>{
	return arr.reduce((prev,item)=>{
        return prev.concat(
            {}.toString.call(item) === '[object Array]'?
            flatten(item):
        	item
        )
    },[]); 
}
-------------------------------------------
var flatten = (arr)=>{
	arr.reduce((prev,item)=>
         prev.concat(
            {}.toString.call(item) === '[object Array]'?
            flatten(item):
        	item
        )
    ,[]); 
}
```

### es6  flat扁平化  set去重   

```js
var arr = [[1,2],[3,6],[5,[2,6]],[3,5,2]];

Array.from(new Set(arr.flat(Infinity))).sort((a,b)=>a-b)
```



