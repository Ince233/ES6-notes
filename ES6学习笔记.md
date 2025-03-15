# forECMA

European Computer Manufacturers Association, 开发评估计算机标准的欧洲组织

## ECMASript

ECMA-262标准化制定的脚本程序设计语言

## ECMA历史版本

见网站

# let变量声明以及声明特性

```javascript
//声明
let a;

let b,c,d;

let e = 100;

let f = 521, g = 'es6', h = [];

//1 变量不能重复声明
let star = 'Taylor';
let star = 'Swift';//let 会报错，var不会

//2 块级作用域 全局 函数 eval
//包括if else while for 的大括号中都为块级作用域
{
    let girl = 'Amy';
}
console.log(girl);//let会报错，因为有块级作用域，而var不会报错

//3 不存在变量提升
console.log(song);
var song = 'love';
//输出undefined，可在变量声明前使用它
console.log(song);
let song = 'love';
//会报错

//4 不影响作用域链
{
    let school = 'sgg';
    function fn(){
        console.log(school);
    }
    fn();//输出sgg
}
//函数作用域内找不到school的声明便往上级作用域寻找，不会因为块级作用域导致报错
```

## 案例 切换颜色

```javascript
//获取div元素对象
let items = document.getElementsByClassName('item');

//遍历并绑定事件
for(var i = 0; i < items.length; i++){
    items[i].onclick = function(){
        //修改当前元素的背景颜色
        this.style.background = 'pink';
        //这里this不能用items[i]，因为var声明的i不存在块级作用域，items[i]向上级window寻找i时，i的值已经为3，超过items的长度
    }
}
//使用let可以解决这个问题
for(let i = 0; i < items.length; i++){
    items[i].onclick = function(){
        //修改当前元素的背景颜色
        items[i].style.background = 'pink';
        //这里可以用items[i]，因为let声明的i存在块级作用域，每次循环都存在一个块级作用域分别声明i=0,1,2
    }
}
```

# const声明常量以及特点

```javascript
//声明常量
const SCHOOL = 'sgg';

//1 一定要赋初始值
const a;//会报错

//2 一般常量命名使用大写（潜规则）

//3 常量的值不能修改
SCHOOL = ‘hm’;//会报错

//4 块级作用域
{
    const PLAYER = 'UZI';
}
console.log(PLAYER;)//会报错

//5 对于数组和对象的元素修改，不算做对常量的修改，不会报错
const TEAM = ['UZI','MLXG','Ming'];
TEAM.push('Meiko');//不会报错，因为数组地址没变
TEAM = 100；//报错，因为地址都改了
```



# 变量的解构赋值

```javascript
//ES6允许按照一定模式从数组和对象中提取值，对变量进行赋值
//称为解构赋值
//1 数组的解构
const F4 = ['ALICE','BOB','CARLO'];
let [a,b,c] = F4;

console.log(a);
console.log(b);
console.log(c);
//输出ALICE,BOB,CARLO

//2 对象的解构

const zhao = {
    name: 'zhaobenshan',
    age: 'unknown',
    xiaopin: function(){
        console.log("I can perform xiaopin");
    }
}

let {name, age, xiaopin} = zhao;

console.log(name);
console.log(age);
console.log(xiaopin);
xiaopin();
```

# 模板字符串

```javascript
//ES6引入新的字符串声明方式``,之前'',""
//1 声明
let str = `反引号字符串`

//2 内容中可以直接出现换行符
let str = '<ul><li>沈腾</li><li>马力</li><li>艾伦</li></ul>'//只能放在一行
let str = `<ul>
			<li>沈腾</li>
			<li>马力</li>	
			<li>艾伦</li>
		   </ul>`
//3 变量拼接
let love = 'wei'
let out = love + 'is the best actor'//只能用+拼接
let out = `${love}is the greatest actor//用${}拼接
 
