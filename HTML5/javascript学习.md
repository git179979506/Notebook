### [bootstrap](http://www.bootcss.com)

> 全栈型的前端框架

### 什么是JavaScript

* 由Netspace公司设计，当时跟Sun公司合作，所以名字起得像Java
* 简称JS

### JS的常见用途

* HTML DOM操作（节点操作：添加、修改、删除节点）
* 给HTML网页增加动态功能，比如动画
* 事件处理：比如监听鼠标点击、鼠标滑动、键盘输入

### Node.js

* Node是一个JavaScript运行环境\(run time\)，是对Google V8引擎进行了封装
* V8引擎执行JavaScript的速度非常快，性能非常好

### Node.js的优势

* 可以作为后代语言
* 单线程

  * 不新增额外线程的情况下，依然可以对任务进行并行处理（采用事件轮询）

* 非阻塞I\/O、V8虚拟机、事件驱动


> Node.js开发指南、JavaScript权威指南

### JavaScript的书写方式

* 页内JS：在当前网页的script标签中编写

  ```
  <script type="text/javascript">
  </script>
  ```

* 外部JS

  ```
  <script src="index.js"></script>
  ```


### JS的常用语法

```js
// 1.基本语法
var age = 18; // number
var money = 100.8; // number
var name = 'jack'; // string
    name2 = 'rose'; 
var result = ture; // false boolean
var number = null; // object
var number2 = undefined; // undefined

// 2.输出
console.log(age, money, name, result, number);

// 3.变量的真实类型 typeof
console.log(typeof age, typeof money, typeof name, typeof result, typeof number);

// 4.基本数据类型的运算
// 4.1 字符串的拼接
var newName = name + '-' + name2;
console.log(newName);

// 4.2 字符串与数字拼接
var str1 = 10 + 10 + '10'; // 2010
var str2 = '10' + 10 + 10; // 101010
var str3 = (10 + '10') + 10; // 101010
console.log(str1, str2, str3);

// 遵循规律：
// - 运算是从左到右
// - 任何类型的变量与string类型的变量拼接就会被强转为string

// 5.数组
var numbers = [-10, ‘san’, name, result, number, ['haha', '呵呵']];

// 5.1 遍历数组
for(var i=0; i<numbers.length, i++) {
    console.log(numbers[i]);
}

for(var i in numbers) {
    // i为下标
    console.log(i, numbers[i]);
}

// 5.2 数组常用的属性
// 删除数组中最后一个内容，出栈
numbers.pop();

// 插入
numbers.push('插入');

// 6.JS常用类库 Math
var numsArr = [10, 22, 33, 44, 11];
var maxNum = Math.max(210, 22, 2);
console.log(maxNum);

var minNum = Math.min.apply(this, numsArr);
console.log(minNum);
```

### JS中常见函数定义、调用

```js
// 1.1 加法运算（两个数）
// 定义
function sum(num1, num2) {
    return num1 + num2;
}

// 调用
var result = sum(12, 323);
console.log(result);

// 1.2 万能的加法函数
function sum2(numbersArray) {
    var result = 0;

    for (var i in numbersArray) {
        result += numbersArray[i];
    }

    return result;
}

// 1.3 匿名函数
// 定义
var res = function () {
    console.log('我是匿名函数');
}

// 调用
res();
```

### JS中创建对象

```js
// 1.创建对象
var dog = {}；
console.log(typeof dog);

// 2.对象的属性和行为
var dog2 = { // object
    name: 'dahuang',
    age: 18,
    height: 1.55,
    dogFriends: ['wangcai', 'wangcai2'],
    eat: function () {
    // 通过this拿到当前对象，this所在的函数在哪个对象就代表哪个对象
        console.log(this.name + '吃'); 
    },
    run: function (where) {
        console.log(this.name + '跑' + where);
    }
};

console.log(dog.age, dog.name);
dog.eat();
dog.run('草地');

// 3.批量创建对象（构造函数）
// 普通函数
var Dog0 = function () {
    console.log('这是一个普通的函数');
}
Dog0();

// 构造函数（OC中的类）
var Dog = function () {
    this.name = null;
    this.age = null;
    this.dogFriends = [];
    this.height = null;
    this.eat = function (something) {
        console.log(this.name + '吃' + something);
    };
    this.run = function (where) {
        console.log(this.name + '跑' + where);
    }
}

var dog1 = new Dog();
dog1.name = '阿黄';
dog1.age = 15;
dog1.dogFriends = ['dog1', 'dog2'];

var dog2 = new Dog();
dog2.name = '旺财';
dog2.age = 1;
dog2.dogFriends = ['dog1', 'dog2'];

console.log(dog1, dog2);

// 带参数
var Dog1 = function (name, age) {
 this.name = name;
 this.age = age;
 this.eat = function (something) {
 console.log(this.name + '吃' + something);
 };
 this.run = function (where) {
 console.log(this.name + '跑' + where);
 }
}

var dog3 = new Dog1('旺财1', 2);
```

### JS中的两大内置对象
####window
```js
// 1.第一大作用:
// 1.1 所用的全局变量都是window的属性
var age = 17;
console.log(age);
console.log(window.age);

// 1.2 所有的全局函数都是window的方法
function Dog () {
    console.log(‘这是一条可爱的狗’);
}
Dog();
window.Dog();
window.alert('哈哈');
window.console.log('全局的');

// 练习
function Person {
    console.log(this);
}

Person(); // this --> window
new Persion(); // this --> Person

// 2.第二大作用
// 2.1  动态的跳转(协议拦截)
window.location.href = 'http://www.baidu.com';
window.location.href = 'app://openCamera?user=zhangsan';
```

####document(DOM操作)
```js
// 作用
// 1.可以动态获取网页中所有的标签（节点）
// 2.可以对获取到的标签进行CRUD

document.write('你好，世界');
document.write('<input type="file">');

// 常用操作 index.js
function changeImg () {
    // 1.获取网页中的图像标签
    var img = document.getElementByClassName('icon')[0];
    // 改变src属性
    img.src = 'image/img_02';
}

// 这样的情况就需要把script标签放在body的尾部 index2.js
var img = document.getElementByClassName('icon')[0];
var p = document.getElementById('word');
var btn = document.getElementByTagName('button')[0];
btn.onclick = function () {
    if (btn.innerText == '隐藏') {
        // 隐藏 css属性 style display
        p.style.display = 'none';
        icon.style.display = 'none';
        btn.innerText = '显示';
    } else {
        p.style.display = 'block';
        icon.style.display = 'inline-block';
        btn.innerText = '隐藏';
    }
}
```

```
<head>
    <script src="index.js"></script>
</head>
<body>
    <img class="icon" src="image/img_01.png" />
    <p id="word">这里风景很美</p>
    <p></p>
    <button onclick="changeImg();">更改图片</button>

    <script src="index2.js"></script>
</body>
```

###常用事件（适当的时候可以使用伪类）
```
// 页面加载完毕
window.onload = function () {
    // code...
}

// 鼠标操作 
img.onmouseover = function () {
    console.log('进入');
}
img.onmousemove = function () {
    console.log('移动');
}    
img.onmouseout = function () {
    console.log('离开');
}
```

###JS中的CRUD
```js
document.write('hello world');

var main = document.getElementById('main');
var img = document.createElement('img');
img.src = 'image/img_01.jpg';
main.appendChild(img);

img.remove();

getElementBy...

console.log(main.childNodes);
```

###JS
```js
类型比较：===
```