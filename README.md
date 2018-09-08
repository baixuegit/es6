# es6 笔记

## 一、let和const

### 1、let
- let有自己的块级作用域：

- let不允许在相同作用域内，重复声明同一个变量。

- let必须先声明再使用。



    但是声明的变量只有在let所在的代码块内有效、
    另外，for循环还有一个特别之处，就是设置循环变量的那部分是一个父作用域，而循环体内部是一个单独的子作用域。


    只要块级作用域内存在let命令，它所声明的变量就“绑定”（binding）这个区域，不再受外部的影响。
    在let声明变量前对变量进行赋值会报错（不存在变量提升）


    ES6 明确规定，如果区块中存在let和const命令，这个区块对这些命令声明的变量，从一开始就形成了封闭作用域。凡是在声明之前就使用这些变量，就会报错。

### 2. const（声明常量）

- const声明不可以被重复
- const有自己的块级作用域
- const在声明的时候必须赋值
- const的值不可以被修改


## 二、对象的简写形式

```js
let name = "bx";
let obj = {
   name:name,
   say:function(){
       console.log("hello")
   }
}

//简写,如果属性名和后面的属性值和变量名相同，可以简写如下：
let obj = {
    name
}
//方法的简写
let obj ={
    say(){
        console.log("hello);
    }
}

```
## 三、es6中的解构赋值

###     1. 对象的解构赋值

```js

    let obj={
        name:"xx",
        age:22
    } 
    // 解构前
    let name = obj.name;
    let age = obj.age;

    //解构后
    //let {对象的属性名:声明的变量名}=obj
    let {name:name,age:age}=obj;
    //只有在对象的属性名和声明的变量名一样时可以简写
    let {name,age}=obj;




```
###     2. 数组的解构赋值

```js
let arr = [1,2,3,4];
//解构前
 let num1 = arr[1];
 let num2 = arr[2];
 let num3 = arr[3];
 let num4 = arr[4];
//  解构后
let [num1,num2,num3,num4] = arr;
console.log(num1,num2,num3,num4);

```
### 3.数组解构中的rest-elemant(...剩余元素)

- 剩余项只可以有一个

- 只可以在数组中的最后出现


    注意：...(剩余元素)拿到的是一个数组，
```js
    // ...语法在es6解构中叫rest-elemant
    // 剩余元素的意思
    let arr = [1,2,3,4];
    // 需求：拿到数组中的2,3,4
    let[num1,...num2] = arr;
    console.log(num2);
    

```

## 四、箭头函数
- 如果箭头函数只有一个参数可以可以省略小阔号

- 如果箭头函数的函数体内只有条代码。可以省略花括号

- 如果箭头函数有返回值且只有一条代码，可以省略花括号和return

```js
    // es5 声明函数
    var fn = function(a,b){
        return a+b
    }

    // 箭头函数
    let fn =(a,b) => {
        return a+b
    }

    console.log(fn(2,3));


```
### 4.1 箭头函数中的this
- 在箭头函数中没有this

- 如果在箭头函数中使用this，那么就会沿着作用域往上找，找到了就是使用，
    如果一直没有最后会返回window（在node中最后会返回一个空的对象）

### 4.2 es5中的this指向问题总结
根据函数的调用模式，来判断this的指向

- 函数调用模式 this 指向 window

- 方法调用模式 this 指向 调用方法的对象

- 构造函数调用模式  this 指向 构造函数的实例

- 上下文调用模式   this 指向 call apply 的第一个参数

###4.3箭头函数中的arguments;
    作    用：      在es5 中的作用，在函数调用的时候，将所有的实参传到arguments对象中，(得到实参是伪数组)；

    使用场景：  在不可以确定实参个数的时候，需要使用arguments来获取所有的实参

    *注意在es6中没有arguments

## 五、剩余参数
注意：
- 剩余参数有只能有一个，并且只可以是列表参数的最后一个
- 剩余参数得到的是一个真数组，可以使用数组的方法

```js
//需求：传入随意参数，求出和还回
    let sun =(...arr) => {
        let result = 0;
        arr.forEach((v) =>{
            result +=v;
        })
        return result;
    }
    sun(1,2)
    sun(1,2,3)

```

