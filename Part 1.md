# JavaScript设计模式

## 面向对象的JavaScript
1. 多态的最根本作用就是通过把过程化的条件分支语句转化为对象的多态性，从而消除这些分支语句。
2. 原型模式：
一种用于创建对象的模式。
	1. 创建对象的两种方法：
				* 指定类型，通过类来创建对象
				* 找到一个对象，创建一个一模一样的对象
	2. 实现关键：语言本身是否提供了clone方法。在ECMAScript5中可用Object.create()来复制
	3. 真正目的在于提供了一种便捷的方式去创建某个类型的对象，克隆只是创建这个对象的过程和手段。
	4. 原型编程范性的规则：
				* A对象是从B对象克隆的，B对象就是A对象的原型
				* 克隆会形成一条原型链
				* 原型继承的本质就是基于原型链的委托机制 
	5. 基本规则
					* 所有的数据都是对象
					* 要得到一个对象，不是通过实例化类，而是找到一个对象作为原型克隆
					* 对象会记住它的原型
					* 如果对象无法响应某个请求，会把这个请求委托给自己的原型
	6. JavaScript中的原型继承
				* JavaScript中大多数数据都是对象。都有根对象：Object.prototype（空对象）
				* 用new运算符来创建对象的过程，实际上也只是先克隆Object.prototype对象，下进行一次其他额外操作的过程。
				* 对象的构造器有原型。_proto_属性默认指出他的构造器的原型对象。对象利用这个属性记住它的构造器的原型。
				* JavaScript中原型指向可以改变，变量搜索沿原型链直至Object.prototype，若都没有，则返回undefined。

## this、call和apply     
* this的指向：
this总是指向一个对象。具体指向哪个对象在运行时基于函数执行环境动态绑定的，而不是函数被声明时的环境
this指向的分类
				1. 作为对象的方法调用时：
           this指向该对象
				2. 作为普通函数调用时：
           不作为对象的属性被调用时，this指向全局的window对象。strict下回调函数的this指向undefined 
				3. 构造器调用时：
            用new调用其后，this指向返回的这个对象。如果显式返回一个对象，那么会返回这个对象，而不是this。如果不是对象，那么使用new后还是this
				4. Function.prototype.call或Function.prototype.apply调用
           动态的改变传入函数的this
				5. 不常用的with和eval时
          前四种具体在实际应用中常用到
* call和apply 
		* 两者的作用一样，只是传入参数的形式不同。

apply接受两个参数：
				1. 指定了函数体内this对象的指向
				2. 带下标的集合，可以为数组或类数组，把集合中的元素作为参数传递给被调用的函数（集合内就是参数，无参数则为空）
        
call接受的参数数量不确定
				1.指定函数体内this对象的指向
				2. 后续为函数所需要的参数
          
			* apply的效率更高。JavaScript不关心参数的个数，在内部就是用数组表示的。
			* 如果第一个参数传入null，那么this指向默认的宿主对象，浏览器中则是window。strict下仍为null
			* call与apply的用途
							1. 改变this的指向。
            典型例子：
```javascript
//一般情况
document.getElementById('div1').onclick = function(){
		alert(this.id);                  //输出div1  
};
//this混乱
document.getElementById('div1').onclick = function(){
		alert(this.id);                 //div1
		var func = function(){
			alert(this.id);        //undefined(普通调用指向Window)
		}
		func();
};
//利用call修正this
document.getElementById('div1').onclick = function(){
		var func = function(){
			alert(this.id);            //div1
		}
		func.call(this);
		//这里的this指向get的Document,给到function内可修整内部的this
}	  
```
								2. Function.prototype.bind
		这个功能用来指定函数内部的this指向。

```javascript
//Function.prototype.bind的模拟实现
 
```
 

