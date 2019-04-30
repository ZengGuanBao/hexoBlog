---
title: JavaScript学习笔记
tags: [JavaScript]
category: 技术
---
工具：Visual Studio Code/MarkdownPad
技术：JavaScript
##JavaScript类型
###基本类型有六种： null，undefined，boolean，number，string，symbol
###typeof 对于基本类型，除了 null 都可以显示正确的类型
	typeof 1 // 'number'
	typeof '1' // 'string'
	typeof undefined // 'undefined'
	typeof true // 'boolean'
	typeof Symbol() // 'symbol'
	typeof b // b 没有声明，但是还会显示 undefined
###想获得一个变量的正确类型，可以通过 Object.prototype.toString.call(xx)。这样我们就可以获得类似 [object Type] 的字符串。
    console.log(Object.prototype.toString.call("jerry"));//[object String]
    console.log(Object.prototype.toString.call(12));//[object Number]
    console.log(Object.prototype.toString.call(true));//[object Boolean]
    console.log(Object.prototype.toString.call(undefined));//[object Undefined]
    console.log(Object.prototype.toString.call(null));//[object Null]
    console.log(Object.prototype.toString.call({name: "jerry"}));//[object Object]
    console.log(Object.prototype.toString.call(function(){}));//[object Function]
    console.log(Object.prototype.toString.call([]));//[object Array]
    console.log(Object.prototype.toString.call(new Date));//[object Date]
    console.log(Object.prototype.toString.call(/\d/));//[object RegExp]
    function Person(){};
    console.log(Object.prototype.toString.call(new Person));//[object Object]
###js中的instanceof运算符

instanceof 运算符用来检测 constructor.prototype 是否存在于参数 object 的原型链上。

语法：obj instanceof Object;//true 实例obj在不在Object构造函数中

1. **instanceof的普通的用法，obj instanceof Object 检测Object.prototype是否存在于参数obj的原型链上。**
Person的原型在p的原型链中

        function Person(){};
	    var p =new Person();
	    console.log(p instanceof Person);//true

2. **继承中判断实例是否属于它的父类**
Student和Person都在s的原型链中

	    function Person(){};
	    function Student(){};
	    var p =new Person();
	    Student.prototype=p;//继承原型
	    var s=new Student();
	    console.log(s instanceof Student);//true
	    console.log(s instanceof Person);//true
3. **复杂用法**，这里的案例要有熟练的原型链的认识才能理解

	    function Person() {}
	    console.log(Object instanceof Object); //true
	    //第一个Object的原型链：Object=>
	    //Object.__proto__ => Function.prototype=>Function.prototype.__proto__=>Object.prototype
	    //第二个Object的原型：Object=> Object.prototype
	    
	    console.log(Function instanceof Function); //true
	    //第一个Function的原型链：Function=>Function.__proto__ => Function.prototype
	    //第二个Function的原型：Function=>Function.prototype
	    
	    console.log(Function instanceof Object);   //true
	    //Function=>
	    //Function.__proto__=>Function.prototype=>Function.prototype.__proto__=>Object.prototype
	    //Object => Object.prototype
	    
	    console.log(Person instanceof Function);  //true
	    //Person=>Person.__proto__=>Function.prototype
	    //Function=>Function.prototype
	    
	    console.log(String instanceof String);   //false
	    //第一个String的原型链：String=>
	    //String.__proto__=>Function.prototype=>Function.prototype.__proto__=>Object.prototype
	    //第二个String的原型链：String=>String.prototype
	    
	    console.log(Boolean instanceof Boolean); //false
	    //第一个Boolean的原型链：Boolean=>
	    //Boolean.__proto__=>Function.prototype=>Function.prototype.__proto__=>Object.prototype
	    //第二个Boolean的原型链：Boolean=>Boolean.prototype
	    
	    console.log(Person instanceof Person); //false
	    //第一个Person的原型链：Person=>
	    //Person.__proto__=>Function.prototype=>Function.prototype.__proto__=>Object.prototype
	    //第二个Person的原型链：Person=>Person.prototype


4. **总结**
对应上述规范做个函数模拟A instanceof B：

	    function _instanceof(A, B) {
		    var O = B.prototype;// 取B的显示原型
		    A = A.__proto__;// 取A的隐式原型
		    while (true) {
			    //Object.prototype.__proto__ === null
			    if (A === null)
			    return false;
			    if (O === A)// 这里重点：当 O 严格等于 A 时，返回 true
			    return true;
			    A = A.__proto__;
		    }
	    }
###对象中的原型方法
首先会调用 valueOf 然后调用 toString，Symbol.toPrimitive （该方法在转基本类型时调用优先级最高），方法你是可以重写的

    let a = {
      valueOf() {
    return 0;
      },
      toString() {
    return '1';
      },
      [Symbol.toPrimitive]() {
    return 2;
      }
    }
    1 + a // => 3
    '1' + a // => '12'
