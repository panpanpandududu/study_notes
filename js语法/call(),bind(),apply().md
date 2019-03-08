#### JS中的每一个function对象都有一个apply（）方法和一个call（）方法

语法分别为：

```js
//call()方法   
//thisObj指代的是将被用作当前对象的对象  argN指将被传递方法参数序列
function.call(thisObj[, arg1[, arg2[,...argN]]]);
//apply()方法
function.apply(thisObj[, argArray]); //argArray指代序列（数组）

```

call（）和apply（）的第一个实参是要调用函数的母对象，它是调用上下文，在函数体内通过this来获得对它的引用。要想以对象o的方法来调用函数f（）,可以如下操作：

```js
f.call(o);
f.apply(o);
```

#### call()

定义：**调用一个对象的一个方法，用另一个对象替换当前对象**。

说明：call方法可以用来代替另一对象调用一个方法，call方法可将一个函数的对象上下文从初始的上下文改变为由thisObj指定的新对象

如：`B.call(A,args1,args2); `//A对象调用B对象的方法

**call有两个妙用：1.继承 2.修改函数运行时的this指针**

#### apply()

说明：apply方法传入两个参数，第一个参数作为函数上下文的对象。另外一个作为参数所组成的数组。