```

# 对象的简化写法

```javascript
//ES6允许在大括号里面，直接写入变量和函数，作为对象的属性和方法，更加简洁
let name = 'sgg';
let change = function(){
    console.log('we can change you');
}

const school ={
    name: name,
    change: change,
    improve(){
        console.log('we can improve you');
    }
}

//由于school属性的键与变量名相同，可以省略成一个
const school ={
    name,
    change,
    improve(){
        console.log('we can improve you');
    }
}

console.log(school.name);//输出sgg
console.log(school.change);//输出function(){console.log('we can change you')}
school.change;//输出we can change you
```

# 箭头函数以及声明特点

```javascript
//ES6允许使用箭头=>声明函数
let fn = functuon(){
    
}
//声明函数
let fn (a,b) => {
    return a+b;
}
//调用函数
let result = fn(1,2);
console.log(result);//输出3

//1 this是静态的，始终指向函数声明（定义）时所在作用域下的this值/定义时的上一级作用域
function getName(){
    console.log(this.name);
}

let getName2 = () => {
    console.log(this.name);
}
//设置window的name属性
window.name = 'sgg';
const shcool = {
    name: 'atsgg'
}

//直接调用
getName();//输出sgg
getName2();//输出sgg

//call方法调用
getName.call(shcool);//输出atsgg
getName2.call(shcool);//输出sgg，this是静态的，继承上一级的name

//2 不能作为构造实例化对象
let Person = (name,age) => {
    this.name = name;
    this.age = age;
}

let me = new Person('Ming', 20);
console.log(me);//报错

//3 不能使用arguments变量
let fn = () => {
    console.log(arguments);
}
fn(1,2);//报错

//4 箭头函数的简写
let add n => n + n;//形参有且只有一个时，省略小括号，代码体只有一行时，省略花括号和return，语句的执行结果就是函数的返回值
```

## 案例 点击div2秒后变粉色

```javascript
//获取元素
let ad = document.getElementById('ad')

//绑定事件
ad.addEventListener("click",function(){
    //定时器
    setTimeout(function(){
        //修改背景颜色 this
        this.style.background = 'pink';//setTimeout的this指向window
    },2000);
});

//获取元素
let ad = document.getElementById('ad')

//解决方式1：外层保存ad为this
ad.addEventListener("click",function(){
    let _this = this;
    setTimeout(function(){
        _this.style.background = 'pink';
    },2000);
});

//解决方式2：使用箭头函数
ad.addEventListener("click",function(){
    //在外层作用域声明的function，所以this指向ad
    setTimeout(()=>{
        this.style.background = 'pink';
    },2000);
});

```

## 案例 从数组中返回偶数元素

```javascript
const arr =[1,2,6,9,10]
const result = arr.filter(function(item){
    if(item % 2 === 0)
        return true;
    else
        return false;
});

const result = arr.filter(item => item % 2 === 0);
console.log(reslut);
//普通函数的this指向调用者，箭头函数的this指向定义时的作用域
//箭头函数适合与this无关的回调，定时器，数组的方法
//不适合与this有关的回调，事件回调，对象的方法，不适合而不是不能
{
    name:"sgg",
    getName:()=>{
        console.log(this.name);//这里的this指向外层window
    }
}
```

# 函数参数的默认值设置

```javascript
//ES6允许给函数参数赋初始值
//1 形参初始值 具有默认值的参数，一般位置要靠后
function add(a,b,c = 10){
    return a + b + c;
} 
let result = add(1,2);
console.log(result);
//2 与解构赋值结合使用
function connect(options){
    let host = options.host;
    let username = options.username;
    ...//很麻烦
}
//可以写作
    function connect({host ="127.0.0.1",username,password,port}){
    console.log(host)
    console.log(username)
    console.log(password)
    console.log(port)//更加方便
}
connect({
    host: 'localhost',
    username: 'root',
    password: 'root',
    port: 3306
})
```

# rest参数

```javascript
//ES6引入rest参数，用于获取函数的实参，用来代替arguments
//ES5获取实参的方式
function data(){
    console.log(arguments);//是一个对象
}
data('a','b','c');

