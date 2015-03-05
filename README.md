# DataBinder
imitate the two-way data-binding of Angular by jQuery

总结几种方式来模拟双向绑定

## Object.defineProperty

> `Object.defineProperty`可以自定义属性的getter和setter
> 当给对象的属相赋值或者取值时，可以调用setter或getter
> 不过此方法在IE8下有兼容性问题，IE8下可以用VBScript来实现

如下：

~~~
// 通过Object.defineProperty可以自定义属性的getter和setter
Object.defineProperty(person, 'house', {
	get: function() {
		console.log('you get me.');
		return str + ' get ';
	},
	set: function(newValue) {
		str = newValue + ' set ';
		console.log('you set me.')
	}
});

person.house = 'yes'; 
console.log(person.house); // result:you set me.you get me.yes set  get
~~~

## ES6的Proxy

> ES6的Proxy也有类似功能：监听对象身上发生了什么事
> 并做相应处理
> 不过现在浏览器基本没有实现这个功能，所以暂时无法用
> 真心觉得ES6的Proxy和Promises很棒 
> 希望主流浏览器能早日都支持 >_<

如：

~~~
// 被监听的对象
var coder = {
	name: 'Angelia',
	age: 18
};

var interceptor = {
	set: function(receiver, property, value) {
		console.log(proper, ' is changed to ', value);
		receiver[property] = value;
	}
};

coder = Proxy(coder, interceptor); // 由于浏览器基本没实现,所以这里会报错
coder.age = 24;
~~~


## 观察者模式

> 有点类似发布订阅模式(Publish/Subscribe)，
> 让多个观察者对象同时监听某一个主题对象，
> 这个主题对象的状态发生变化时就会通知所有的观察者对象，
> 使得它们能够自动更新自己
> 用js和jq分别在网上扒了个例子改了改

