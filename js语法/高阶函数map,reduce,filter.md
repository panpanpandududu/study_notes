### 高阶函数

**定义：一个函数可以接受另一个函数作为参数**

#### 1.map()

语法形式：**List.map(f)**或**map(f,List)**

**作用：map函数接收两个参数，f为函数，List为一个序列,将参数函数f作用于List的每一个元素，然后返回一个新的List（序列)**

注意：**map是单元素，即序列元素自身调用方法**

由于map()方法定义在js的array中，我们调用array的map方法，传入我们自己的函数，得到一个新的array.

如下所示：

```js
function square(x){
    return x*x;
}
var arr=[1,2,3,4];
var results=arr.map(square); 
console.log(results);// [1, 4, 9, 16]
//将字符串转换成整数
  var arr_string== ['1', '2', '3'];
  var r = arr_string.map(s=>parseInt(s));
  console.log(r);
```

#### 2.reduce()

#### //reduce方法也是定义在数组`Array`上

作用：array的`reduce()`把一个函数作用在这个array的`[x1, x2, x3...]`上，这个函数必须接收两个参数，reduce把结果继续和序列的下一个元素做累积计算，其效果就是如下：

```js
[x1, x2, x3, x4].reduce(f) = f(f(f(x1, x2), x3), x4)
```

如数组求和

```js
  //数组求和
  function sum(x,y){
    return x+y;
  }
  var arr=[1,2,3,4];
  var rs=arr.reduce(sum);
  console.log(rs);//10
```

#### 3.filter()

作用：把数组的某些元素过滤掉，返回剩下的元素