//rest参数
function data(...args){
    console.log(args);//是一个数组，可以使用filter,some,every,map等方法
}
data('a','b','c')

//...args必须放到形参的最后
function data(a,b,...args){//不能放前面或中间
    console.log(a);
    console.log(b);
    console.log(...args);
}
data(1,2,3,4,5,6)//输出第一行1，第二行为2，第三行为[3,4,5,6]
```

# 扩展运算符

```javascript
//...扩展运算符
//能将数组转换为逗号分隔的参数序列
const BOYS = ['Bob','Alice','Jake'];

function perform(){
    console.log(arguments);
}
perform(BOYS);//只能传入第一个参数'Bob'
perform(...BOYS);//可以传入'Bob','Alice','Jake'
```

## 案例 数组操作

```javascript
const MEN = ['Taili','Xiaoyang'];
const WOMEN = ['Zengyi','Linghua']
//1 数组的合并
const APPLE = MEN.concat(WOMEN);//数组合并
const APPLE2 = [...MEN,...WOMEN];//也可以做到数组合并

//2 数组的克隆
const APPLE3 = [...APPLE2]//克隆到APPLE3

//3 将伪数组转换成真数组
const DIVS = document.querySelectorAll('div');//原型是对象
const DIVARR = [...DIVS];//转换成了数组
//arguments也可以转，但是有了rest所以没必要
```



# Symbol新数据类型

特点：

1. Symbol值是唯一的，用来解决命名冲突
2. Symbol值不能与其他数据进行运算
3. Symbol定义的对象属性不能使用for...in进行循环遍历，但是可以使用Reflect.ownKeys来获取对象的所有键名

```javascript
//创建Symbol
let s1 = Symbol();
console.log(s1,typeof s1);//输出Symbol() "symbol"

//每次调用 Symbol()，即使传入相同的描述字符串，都会创建一个全新的唯一 Symbol 值
//这些 Symbol 互不相等，即使描述（description）相同
let s2 = Symbol('frontend');
let s3 = Symbol('frontend');

console.log(s2 === s3);//返回false

//Symbol.for()创建与Symbol()的不同
//Symbol.for() 会在 全局 Symbol 注册表（Global Symbol Registry）中查找是否已存在相同 key 的 Symbol
//如果 存在，则返回已存在的 Symbol（即复用）
//如果 不存在，则创建一个新的 Symbol 并存入注册表
let s4 = Symbol.for('web');
let s5 = Symbol.for('web');

console.log(s4 === s5);//返回true

//不能与其他数据进行运算

let result = s + 100;
let result = s > 100;//都会报错

```

补充：Js的所有数据类型：USONB

U: undefined

S: string symbol

O: object

N: null number

B: boolean

## 案例 向对象中添加属性和方法

```javascript
let game ={}

game.up = function(){

}//想向game中添加方法，不确定game中是否已经有up,这样效率低

let methods = {
    up:Symbol(),
    down:Symbol()
};

game[methods.up] = function(){
    console.log("a methods to change shapes")
}

game[methods.down] = function(){
    console.log("a methods to go down")
}//安全快速的将方法添加到对象game里面

```

# Symbol内置值

P17跳过

# 迭代器iterator

P19没看懂

# 生成器 特殊的函数

P21-24没看懂

应用：

异步编程？

文件操作，网络操作（ajax, request），数据库操作

模拟获取 用户数据 订单数据 商品数据

# Promise语法

## Promise的基本使用

ES6引入的异步编程的新方案。语法上Promise是一个构造函数，用来封装异步操作，并可以获取其成功或失败的结果

1. Promise构造函数：Promise(exrcutor){}
2. Promise.prototype.then方法
3. Promise.prototype.catch方法

```javascript
const p =new Promise(function(resolve,reject){
    setTimeout(function(){
        let data = '数据库中的用户数据';
        //resolve代表成功
        resolve(data);
        
        let err = '读取失败';
        reject(data);
    },1000);
});

