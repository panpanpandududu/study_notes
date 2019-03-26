```js
var arr = [1, 2, 3, 3];
console.log(arr.push(9));
Array.prototype.insert = function(item, index){
    // let start=this.slice(0,index);
    // let end=this.slice(index,this.length);
    let start = this.filter((v, i) => i < index);
    let end = this.filter((v, i) => i >= index);
    return [...start, item, ...end];
};
var b = arr.insert(4, 2);
console.log('this b', b);

//用原型链实现filter（）方法
Array.prototype.myfilter = function(callback){
    var res = [];
    for (var i = 0; i < this.length; i++){
        var v = this[i];
        if (callback(v, i, this)) res.push(arr[i]);
    }
    return res;
};
var arr = [1, 2, 3];
arr.myfilter();
console.log(arr.myfilter());
```

## 原型链

#### 定义：

每个实例对象都有一个私有属性（`_proto_`）指向它的原型对象（**prototype**）。该原型对象也有一个原型对象**`_proto_`**,层层向上直到一个对象的原型对象为null，根据定义，null没有原型，作为此原型链中的最后一个环节。这种一级一级的链型结构称之为原型链（**prototype chain**）。

实际上定义一个对象的时候原型链本身就已经生成了。javascript处处皆对象的思想在这里理解起来就很容易了。**万物始于object.prototype.**

#### 结论：

**1.`_proto_`是原型链查询中实际用到的，总是指向prototype;**

**2.`prototype`在定义构造函数时自动创建，总是被`_proto_`所指**

从上可知，`prototype`只能作为构造函数的属性，而`_proto__`可以作为任何对象的属性。

#### 图解：

![20190314142755.png](https://user-gold-cdn.xitu.io/2019/3/14/1697caac2a745a9e?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)

Person:构造函数

Person.prototype:原型（对象）

person：实例

构造函数`Person`通过内部的`prototype`属性访问到原型，实例`person`通过`_proto_`访问到原型，既然构造函数通过 `prototype` 来访问到原型，那么原型也应该能够通过某种途径访问到构造函数，这就是 `constructor`

注意：constructor是原型的一个属性，Constructor指的是真正的构造函数

```js
function Person(){}
res= Person.prototype.constructor === Person //true
person = new Person()
res = person._proto === Person.prototype  //true

//实例访问构造函数
res = person._proto_.constructor ===Person; //true
```

在获取一个实例的属性的过程中，如果属性在该实例中没有找到，就会循着`_proto_`指定的原型上去寻找，如果找不到，尝试寻找圆形的原型。







