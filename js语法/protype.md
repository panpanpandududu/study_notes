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

function uique(arr){
    var new_arr = [];
    for (let i = 0; i < arr.length; i++){
        var item = arr[i];
        if (new_arr.indexOf(item) == -1){
            new_arr.push(arr[i]);
        }
    }
    return new_arr;
}

const ab = arr => arr.reduce((a, c) => {
    !a.includes(c) && a.push(c);
    return a;
}, []);

const s = arr => arr.reduce((a, c) => a.includes(c) ? a : a.concat(c));
const c = arr => {
    const map = new Map();
    return arr.filter(v => map.has(v) ? false : map.set(v));
};


arr.reduce((a, c) => a + c, 0);
uique(arr);
//
var obj = new Set(arr);
console.log(obj);

var new_arrs = Array.from(obj);
console.log(new_arrs);


const n = [...new Set(arr)];


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