p.then(function(value){
    //成功执行的代码
    console.log(value);
},function(reason){
    //失败执行的代码
    console.error(reason);
});
```

### 案例 Promise封装读取文件

```javascript
//1 引入fs模块
const fs = require('fs');

//2 调用方法读取文件
fs.readFile('./resources/file.md',(err,data)=>{
    if(err) throw err;
    
    console.log(data.toString());
});

//3 使用Promise封装
const p = new Promise(function(resolve,reject){
    fs.readFile("./resources/file.md",(err,data)=>{
        //判断如果失败
        if(err) reject(err);
        //判断如果成功
        resolve(data);
    });
});

p.then(function(value){
    console.log(value.toString());
},function(reason){
    console.log("读取失败")；
})
```

### 案例 Promise封装AJAX请求

```javascript
//接口地址:https://api.apiopen.top/getJoke

//传统方法
//1 创建对象
const xhr = new XMLHttpRequest();

//2 初始化
xhr.open("GET", "https://api.apiopen.top/getJoke");

//3 发送
xhr.send();

//4 绑定事件
xhr.onreadystatechange = function(){
    //判断
    if(xhr.readyState == 4){
        //判断响应状态码
        if(xhr.status >= 200 && xhr.status < 300){
            //表示成功
            console.log(xhr.response);
        }else{
            //如果失败
            console.error(xhr.status);
        }
    }
}

//Promise方法
//1 创建对象

const p = new Promise((resolve,reject) =>{
    const xhr = new XMLHttpRequest();

    //2 初始化
    xhr.open("GET", "https://api.apiopen.top/getJoke");

    //3 发送
    xhr.send();

    //4 绑定事件
    xhr.onreadystatechange = function(){
        //判断
        if(xhr.readyState == 4){
            //判断响应状态码
            if(xhr.status >= 200 && xhr.status < 300){
                //表示成功
                resolve(xhr.response);
            }else{
                //如果失败
                reject(xhr.status);
            }
        }
    }
})

p.then(function(value){
    //对数据做处理
    console.log(value);
},function(reason){
    console.log(reason);
});

```

## Promise.prototype...then方法

```javascript
//创建promise对象
const p = new Promise((resolve,reject) => {
    setTimeout(()=>{
        resolve("用户数据")；
    },1000);
});

//调用then方法
const result = p.then(value =>{
    console.log(value);
    //return 123;
    return new Promise((resolve,reject) => {
        //resolve("OK");
        reject('error');
    })
},reason =>{
    console.warn(reason);
}
);

console.log(result);//输出一个promise对象，说明then返回结果也是promise,其结果由回调函数的返回结果决定
//1 如果回调函数中的返回结果是非promise类型的属性，状态为成功，返回值为对象的成功值
//2 如果回调函数中的返回结果promise类型的属性
//3 抛出错误，则失败值就是错误
//then方法可以链式调用
```

### 案例 多文件内容读取

```javascript

```

## Promise的catch方法

```javascript
const p = Promise((resolve, reject) =>{
    setTimeout(() => {
        reject("出错啦")
	},1000);
});
//p.then(null, reason => {...}) 和 p.catch(reason => {...}) 在处理 Promise 拒绝时的效果是一样的
//catch 语法简洁且清晰，通常用于处理拒绝情况，而 then 既可以处理成功，也可以处理失败，适用于更复杂的场景
catch 语法简洁且清晰，通常用于处理拒绝情况，而 then 既可以处理成功，也可以处理失败，适用于更复杂的场景。
p.then(value => {
    
},reason => {
    console.error(reason);
});

p.catch(reason =>{
    console.warn(reason);
});
```

# Class类

## class关键字引入

引入class关键字，但其功能ES5都可以实现

```javascript
//ES5完成手机类
function phone(brand,price){
    this.brand = brand;
    this.price = price;
}
//添加方法
phone.prototype.call = function(){
    console.log('I can make a call');
}

