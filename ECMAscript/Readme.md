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

   