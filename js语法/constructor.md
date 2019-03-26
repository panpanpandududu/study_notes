### 构造函数

#### 定义：

**构造函数是生成对象的模板，一个构造函数可以生成多个对象，每个对象都有相同的结构。**

#### 缺点：

a.每当实例化一个对象时，需要调用一次构造函数的某个方法或某个属性，使得每次调用都会在栈中占用内存，造成内存污染。

b.所有的实例对象都可以继承构造器函数中的属性和方法，但是对同一个对象实例之间，无法共享属性

解决思路：

　a:所有实例都会通过原型链引用到prototype

　b:prototype相当于特定类型所有实例都可以访问到的一个公共容器

　c:那么我们就将重复的东西放到公共容易就好了

#### 特点

a.构造函数的首字母必须大写，用来区分于普通函数

b.内部使用的this对象,指向即将要生成的实例对象

c.使用new来生成实例对象

ef:

```js
function Person(name,age){
    this.name=name;
    this.age=age;
    this.sayHello=function(){
        console.log(this.name+'say hello');
    }
}
var boy=new Person('David',22);
console.log(boy.sayHello（）)；
```