let huawei = new phone('华为'，3999);
Huawai.call();
console.log(Huawei);
```

```javascript
//ES6完成手机类
class phone{
    //构造方法 名字不能修改
    constructor(brand,price){
        this.brand = brand;
    	this.price = price;
    }
    //必须使用该语法不能使用ES5的对象完整形式,应省略:function
    //call: function(){};错误
    call(){
        console.log("I can make a call");
    }
}

let onePlus = new phone('1+',2999);
onePlus.call();
console.log(onePlus);
```

## class静态成员

```javascript
//ES5
function phone(){
    
}
phone.name = '手机';
phone.change = function(){
    console.log('I can change the world');
}

phone.prototype.size = "5.5inch";
const nokia = new phone();
console.log(nokia.name);//undefined
console.log(phone.name);//可输出'手机'
nokia.change();//undrfined
phone.change();//输出"I can change the world"
console.log(nokia.size);//可输出"5.5inch"
//name,change是属于函数对象（类）的，只有phone类能访问，实例nokia不能访问，称为静态成员
//size是属于实例的，nokia能访问，而phone类不能访问
```

```javascript
//ES6
class phone{
    //静态成员
    static name = '手机';
	static change(){
        console.log('I can change the world');
    }
}

let nokia = new phone();
console.log(phone.name);//输出"手机"
console.log(nokia.name);//undefined
phone.change();//输出"I can change the world"
//static直接定义了静态成员，只有该phone类能访问，该对象的实例nokia不能访问
```

## 构造函数继承(ES5)

```javascript
//ES5写法
function phone(brand, price){
    this.brand = brand;
    this.price = price;
}

Phone.prototype.call = function(){
    console.log("I can make a call");
}

//智能手机
function smartPhone(brand, price, color, size){
    phone.call(this,brand,price);
    this.color = color;
    this.size = size;
}

//设置子级构造函数的原型
smartPhone.prototype = new phone;
smartPhone.prototype.constructor = smartPhone;

//声明子类的方法
smartPhone.prototype.photo = function(){
    console.log('I can take a photo');
}

const xiaomi = new smartPhone('小米',2499,'黑色','5.5inch');
```

## class类继承

```javascript
//ES5类继承
class phone{
    //构造方法
    constructor(brand, price){
        this.brand = brand;
        this.price = price;
    }
    call(){
        console.log('I can make a call');
    }
}

class smartPhone extends phone{
    constructor(brand, price, color, size){
        super(brand, price);
        this.color = color;
        this.size = size;
    }
    photo(){
        console.log('I can take a photo');
    }
}

const xiaomi = new smartPhone('小米',2499,'黑色','5.5inch');//父类方法在_proto_里面
```

## 子类对父类的方法重写

```javascript
//ES5类继承
class phone{
    //构造方法
    constructor(brand, price){
        this.brand = brand;
        this.price = price;
    }
    call(){
        console.log('I can make a call');
    }
}

class smartPhone extends phone{
    constructor(brand, price, color, size){
        super(brand, price);
        this.color = color;
        this.size = size;
    }
    photo(){
        console.log('I can take a photo');
    }
    //重写
    call(){
        console.log('I can make a video call');//父类的 call() 方法依然存在，但是由于子类的 call() 方法覆盖了父类的方法，所以当你调用 smartPhone 实例的 call() 方法时，它会调用子类的实现。
    }
}

const xiaomi = new smartPhone('小米',2499,'黑色','5.5inch');//父类方法在_proto_里面
xiaomi.call(); // 调用的是子类的 call 方法，输出: 'I can make a video call'
xiaomi.photo(); // 调用子类的 photo 方法，输出: 'I can take a photo'

const iphone = new phone('苹果', 5999);
iphone.call(); // 调用的是父类的 call 方法，输出: 'I can make a call'

