数组是除了Object外最常用类型，具有与其他语言数组顺序存放数据一样的特性外，还具有如下特性：
- 每一项可以保存任何类型的数据
- 数组的容量大小是可以动态调整的

# 创建
创建数组有两种基本方式
- 构造函数方式
```` 
let colors = new Array(); //空数组
let colors = new Array(20); //创建容量大小为20的数组
let colors = new Array('red','blue'); // 创建包含2个字符串的数组
    
// 以上所有的new可以省略
let colors = Array(); //空数组
let colors = Array(20); //创建容量大小为20的数组
let colors = Array('red','blue'); // 创建包含2个字符串的数组
```` 

- 常量式
由一对包含数组项的中括号（[]）表示，多个数据项之间以逗号（，）隔开
```` 
let colors = []; //空数组
let colors = ['red','blue']; // 创建包含2个字符串的数组
````

# 操作

## 获取长度
可以通过length属性获取数组的大小
````
let colors = ['red', 'blue'];
let length = colors.length; //值为2
````

## 检测数组
通过isArray()静态方法判断一个变量是否式数组
````$xslt
const a = someValue;
if(Array.isArray(a)){
}
````

## 转换
通过join()方法统一添加分隔符并返回

````
const colors = ['red', 'blue', 'green'];
const a = colors.join(','); // a的值为'red,blue,green'
const b = colors.join('&'); // b的值为'red&blue&green'
````
> 如果不给join()方法传入任何参数，或传入undefined，则使用逗号作为分隔符。

## 增删改查
- 栈方法
    - push()方法，可以接收任意数量的参数，把它们逐个添加到数组的尾部，并返回新数组长度
    - pop()方法，移除数组最后一个元素，改变数组长度，并返回移除的元素
````
let colors =[];

let a = colors.push('red', 'blue'); //a =2, colors = ['red', 'blue'];
let b = colors.push('green'); //b = 3, colors = ['red', 'blue', 'green']

let c = colors.pop(); // c = 'green', colors = ['red', 'blue']
````

- 队列方法
    - shift()方法，移除数组的第一个元素并返回该元素，数组长度减一
    - unshift()方法，在数组前面添加元素，并返回新数组的长度
 ````
 let colors =['red', 'blue', 'green'];
 
 let a = colors.shift(); //a ='red', colors = ['blue', 'green'];
 let b = colors.unshift('black'); //b = 3, colors = ['black', 'blue', 'green']
 ````
 
 - 排序
    - sort()方法，默认按照字符串升序排序，一般都不满足要求，需要传入比较函数才能正确工作
    - reverse()方法，倒序，不比较大小
`````
let a = [1, 2, 9, 3, 10];

let b = a.reverse(); //b = [10, 3, 9, 2, 1], a和b相同
let c = a.sort(); //c = [1,10, 2, 3, 9], a和c相同

`````
> sort()方法默认排序是按照元素toString()后排序的，所以很多时候这并不能满足当前的需求，所以提供了传入比较函数的参数，比较函数接收两个参数，
如果第一个参数应该位于第二个参数之前则返回一个负数，如果相等返回0，如果第一个参数应该位于第二个参数之后则返回一个正数。

````
function compare(value1, value2){
    if(value1 < value2){
        return -1;
    } else if(value1 > value2){
        return 1;
    } else{
        return 0;
    }
}

let a = [1, 2, 9, 3, 10];

let b = a.reverse(); //b = [10, 3, 9, 2, 1], a和b相同
let c = a.sort(compare); //c = [1, 2, 3, 9, 10], a和c相同
````
> 对于数值类型或者valueOf()方法返回数值类型的元素，可以使用一个简单的比较函数，该函数只要用第二个值减去第一个值即可。
````
function compare(value1, value2){
    return value2 - value1;
}
````
- concat()方法  
基于当前数组中所有元素创建一个新数组
````
let colors = ['red', 'blue'];
let a = colors.concat('green', ['white', 'black']); 
// colors = ['red', 'blue'] 保持不变
// a = ['red', 'blue', 'green', 'white', 'black'] 合并后的数组   
````

- slice()方法
基于当前数组中的一个或多个元素创建一个新数组，可以接收一个或者两个参数，即子数组的其实位置和结束位置（不含）。
````
let colors = ['red', 'blue', 'green'];

let a = colors.slice(1); // 从1开始到结束， a = ['blue', 'green'], colors = ['red', 'blue', 'green']
let b = colors.slice(1, 2); // 从1开始到2但不包含2，b = ['blue'], colors = ['red', 'blue', 'green']
````
> 如果slice()方法中的参数中有一个负数，则用数组长度加上该数来确定相应的位置，如果其实位置大于结束位置返回空数组。

- splice()方法
基于当前数组进行删除、插入和替换操作，接收三个参数，即起始位置、要删除元素的个数和新的任意数量元素，返回删除元素组成的数组
    - 删除   
    可以删除任意数量的元素，只需指定2个参数：要删除的第一项的位置和要删除的元素个数。
    - 插入 
    可以向指定位置插入任意数量的元素，只需指定3个参数：起始位置、0（要删除的元素个数）、要插入任意数量的元素
    - 替换 
    可以向指定位置插入任意数量的元素，且同时删除任意数量的元素，只需指定3个参数：起始位置、要删除的元素个数、要插入任意数量的元素
    
````
let a = ['red', 'blue', 'green'];

let b = a.splice(0, 1);//从0开始删除一个元素，b = ['red'], a = ['blue', 'green']
let c = a.splice(0, 0, ['white','black']);//从0开始插入两个元素，c = [], a = ['white','black','blue', 'green']
let d = a.splice(0, 1, ['orange','yellow']);//从0开始删除一个元素然后插入两个元素，d = ['white'], a = ['orange','yellow','black','blue', 'green']
````

- 查找
    - indexOf()方法     
    从数组的头部开始查找，接收两个参数，即要查找的元素和起始位置（可选），返回要查找元素在当前数组的位置
    - lastIndexOf()方法      
    从数组的尾部开始查找，接收两个参数，即要查找的元素和起始位置（可选），返回要查找元素在当前数组的位置
