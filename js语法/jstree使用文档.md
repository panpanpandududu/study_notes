

### 函数防抖和节流

问题来源：在前端开发

#### 1.每秒显示一次的方法：

**a.利用时间戳，判断显示时间差是否大于设置的定时时间**

```js
let num = 1;
let content = document.getElementById('content');

function test(fn,delay) {
    let lastTime = 0;//设置初始时间
    return function() {
        const now = Data.now();//获取当前时间
        //根据时间差是否比时间间隔长，来决定是否返回函数
        if(now - lastTime <= delay) return; 
        fn(arguments);//隐形else判断而来，now - lastTime > delay执行
        lastTime = now;//重新赋值初始时间
    };
};

function count(){
    content.innerHTML = num++;
};
content.onmousemove = test(count,1000);
```

b.**利用setTimeout()**，设置标签，根据标签的状态值

```js
let num = 1;
let content = document.getElementById('content');
function test(fn,delay) {
    let canRun = true; //定义一个标签来实现，根据标签状态来判断
    return function() {
        if(!canRun) return;
        if(canRun) fn(arguments);
        canRun = false;
        setTimeout(()=>{
            canRun = true;
        }, delay);
    };
};

function count(){
    content.innerHTML = num++;
};
content.onmousemove = test(count,1000);

```

**c.当多长时间后触发**

```js
let num = 1;
let content = document.getElementById('content');

function test(fn,delay) {
    let time;
    return function() {
        if (time){
            clearTimeout(time);
        }
        time =  setTimeout(()=>{
            time = null;
            fn(arguments);
        }, delay);
    };
};

function count(){
    content.innerHTML = num++;
};
content.onmousemove = test(count,1000);
```

**d.时间段内显示一次**

```js
let num = 1;
let content = document.getElementById('content');

function test(fn,delay) {
    let time;
    return function() {
        if (time){
            clearTimeout(time);
        }
        if (!time) fn(arguments);
        time =  setTimeout(()=>{
            time = null;
        }, delay);
    };
};

function count(){
    content.innerHTML = num++;
};
content.onmousemove = test(count,1000);
```

