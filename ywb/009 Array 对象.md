#### 2 Array 对象   

创建 Array 对象的方式：    
```JavaScript
new Array();
new Array(size);
new Array(element0, element1, ..., elementn);
```
##### 2.1 参数  
* 参数 size 是期望的数组元素个数。返回的数组，length 字段将被设为 size 的值。  

参数 element ..., elementn 是参数列表。当使用这些参数来调用构造函数 Array() 时，新创建的数组的元素就会被初始化为这些值。它的 length 字段也会被设置为参数的个数。  
##### 2.2 返回值  
返回新创建并被初始化了的数组。  

如果调用构造函数 Array() 时没有使用参数，那么返回的数组为空，length 字段为 0。  

当调用构造函数时只传递给它一个数字参数，该构造函数将返回具有指定个数、元素为 undefined 的数组。  

当其他参数调用 Array() 时，该构造函数将用参数指定的值初始化数组。  

当把构造函数作为函数调用，不使用 new 运算符时，它的行为与使用 new 运算符调用它时的行为完全一样。  
##### 2.3 方法  
* unshift() ：在数组头部插入元素  
* shift() ：移除并返回数组的第一个元素  
* push() ：在数组尾部插入元素  
* pop() ：移除并返回数组的最后一个元素  
* concat() ：把元素衔接到数组中。不会修改原先的array,返回新的数组  
```JavaScript
var demoArray = ['a', 'b', 'c'];
var demoArray2 = demoArray.concat('e');
console.log(demoArray); // => demoArray:['a','b','c']  原数组不发生变更
console.log(demoArray2); // => ['a','b','c','e']
```
* every() ：依次遍历元素，判断每个元素是否都为true  
```JavaScript
var demoArray = [1, 2, 3];
var rs = demoArray.every(function (value, index, self) {
     return value > 0;
});
console.log(rs); // => true
```
* pop() ：移除并返回数组的最后一个元素  
```JavaScript
var demoArray = ['a', 'b', 'c'];
demoArray.pop(); // => c
demoArray.pop(); // => b
demoArray.pop(); // => a
demoArray.pop(); // => undefined
```
##### 2.4 复制  
* 浅度复制
```JavaScript
var demoArrayA = ['a', 'b', 'c', 'd', 'e'];
var demoArrayB = demoArrayA; // 把数组A 赋值给数组B
demoArrayB[0] = 1; // 对数组B 的元素进行修改
console.log(demoArrayA); // => [1, 'b', 'c', 'd', 'e']：数组A 的元素也发生了变更
```
* 深度复制  
```JavaScript
var demoArrayA = ['a', 'b', 'c', 'd', 'e'];
var demoArrayB = demoArrayA.concat(); // 使用concat()方法，返回新的数组
demoArrayB[0] = 1; // 对数组B 的元素进行修改
console.log(demoArrayA); // => ['a', 'b', 'c', 'd', 'e']：数组A 的元素没变更
console.log(demoArrayB); // => [  1, 'b', 'c', 'd', 'e']：数组B 的元素发生了变更
```

