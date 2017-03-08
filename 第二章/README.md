## 对象的深度复制

> * 1. 利用Object.prototype.toString.call(obj) == '[object Array]',判断是否是数组。
> * 2. 利用arguments.callee(arg)实现递归。

```js
function deepClone(obj){
	var result;
	//初始化对象，确定是否是引用类型
	if(typeof obj === 'object'){
		if(Object.prototype.toString.call(obj) == '[object Array]'){
			result = [];
		}else{
			result = {};
		}
	}
	//遍历属性，如果是引用类型，则递归深度复制，否则直接赋值；
	for( var property in obj){
		var arg = obj[property];
		result[property] = typeof arg === 'object'? arguments.callee(arg) : arg;
	}
	return result;
}
var oPerson={
    oName:"rookiebob",
    oAge:"18",
    oAddress:{
        province:"beijing"
    },    
    ofavorite:[
        "swimming",
        {reading:"history book"}
    ],
    skill:function(){
        console.log("bob is coding");
    }
};
var oNew=deepClone(oPerson);
console.log(oPerson.oAddress.province);//beijing
oNew.oAddress.province="shanghai";
console.log(oPerson.oAddress.province);//beijing