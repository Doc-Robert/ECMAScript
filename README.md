# ECMAScript6-11



# 第一章ECMAScript介绍

## 1、ECMAScript

**ECMAScript**是一种由[Ecma国际](https://baike.baidu.com/item/Ecma国际)（前身为[欧洲计算机制造商协会](https://baike.baidu.com/item/欧洲计算机制造商协会/2052072)，European Computer Manufacturers Association）通过ECMA-262标准化的脚本[程序设计语言](https://baike.baidu.com/item/程序设计语言)。这种语言在[万维网](https://baike.baidu.com/item/万维网)上应用广泛，它往往被称为[JavaScript](https://baike.baidu.com/item/JavaScript)或[JScript](https://baike.baidu.com/item/JScript)，所以它可以理解为是JavaScript的一个标准,但实际上后两者是ECMA-262标准的实现和扩展



# 第二章ES6新特性

## 1、 let变量声明

- 变量声明 let 

  ​	特性：

  - 变量不能重复声明
  - 块级作用域生效 全局 函数 eval

  - 不存在变量提升；let 不允许 在声明他前 使用
  - 不影响作用域链



> `let练习`
>
> ```html
> <!DOCTYPE html>
> <html lang="en">
> <head>
>     <meta charset="UTF-8">
>     <meta name="viewport" content="width=device-width, initial-scale=1.0">
>     <title>let</title>
>     <style>
>         .item{
>             width: 100px;
>             height: 50px;
>             border: 1px solid pink;
>             margin: 20px;
>         }
>     </style>
> </head>
> <body>
>     <div class="container">
>         <h2 class="page-header">touch to change sytle</h2>
>         <div class="item"></div>
>         <div class="item"></div>
>         <div class="item"></div>
>     </div>
>     <script>
>         //获取元素
>       let items = document.getElementsByClassName("item")
> 
>       for(let i = 0; i<items.length;i++){
>           //切换元素style
>           items[i].onclick = function(){
>               items[i].style.background = 'pink'
>           }
>       }
> 
>       //使用var 声明变量 会使循环完成
>       // i=3 当点击div 时i=3 带入 div元素长度最大为2 使其越界 导致他找不到3 
>     </script>
> </body>
> </html>
> ```





## 2、const 变量声明

变量声明const  声明常量  ；（java final）

```js
  const LADY = 'Reines';
```

- const注意事项

  - 1.一定要在声明时赋初始值 
  - 2.一般常量使用大写
  - 3.常量的值不能修改
  - 4.块级作用域  超出显示未定义
  - 5.对于数组和对象的元素修改，不算做对常量的修改，不会报错

  ```js
  const TEAM = ["Reines","waybo","hanhan"]
  TEAM.push("solomen")
  console.log(TEAM)
  ```




## 3、变量的解构赋值

*es6允许按照一定模式从数组和对象中提取值，对变量进行赋值*

*其中被称为解构赋值*

- 对数组的解构赋值

> ```js
>         const caster = ['gray','Reines','waybo'];
>         let [g,r,w] = caster
>     
>         console.log(g);
>         console.log(r);
>         console.log(w);
> ```

- 对对象的解构赋值

> ```js
>         //对象的解构
>         const elMello ={
>             name:'Reines',
>             age:'unknown',
>             lord: function(){
>                 console.log("waybo");
>             }
>         };
> 
>         let {name, age, lord} = elMello;
>         console.log(name);
>         console.log(age);
>         console.log(lord);
> 
>     
>         lord();
> ```



## 4、模板字符串

​		es6 引入新的声明字符串的方式 **` `` `**

- 声明

```js
        //1、声明
        let str = `new String`;
        console.log(str, typeof str);
```

`tips：`

- 可以在`` 中出现换行符
- 可以进行变量拼接

```js

        //3. 变量拼接
        let name = 'waybo';
        let show = `${name} lord elmello ni sei`
        console.log(show);
```

> 结果为：
>
> ```js
>  waybo lord elmello ni sei
> ```

## 5、简化对象写法

ES6允许在大括号里，直接写入变量和函数，作为对象的属性和方法 ，熟悉更加简洁

```js
let name = "Reines";
let elMello = function(){
    console.log('lord');
}

const school = {
    name,
    elMello, //变量使用
    improve(){// 方法简写
        console.log('简便写法');
    }
}
console.log(school);
```

> console.log(school); 
>
> 打印结果

```
{name: "Reines", elMello: ƒ, improve: ƒ}
```



tips:

```js
improve(){// 方法简写
        console.log('简便写法');
    }
```

原：

```js
improve = function(){// 方法简写
        console.log('简便写法');
    }
```



## 6、箭头函数 =>

### 6.1 箭头函数的使用

ES6允许使用箭头 （=>） 定义函数

```js
let fn = () => {
    console.log('=>函数');
}
fn();
```

> - *this 是静态的   ; this 始终指向函数声明时所在作用域下的 this 的值*
>
> ```js
>         function getName(){
>             console.log(this.name);
>         }
> 
>         let getName2 = () =>{
>             console.log(this.name);
>         }
>         //设置window 对象name 属性
>         window.name = "Reines";
>         const teacher = {
>             name:'waybo'
>         };
> 
>         // call() 方法调用
>         getName.call(teacher)//waybo
>         getName2.call(teacher);//Reines
> ```
>
> 
>
> - 2.不能作为构造实例化对象
>
> ```js
>         let Person = (name,age) => {
>             this.name = name;
>             this.age = age
>         }
>         ;//构造方法找不到
> ```
>
> - 3.不能使用 arguments 变量
>
> ```js
>         let args = () =>{
>             console.log(arguments);
>         }
> 
>         args(1,2,3)
> ```
>
> Uncaught ReferenceError: arguments is not defined
>
> - 4.箭头函数简写
>
> ```js
> // 1)省略小括号 ，当形参只有一个的时候
> // 2)省略花括号。当代码体只有一句时 此时return必须省略
> let test = n => n + n;
> ```



### 6.2 箭头函数实践

```html
    <style>
        div{
            width: 200px;
            height: 200px;
            background: #0ff;
        }
    </style>
</head>
<body>
    <div id="ad"></div>
    <script>
        //获取·元素
        let ad = document.getElementById('ad')
        //事件
        ad.addEventListener('click',function(){
            // this 为静态的 会指向在声明时所在作用域下this 的值
            setTimeout(()=>{
            
                this.style.background = "pink";
            },1000)
        })
        
        //返回 数组中偶数的元素
        const arr = [1,6,4,23,100]
        
        const result = arr.filter(item => item % 2 === 0)

        console.log(result);
        //箭头函数适合 与this 无关的回调 定时器 数组的方法回调
        //不适合  与this 有关的回调 事件回调 对象的方法；
        // 因为 this 不会指向当前作用域的元素 而是指向作用域外的元素


    </script>
</body>
```



- 当定时器不使用箭头函数

```js
    ad.addEventListener('click',function(){
        // this 为静态的 会指向在声明时所在作用域下this 的值
        setTimeout(function(){
        
            this.style.background = "pink";
        },1000)
    })

//Uncaught TypeError: Cannot set property 'background' of undefined
```
> this不会指向外部作用域的元素 从而找到当前作用域元素值 





- 箭头函数适合 与this 无关的回调 定时器 数组的方法回调
- 不适合  与this 有关的回调 事件回调 对象的方法；
  因为 this 不会指向当前作用域的元素 而是指向作用域外的元素



## 7.参数默认值

es6允许给函数参数赋值初始值



- 1. 形参初始值 具有默认值参数 ，一般位置要靠后 

```js
  function add(a,b,c){
            return a + b + c;
        }
        let result = add(1,2,3);
        console.log(result);

```

**tips**:

> 当传参数时有参数未传入 ，可以给参数设置默认值

```js
  function add(a,b,c=10){
            return a + b + c;
        }
        let result = add(1,2);
        console.log(result);
```

结果为13

注意：设置默认值得参数 一般位置要靠后 否则会NaN





-  2.与解构赋值结合

```js
        function connect({host,userName,password,port=3308}){
            console.log(host);
            console.log(userName);
            console.log(password);
            console.log(port);
        }
        connect({
            host :'localhost',
            userName: 'root',
            password: 'root',
            //port: 3306
        })
```



## 8.rest 参数

es6引用rest 参数 用于获取函数的实参 ，用来代替arguments

- 在es5获取实参的方式

```
        function date(){
            console.log(arguments);
        }
        date('Reines',"waybo",'saber')
```

> 得出的结果为  一个object 的对象

- 使用rest 参数

```js
        function date2(...args){
            console.log(args);
        }
        date2('Reines',"waybo",'saber')
```

> 结果 会得出一个 数组



**tips：**

- rest 参数必须要放在最后

```js
function fn(a,b,...args){
    console.log(a);
    console.log(b);
    console.log(args);
}
fn(1,3,4,5,6,7,)
```

得出的结果为

> 1
> 3
> (4) [4, 5, 6, 7]

第一第二个值 会赋值给ab 后面的放在args 中 用作数组

、



## 9、spread 扩展运算符

扩展运算符 ... 能将 数组 转换为逗号分隔的 参数序列

```js
        //数组 
        const ccc = ['bb','moon','canser']

        function MoonCanser(){
            console.log(arguments);
        }
        MoonCanser(ccc);
```

得出一个arguments 数组

![image-20210104144339962](C:\Users\user\AppData\Roaming\Typora\typora-user-images\image-20210104144339962.png)



使用扩展运算符

> ```js
>         MoonCanser(...ccc);
> ```

转换为逗号分隔的 参数序列

![image-20210104144501938](C:\Users\user\AppData\Roaming\Typora\typora-user-images\image-20210104144501938.png)



### `应用`：

#### 1.添加数组

```js
 const upthree = ['saber','lanser','archer']
        const downthree = ['assxin','rider','caster']
        const fate = [...upthree,...downthree]
        //相当于 ['saber','lanser','archer'  , 'assxin','rider','caster']
        console.log(fate);
```

...把数组展开 放进数组

> (6) ["saber", "lanser", "archer", "assxin", "rider", "caster"]

#### 2.数组的克隆

```js
//2.数组的克隆
const special = ['ruler','avenger','mooncanser']

const clone = [...special]
console.log(clone);
```

clone 数组



#### 3.将伪数组转换为真正的数组

```html
<div></div>
<div></div>
<div></div>
<script>
    const divs = document.querySelectorAll('div');
    const divArr = [...divs]
    console.log(divArr);
</script>
```

![image-20210104153052945](ECMAScript6-11.assets/image-20210104153052945.png)

## 10、symbol 

