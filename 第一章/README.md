## 定义一个可以为函数添加多个方法的addMethod方法

```js
Function.prototype.addMethod = function (obj) {
	
	for (key in obj){
		this.prototype[key] = obj[key];
	}
	return this;
}
var Methods = function () {};
Methods.addMethod({"aa" : function() {}, "bb" : function () {alert(11)}});

var a = new Methods();
console.log(a);
```

## 试着定义一个既可以为函数原型也可以为自身添加函数的addMethods方法

```js
/*为函数或者其原型添加方法
 *@obj  JSON格式数据，{key: function(){}}
 *@option  Bool  true:为函数添加，false:为原型添加
 */
Function.prototype.addMethod = function (obj, option) {
	if(option){
		for(key in obj){
			if(obj.hasOwnProperty(key)){
				this[key] = obj[key];
			}
		}
	}else{
		for (key in obj){
			if(obj.hasOwnProperty(key)){
				this.prototype[key] = obj[key];
			}
		}
	}
	return this;
}
var myMethods = function () {};

myMethods.addMethod({"aa" : function() {}, "bb" : function () {alert(11)}}, true);

myMethods.bb();//alert(11)

var a = new myMethods();
myMethods.addMethod({"aa" : function() {}, "bb" : function () {alert(11)}}, false);
console.log(a);



```