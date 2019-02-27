### javacript类与封装

#### 一：javacript类

类与面向对象编程密不可分，面向对象编程就是将需求抽象成一个对象（类），然后针对这个对象分析其特征（属性）与动作（方法），它的一个特点就是封装，即把需要的功能放在一个对象里。

**如何在javaScript中创建一个类？**

##### 1.ES5

首先声明一个函数保存在一个变量里，然后在这个函数（这个函数称之为类）的内部通过对this变量添加属性名或者方法来实现对类添加属性或者方法。

```js
var Book=function(id,bookname,price){
    this.id=id;
    this.bookname=bookname;
    this.price=price;
}
```

以上创建了一个类`Book`(类名首字母大写),这种创建类的方式也叫构造函数模式.也可以在类的原型上添加属性和方法。

在类的原型上添加属性和方法(两种方式)

```js
//方式一
Book.prototype.display=function(){};
//方式二
Book.prototype={
    display:function(){};
}
```

以上将需要的方法和属性都封装在Book类里面了。当我们调用此方法时，需要使用New关键字以实例化新的对象

```js
var newBook=New Book(10, "JavaScript", 50);
```

通过new关键字实例化对象其实经历了一个简要的内部步骤：

创建新对象->将构造函数Book的作用域赋值给它，因此this就指向Book，最后执行各种想要的方法。

分析如下代码：

```js
var Book=function (id,name,price){
		this.id=id;
		this.name=name;
		this.price=price;
	}
  Book(10,"javascript",30);
  console.log(window.id); //10
```

从上述`window.id`结果来看，当我们调用构造函数时，没有将其赋值给新对象，故this指向的作用域就是全局作用域，我们就可以通过window对象调用Book构造函数里面的方法了。

##### 2.ES6

ES6中引入了**class**的概念，通过**class**关键字，极大地方方便了类的创建与使用，将上述原型中添加属性的代码用**class**改写如下：

```js
class Book{
    constructor(id,bookname,price){
       this.id=id;
       this.bookname=bookname;
       this.price=price;
    }
    display(){
        //...
    }
}
//等价于
var Book=function(id,bookname,price){
    this.id=id;
    this.bookname=bookname;
    this.price=price;
}
Book.prototype={
    display:function(){
        //...
    }
}
```

`class`省略了`function`的书写。

**点语法在函数内部添加属性与通过prototype创建属性的区别**

在函数内部通过点语法添加属性，当使用new操作符创建新的Book实例时，相应的this指向这个新实例，所以id与bookname等这些内部方法也会被创建，也就是说每定义一个函数，就实例化了一个对象，每个方法在每个实例上创建了一遍，通过prototype每次创建一个新对象时这些属性和方法不会被重新创建。

#### 二：封装

函数内部作用域在外部环境是不能访问内部作用域的私有方法和私有属性，而通过this创建的方法或属性在外部环境却能访问到，故this定义的这些方法或属性称为公有属性和公有方法，统称为特权方法。

```js
var Book=function (){
    var num=1; //私有属性
    function checkId(){ //私有方法
        //...
     }
    this.getName=function(){ //特权方法
        //...
    }
    this.id=id; //对象公有属性
    this.setName(name); 
    this.setPrice(price);//构造器
}
```

在通过new关键字实例化对象时，通过this定义的方法能被访问到，但私有属性却不能访问，这是因为实例化对象将作用域移到了外部实例对象，通过外部不能访问到内部的私有属性，而this定义的方法会将此方法的作用域指向实例化的对象。

```js
Book.isChinese=true;
Book.resetTime=function(){
    console.log('new time');
}
Book.prototype=function(){
    jsJSBook:false;
    display:function(){
        //...
    }
}
```

#### JS 的几种封装方法

##### 1.对象原型封装

基本思想：在原函数中建立getter和setter方法，之后在原函数的原型进行其他操作。

好处：只能通过get和set访问函数中的数据，实现了真正的封装，实现了属性的私有化。

劣处：这样做所有的方法都在对象中，会增加内存的开销

```js
function Person(name,age,no){ 
   this._name=name; 
   this._age=age; this._no=no; 
   this.checkNo=function(no){
       if(!no.constructor == "string"|| no.length!=4) 
         throw new Error("学号必须为4位"); 
   };
    //var _no,_age,_name; 
   this.setNo=function(no){ 
      this.checkNo(no); this._no=no;
    }; 
   this.getNo=function(){ 
      return this._no;
   }; 
   this.setName=function(name){ 
       this._name=name;
   };
   this.getName=function(){
        return this._name;
   }; 
   this.setAge=function(age){ 
       this._age=age;
   };
   this.getAge=function(){
       return this._age; 
   }; 
   this.setNo(no);
   this.setName(name);
   this.setAge(age);
   Person.prototype={
       toString:function(){
           return "no = " + this.getNo() + " , name = " + this.getName() + " , age = " + this.getAge();
       }
   };
  var per=new Person("lili",23,"0004");
  console.log(per.toString());
  per.setNo("0001");
  console.log(per.toString());
  per.setAge(25);
  console.log(per.toString());
```

##### 2.闭包封装

基本思想：构建闭包函数，在函数内部返回匿名函数，在匿名函数内部构建方法，在每次进行实例化调用的时候，其实都是每次都是调用返回函数的子函数，同时能保持对对象中的属性的共享
  好处：可以做到实例对象向对象属性的共享并且保持私有

  坏处：所有的get和set都存储在对象中，不能存储在prototype中，会增加开销

```js
/*
    * 2、闭包的封装方式，在这个封装方法中，所有的实例成员都共享属性和方法
    * 使得所有得方法和属性都私有且对象间共享
    * */
    var Person=(function(){
        /*共享函数*/
        let checkNo=function(no){
            if(!no.constructor=="string"||no.length!=4){
                throw new Error("必须为4位数");
            };
        };
        let times=0;//共享数据
        return function(no,name,age){
            console.log(times++);
            this.setNo=function(no){
                checkNo(no);
                this._no=no;
            };
            this.getNo=function(){
                return this._no;
            };
            this.setName=function(name){
                this._name=name;
            };
            this.getName=function(){
                return this._name;
            };
            this.setAge=function(age){
                this._age=age;
            };
            this.getAge=function(age){
                return this._age;
            };
            this.setNo(no);
            this.setAge(age);
            this.setName(name);
 
        }
    })();
    Person.prototype={
        constructor:Person,
        toString:function(){
            return "no = " + this._no + " , name = " + this._name + " , age = " + this._age;
        }
    }
 
    let per=new Person("0001",15,"simu");//输出之后times会逐渐增加，变为1、2、3
    let per1=new Person("0002",15,"simu1");
    let per2=new Person("0003",15,"simu2");
    console.log( per.toString());
    console.log( per1.toString());
    console.log( per2.toString());
```

