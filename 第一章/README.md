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