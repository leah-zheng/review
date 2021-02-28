## forEach遍历

forEach是在Array.prototype上的方法，该方法的调用者必须为数组

```js
data.forEach(参数1[每次遍历执行的fn],参数2[fn的this指向])
```

```js
data.forEach(function(elem,index,array){
	oLi[index].innerHTML = elem.course;
},{name:'test'})
//当第二个参数为原始值时，会强制进行包装类，因为this指向对象，而null和undefined不能包装类，所以this还是指向Window

//升级版
data.forEach(function(elem,index,array){
	this[index].innerHTML = elem.course;
},oLi)
```

### 重写forEach

```js
 Array.prototype.myForEach = function(fn){
 	var arr = this,
 		len = arr.len,
 		arg2 = arguments[1]||window;
 	for(var i = 0; i < len; i++){
 		fn.apply(arg2,[arr[i],i,arr]);
 	}
 }
```

## filter过滤

是在Array.prototype上的方法，该方法的调用者必须为数组，**返回一个新的数组**

```js
var newArr = data.filter(参数1[每次遍历执行的fn,添加return为true的元素到新数组中],参数2[fn的this指向])
```

```js
var newArr = data.filter(function(elem,index,array){
	return elem.is_free === '1'
},{name:'test'})
```

### 重写filter

```js
Array.prototype.myFilter = function(fn) {
    var arr = this,
        len = arr.len,
        arg2 = arguments[1] || window,
        newArr = [],
        item;

    for (var i = 0; i < len; i++) {
        item = deepclone(arr[i])
        fn.apply(arg2, [arr[i], i, arr]) ? newArr.push(item) : "";
    }

    return newArr
}
```

## map映射

是在Array.prototype上的方法，该方法的调用者必须为数组，**返回一个新的数组**

```js
var newArr = data.map(参数1[每次遍历执行的fn,添加return指定值到新数组],参数2[fn的this指向])
```

```js
var newArr = data.map(function(elem,index,array){
	elem.course = this.name +elem.course;
	return elem;
},{name:'test'})
```

### 重写map

```js
Array.prototype.myMap = function(fn){
	var arr = this,
		len = arr.length,
		arg2 = arguments[1] || window,
		newArr = [],
		item;
	for(var i = 0; i < len; i++){
		item = tools.deepclone(arr[i]);
		newArr.push(fn.apply(arg2,[arr[i],i,arr]););
	}
	return newArr;
}
```

## every

如果有一个不满足条件就停止遍历，条件是return后面的表达式，返回最后一次遍历return中的bool值

```js
var res = data.every(function(elem,index,item){
	return elem.is_free == '0';
})

//false说明data中有免费课；若为true说明data中都是收费课
```

#### 重写every

```
function myEvery(fn){
	var arr = this,
		len = arr.length,
		arg2 = arguments[1] || window,
		res = true;
	for(var i = 0; i < len; i++){
		if(!fn.apply(arg2,[arr[i],i,arr])){
			res = false;
			break;
		}
	}
	return res;
}
```



## some

有一个满足条件的值就停止遍历，条件是return后的表达式，返回最后一次遍历return中的bool值

```js
var res = data.some(function(elem,index,arr){
	return elem.is_free == '0'
})

//若false说明data中没有收费课，若true说明至少有一个收费课
```

#### 重写some

```
function mySome(fn){
	var arr = this,
		len = arr.length,
		arg2 = arguments[1] || window,
		res = false;
	for(var i = 0; i < len; i++){
		if(fn.apply(arg2,[arr[i],i,arr])){
			res = true;
			break;
		}
	}
	return res;
}
```

## reduce归纳函数

  prev与initialValue是映射关系，首次遍历的时prev的值为initialValue，之后需要每次return prev，否则会为undefined

```js
var initialValue = [];
var newArr = data.reduce(function(prev,elem,index,arr){
	if(elem.is_free === '1') {
		prev.push(elem)
	}
	return prev;
},initialValue)
```

### reduce重写

```js
function myReduce(fn.initialValue){
	var arr = this,
		len = arr.length,
		arg2 = arguments[2] || window;
	for(var i = 0; i < len; i++){
		initialValue = fn.apply(arg2,[initialValue,arr[i],i,arr]);
		return initialValue
	}
}
```

### reduceRight逆序归纳

```js
function myReduceRight(fn.initialValue){
	var arr = this,
		len = arr.length,
		arg2 = arguments[2] || window;
	for(var i = len - 1; i >= 0; i--){
		initialValue = fn.apply(arg2,[initialValue,arr[i],i,arr]);
		return initialValue
	}
}
```