xiaomi.call = function() { console.log("Overridden in instance"); }//实例级别的重写可覆盖类
xiaomi.call(); // 输出: 'Overridden in instance'

```

## get和set

```javascript
class phone{
    get price(){
        console.log('price is read');
        return 'ok';
    }
    set price(newVal){
        console.log('price is revised');
    }
}

let s = new phone();
console.log(s.price);

s.price = 'free';
//输出'price is revised'
```



# 模块化

指将一个大的程序文件，拆分成许多小的文件，然后将小文件组合起来

模块化的好处：

- 防止命名冲突
- 代码复用
- 高维护性

ES6之前的模块化产品有:

CommonJS: NodeJs,Browserify

AMD: requireJS

CMD: seaJS

模块化语法：

两个命令：export and import

export 用于规定模块的对外接口

import用于输入其他模块提供的功能

```javascript
//命名导入：适用于多个导入
export let school = 'sgg';

export function teach(){
    console.log("a function which is exported");
}
//命名为some.js
```

```javascript
//在另一个html文件引入some.js
import * as m1 from "./some.js";
//或 import {school, teach} from "./some.js";
console.log(m1);
```

```javascript
//默认导入：适用于单一主要功能导入
export default class User{
    constructor(name) {
        this.name = name;
    }
}
//命名为some.js
```

```javascript
import MyUser from "./some.js";
const newUser = new MyUser("Bob");
console.log(newUser.name);
```

```javascript
//混合导入
export let school = 'sgg';

export function teach(){
    console.log("a function which is exported");
}

export default class User{
    constructor(name) {
        this.name = name;
    }
}
//命名为config.js
```

```javascript
import MyUser,{school, teach} from "./config.js";
```

```javascript
//标签内引入
//标签属性引入
<script src = "./src/js/app.js" type = "module"></script>
//入口文件

//模块引入
import * as m1 from "./m1.js";
import * as m2 from "./m2.js";
import * as m3 from "./m3.js";

