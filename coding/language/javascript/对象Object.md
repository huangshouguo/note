# 创建
创建数组有两种基本方式
- 构造方法
````
let p = new Person();
````

- 常量式

````
let person = {
    name: 'mk',
    age: 25
}
````

# 访问属性
````
let person = {
    name = 'mk'
}

let name = person.name; //第一种方式
let name = person['name']; // 第二种方式
````

# 常用属性
定义枚举常量

````
const COLORS = Object.freeze({
    red: 'red',
    blue: 'blue'
});
````

# 对象合并

````
const a = {};
const b = {};

const result = Object.assign({}, a, b);//这样即使a或者b为undefined 均不会崩溃
````