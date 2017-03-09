## 用工厂方法模式为页面创建不同的按钮
> * 第一点注意利用安全模式，防止调用工厂是没有用new关键字
> * 第二点，利用工厂方法模式，将按钮的创建以及样式的创建放入原型当中，从而实现按钮的插入可拓展化

```js
var Factory = function (type, content) {
	if(this instanceof Factory){
		var s = new this[type](content); 
		return s;
	}else{
		return new Factory(type, content);
	}
}

Factory.prototype = {
	Primary : function (content) {
		this.content = content;
		(function(content){
			var button = document.createElement('button');
			button.innerHTML = content;
			button.style.border = '1px solid blue';
			document.getElementById('container').appendChild(button);
		})(content);
	},
	Info : function (content) {
		this.content = content;
		(function(content){
			var button = document.createElement('button');
			button.innerHTML = content;
			button.style.border = '1px solid green';
			document.getElementById('container').appendChild(button);
		})(content);
	},
	Danger : function (content) {
		this.content = content;
		(function(content){
			var button = document.createElement('button');
			button.innerHTML = content;
			button.style.border = '1px solid red';
			document.getElementById('container').appendChild(button);
		})(content);
	}
}

var data = [
	{type : 'Primary', content : '按钮'},
	{type : 'Info', content : '消息'},
	{type : 'Danger', content : '危险'}
]

for (var i = 0; i < data.length; i++) {
	Factory(data[i].type,data[i].content);
}
```