```

# Js基础补充

## Js数组的方法

| 方法        | 是否修改原数组 | 参数                           | 返回值               | 作用                         | 回调函数参数                                          |
| ----------- | -------------- | ------------------------------ | -------------------- | ---------------------------- | ----------------------------------------------------- |
| pop()       | ✅              | 无                             | 被删除的元素         | 删除最后一个元素             | 无                                                    |
| push()      | ✅              | 一个或多个要添加的元素         | 新数组长度           | 追加元素到数组末尾           | 无                                                    |
| shift()     | ✅              | 无                             | 被删除的元素         | 删除第一个元素               | 无                                                    |
| unshift()   | ✅              | 一个或多个要添加的元素         | 新数组长度           | 在数组开头添加元素           | 无                                                    |
| reverse()   | ✅              | 无                             | 修改后的数组         | 反转数组                     | 无                                                    |
| sort()      | ✅              | 排序函数（可选）               | 修改后的数组         | 排序数组（默认按字符串排序） | `a`, `b`（比较的两个元素）                            |
| splice()    | ✅              | 起始索引、删除个数、插入的元素 | 被删除的元素数组     | 删除/替换/插入元素           | `value`, `index`, `array`（数组元素及其索引）         |
| forEach()   | ❌              | 回调函数                       | undefined            | 遍历数组，不返回新数组       | `element`, `index`, `array`（当前元素、索引、原数组） |
| map()       | ❌              | 回调函数                       | 新数组               | 遍历数组并返回新数组         | `element`, `index`, `array`（当前元素、索引、原数组） |
| filter()    | ❌              | 回调函数                       | 新数组               | 过滤数组并返回符合条件的元素 | `element`, `index`, `array`（当前元素、索引、原数组） |
| some()      | ❌              | 回调函数                       | true / false         | 是否有元素符合条件           | `element`, `index`, `array`（当前元素、索引、原数组） |
| find()      | ❌              | 回调函数                       | 第一个符合条件的元素 | 找到符合条件的第一个元素     | `element`, `index`, `array`（当前元素、索引、原数组） |
| findIndex() | ❌              | 回调函数                       | 第一个符合条件的索引 | 找到符合条件的第一个元素索引 | `element`, `index`, `array`（当前元素、索引、原数组） |
| slice()     | ❌              | 起始索引、结束索引（可选）     | 新数组               | 返回数组的一个片段           | 无                                                    |

```javascript
//forEach打印数组元素的平方
const numbers = [2,4,6,8,10];
numbers.forEach(val => {
    console.log(val * val);
})
//map创建新数组=原数组+1
const nums = [1, 2, 3, 4, 5]
const newnums = nums.map(val1,val2 => val1 + 1 );//val2可省略
console.log(newnums);
//filter筛选元素>5
const mixed = [3, 7, 8, 1, 2, 9, 5]
const larger = mixed.filter(val1,val2 => val1 > 5);//val2可省略
console.log(larger);
//some查找是否存在>18的元素
const ages = [21, 16, 18, 24, 30]
const exist = age.some(val,val2 => val1 > 18);//val2可省略
console.log(exist);
//find查找第一个符合条件的元素
const students = [
  {name: "Alice", age: 18},
  {name: "Bob", age: 22},
  {name: "Charlie", age: 17}
];
const first = students.find(stu => stu.name === "Charlie");
console.log(first);
//findIndex查找第一个符合条件的元素索引
const names = ["Alice", "Bob", "Charlie", "David"];
const index = names.findIndex(name => name === "Charlie");
console.log(index); // 返回 2，因为 "Charlie" 在索引 2
//slice索引
const colors = ["red", "blue", "green", "yellow", "pink"];
const slicedColors = colors.slice(1, 3);//区间为左闭右开
console.log(slicedColors); // 返回 ["blue", "green"]
//splice插入元素
const fruits = ["apple", "banana", "cherry", "date"];
const removed = fruits.splice(1, 2, "orange", "pear");
console.log(fruits); // 返回 ["apple", "orange", "pear", "date"]
console.log(removed); // 返回 ["banana", "cherry"]
//sort排序
const nums = [8, 3, 12, 5, 1];
const sortedNums = nums.sort((a, b) => a - b);
console.log(sortedNums); // 返回 [1, 3, 5, 8, 12]
```



## 各种函数：

| 特性                 | 函数声明            | 函数表达式                 | 箭头函数               | 构造函数               | Generator 函数       | Async 函数                 |
| -------------------- | ------------------- | -------------------------- | ---------------------- | ---------------------- | -------------------- | -------------------------- |
| 语法                 | `function foo() {}` | `const foo = function(){}` | `const foo = () => {}` | `function Person() {}` | `function* foo() {}` | `async function foo() {}`  |
| 是否提升             | 是                  | 否                         | 否                     | 否                     | 否                   | 否                         |
| `this` 指向          | 函数的调用上下文    | 函数的调用上下文           | 外部作用域             | 新创建的对象           | 外部作用域           | 返回 `Promise`，`await` 等 |
| 是否可以作为构造函数 | 是                  | 否                         | 否                     | 是                     | 否                   | 否                         |
| 返回值               | 没有返回值          | 返回函数                   | 返回函数               | 返回新对象             | 返回迭代器对象       | 返回 `Promise` 对象        |

## 函数声明、函数表达式、与构造函数

```javascript
function add(a,b){return a+b;}//函数声明
var add=function(a,b){return a+b;}//函数表达式
var add=new Function('a','b','return a+b')//构造函数
```

## 四则运算符对字符串/数字的操作优先级

在 JavaScript 中，运算符 `+` 和 `-*/` 的行为有所不同：

1. **+ 运算符：**

   - 如果两边的操作数中有任何一个是字符串，`+` 会将其转换成字符串并执行字符串拼接。
   - 如果两边的操作数都是数字，`+` 会执行数值加法。

   例如：

   ```javascript
   javascript复制编辑console.log(5 + 3);        // 输出 8（数字加法）
   console.log('5' + 3);      // 输出 '53'（字符串拼接）
   console.log(5 + '3');      // 输出 '53'（字符串拼接）
   console.log('5' + '3');    // 输出 '53'（字符串拼接）
   ```

2. **-, \*, / 运算符：**

   - 这些运算符优先执行数值运算。如果操作数是字符串，它们会尝试将字符串转换为数字进行计算。

   例如：

   ```javascript
   javascript复制编辑console.log(5 - 3);        // 输出 2（数字减法）
   console.log('5' - 3);      // 输出 2（字符串 '5' 会转换为数字）
   console.log(5 * '3');      // 输出 15（字符串 '3' 会转换为数字）
   console.log('5' / '2');    // 输出 2.5（字符串 '5' 和 '2' 会转换为数字）
   ```

## 显式转换

- `parseInt()`：从字符串的开头将字符串解析为整数，会解析到第一个非数字字符为止，如果无法解析则返回 `NaN`。
- `Boolean()`：将值转换为布尔类型，`undefined`、`null`、`0`、空字符串、`NaN` 转换为 `false`，其他值转换为 `true`。

## **try...catch...finally 的执行顺序**

`try...catch...finally` 用于处理异常，执行顺序如下：

1. **try 代码块**：
   - 先执行 `try` 代码块中的代码。
   - 如果发生异常，则立即跳转到 `catch` 代码块，并跳过 `try` 中异常之后的代码。
   - 如果没有异常，`catch` 代码块不会执行，继续执行 `finally` 代码块。
2. **catch 代码块**（可选）：
   - 仅当 `try` 代码块中发生异常时执行 `catch` 代码块。
   - 处理异常，并防止程序崩溃。
3. **finally 代码块**（可选）：
   - **无论 try 代码块是否发生异常，finally 都会执行。**
   - 通常用于清理资源，例如关闭数据库连接、释放文件句柄等。

# JavaScript 和 CSS 的命名方式

## JS与CSS 中命名区别
在 JavaScript 中，DOM 元素的属性名采用**驼峰命名法**。例如：
- `background-color`（CSS 中的属性名）在 JavaScript 中变成了 `backgroundColor`
- `font-size` 变成了 `fontSize`
- `border-left-width` 变成了 `borderLeftWidth`

在 CSS 中，属性名使用**连接线命名法**。例如：
- `background-color`
- `font-size`
- `border-left-width`

```javascript
<div class="test"></div> 
// 在 JavaScript 中，获取类名为 'test' 的第一个元素，并修改其背景色为红色
document.getElementsByClassName("test")[0].style.backgroundColor = "red";
```

# JavaScript 获取元素的方法



| 方法                                | 返回值类型    | 说明                                     |
| ----------------------------------- | ------------- | ---------------------------------------- |
| `document.getElementsByClassName()` | `NodeList`    | 返回所有匹配的类名元素                   |
| `document.getElementsByTagName()`   | `NodeList`    | 返回所有匹配的标签元素                   |
| `document.querySelectorAll()`       | `NodeList`    | 返回所有匹配的元素（多个匹配时返回所有） |
| `document.getElementById()`         | `HTMLElement` | 返回匹配的单一元素（通过 `id`）          |
| `document.querySelector()`          | `HTMLElement` | 返回匹配的第一个元素（通过 CSS 选择器）  |

```javascript
// 返回节点列表
const elements = document.getElementsByClassName("example"); // NodeList

// 返回单一元素
const element = document.getElementById("unique"); // HTMLElement

// 返回节点列表
const allDivs = document.querySelectorAll("div"); // NodeList
```

## 总结
除了 id选择器的唯一性和 querySelector()返回的是单一节点，其他方法返回的都是节点列表