## 六、函数的默认参数
 - 在es6中如果没有传入参数可以使用默认的参数
 ```js
 let fn = (a = 100 , b = 200) => {
     return a + b;
 }

 console.log(fn(50,20))
 ```

## 七、使用变量的属性名，作为对象的属性名
```js
let key = "name";
let obj = {
    [key]: "cc"
}
console.log(obj)

```

## 八、对象的扩展运算符
- 使用扩展运算符(...)，就是把一个对象的属性给当前的这个对象也来一份
- 后面写上自己的属性
```js
let parson = {
    name:"xx",
    age:18
}
var student = {...parson,say (){console.log("hello")}}

console.log(student);
student.say();
```
## 九、使用数组作为参数传递
```js
let arr = [1,2,3];
let sum = (a,b,c) => {
    return a+b+c;
}
//es5使用数组作为参数：
//let result = sum.applay(null,arr);
//console.log(result);

//在es6中 ... 在下面的场景中就相当于将数组所有元素拆解开一次传递给函数形参了！
let result = sum({...arr});
console.log(result);

```

## 十、es6中class的使用
- 值class中会自动把方法添加到构造函数的原型上
```js
class parson ={
    constructor(name,age){
        this.name = name;
        this.age  =age;
    }
    say (){
        console.log("hello")
    }
}
let p = new parson("xx",18);
p.say();

```

## 十一、静态成员和实例成员
- 成员是指：属性和方法
- 静态成员：通过构造函数本身访问到的成员
- 实例成员：通过构造函数的实例访问到的成员
```js
class parson {
    // 使用构造器给构造函数添加实例属性
    constructor(name,aga){
        this.name = name;
        this.age = age;

    }
    // 添加实例方法
    say(){
        console.log("hello")
    }
    // 添加静态成员
    static sayHi(){
        console.log("我是静态成员")
    }
}
let p = new parson("xx",18);
//调用静态成员
parson.sayHi();


```

## 十二、使用class实现继承
- 使用extends继承指定的函数
- 使用super()来继承父类的属性

```js
class parson{
    constructor(age,name){
        this.name = name;
        this.age = age;

    }
    say(){
        console.log("123")
    }
}

class student extends parson {
    constructor(name,age){
        super(name,age);
        this.stuNo= 1000

    }
    sing(){
        console.log("爱你")
    }
}
let stu = new student("xx",18);
stu.say();
stu.sing();

```
## 十三、字符串模板
- 使用反引号包裹字符串

- 需要拼接的变量需要使用${变量名}拼接

```js
let name = "baixue";
let age = 18;
//es5
var  str = "大家好我是"+name+"，我今年"+age+"岁了";
//es6
let str = `大家好我是 ${name}，我今年${age}岁了`;


```

## 十四、promise的介绍
- 使用promise主要是用来解决回调地狱的
- 1.使用别人写好的promise api   .then
     axios: 这是一个用来发送ajax请求的库 这个库支持Promise
     支持promise就意味着可以使用.then方法来使用回调函数
     .then方法有两个参数，第一个是成功的回调，第二个是失败的回调
```js
//需要引入第三方的包
    axios({
        url: "",
        data: {},
        method: "get"
    }).then(function (data) { 
        // 成功的回调函数
    })

```

- 2.自己封装Promise给别人使用
    promise方法有.then方法 可以用来传递回调函数
    - promise方法有三种状态，
        1.pending   挂起正在执行
        2.fullfilled 成功 已经执行完毕并且结果是成功的
        3. rejected: 失败 已经执行完毕并且结果是失败的
```js
//使用promise 方法的.then()方法解决回调地狱
//封装函数需要返回一个promise的实例，调用的时候可以通过.then()方法解决回调地狱
function timeout(time){
    return new promise(function(resolve,reject){
        setTimeout(function(){
               // 当异步操作完成之后，我们不需要考虑要执行什么回调函数
            // 只需要考虑改变当前Promise的状态就可以了

            // 1. resolve函数调用可以将当前promise改变为成功
            // 2. reject函数调用可以将当前promise改变为失败

            // resolve和reject函数都可以传递参数给回调函数！
            reject(123);
        })
    })
}


timeout(2000).then((data) => {
   console.log(data);
    
}).then(function(){
   console.log(data);
   return timeout(2000); 
}).then(function(data){
    console.log(data);

})
//每隔两秒打印一次


```















​    

​    




