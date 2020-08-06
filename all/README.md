# fe-interview

[![mnt-image](https://img.shields.io/maintenance/yes/2020.svg)](../../commits/master)
[![GitHub stars](https://img.shields.io/github/stars/daily-interview/fe-interview.svg)](https://github.com/daily-interview/fe-interview/stargazers)
[![GitHub forks](https://img.shields.io/github/forks/daily-interview/fe-interview.svg)](https://github.com/daily-interview/fe-interview/network)
[![GitHub license](https://img.shields.io/badge/license-MIT-blue.svg)](https://github.com/daily-interview/fe-interview/blob/master/LICENSE)

## 所有面试题

1、  [js] [介绍一下 JS 的基本数据类型。](https://github.com/daily-interview/fe-interview/issues/1)

```
JS 7 种基本数据类型（原始类型），即 （Undefined、Null、Boolean、Number 、String） + （Symbol、BigInt）和 3种引用数据类型：对象(Object)、数组(Array)、函数(Function)。
 
基本类型值：指的是保存在栈内存中的简单数据段。

引用类型值：指的是那些保存在堆内存中的对象。变量中保存的实际上只是一个指针，这个指针指向内存堆中实际的值。

> 注：Symbol 是 ES6 引入了一种新的原始数据类型，表示独一无二的值; BigInt即是第七种基本类型，V8引擎v6.7 默认启用对 BigInt 的支持。

Symbol用法 

语法  

Symbol (value)

eg.

```
let a=Symbol ("welcome");
console.log(a); //输出 Symbol(welcome)
```

BigInt用法  

语法  

BigInt(value) || 数字后面加n;

eg.

```
let b1 = BigInt(10);
let b2 = 10n;
console.log(b1,b2); //输出 10n 10n
```
```

2、 [js] [js实现几种常见排序算法。( 手写 )](https://github.com/daily-interview/fe-interview/issues/2)


冒泡排序：

![bubbleSort.gif](https://upload-images.jianshu.io/upload_images/3100736-d38281a90f05aff1.gif?imageMogr2/auto-orient/strip)

```javascript
const arr = [3, 44, 38, 5, 47, 15, 36, 26, 27, 2, 46, 4, 19, 50, 48];

function bubbleSort(arr) {
    let len = arr.length;
    if(len >= 1) {
        for(let i = 0;i < len - 1; i++) {
            for(let j = 0;j < len - 1 - i; j++) {
                if(arr[j] > arr[j + 1]) {
                    let temp = arr[j + 1];
                    arr[j + 1] = arr[j];
                    arr[j] = temp;
                }
            }
        }

    }
    return arr;
}

console.log(bubbleSort(arr));
```

冒泡排序优化版： 

```javascript
const arr = [3, 44, 38, 5, 47, 15, 36, 26, 27, 2, 46, 4, 19, 50, 48];

function bubbleSort(arr) {
    let len = arr.length;
    let lastExchangeIndex = 0;
    //无序数列的边界，每次比较只需要比到这里为止
    let sortBorder = len - 1;
    if(len >= 1) {
        for(let i = 0;i < len; i++) {
            //有序标记，每一轮的初始是true
            let isSorted = true;
            for(let j = 0;j < sortBorder - i; j++) {
                if(arr[j] > arr[j + 1]) {
                    let temp = arr[j + 1];
                    arr[j + 1] = arr[j];
                    arr[j] = temp;
                    //有元素交换，所以不是有序，标记变为false
                    isSorted = false;
                    //把无序数列的边界更新为最后一次交换元素的位置
                    lastExchangeIndex = j;
                }
            }
            sortBorder = lastExchangeIndex;
            if(isSorted) { //有序,跳出循环
                break;
            }
        }

    }
    return arr;
}

console.log(bubbleSort(arr));
```

选择排序：

![selectSort.gif](https://upload-images.jianshu.io/upload_images/3100736-6bb5d8693bc99a16.gif?imageMogr2/auto-orient/strip)

```javacript
const arr=[3,44,38,5,47,15,36,26,27,2,46,4,19,50,48];

function selectionSort(arr) { 
    let len = arr.length;
    let minIndex, temp;
    for (let i = 0; i < len - 1; i++) {
        minIndex = i;
        for (let j = i + 1; j < len; j++) {
            if (arr[j] < arr[minIndex]) { 
                // 寻找最小的数
                minIndex = j; 
                // 将最小数的索引保存
            }
        }
        temp = arr[i]; 
        arr[i] = arr[minIndex];
        arr[minIndex] = temp; 
    } 
    return arr;
}

console.log(selectionSort(arr));
```

选择排序优化版：

```javascript
const arr = [3, 44, 38, 5, 47, 15, 36, 26, 27, 2, 46, 4, 19, 50, 48];

function selectionSort(arr) { 
    let len = arr.length;
    let left = 0;
    let right = len - 1;
    while (left < right) {
        let max = left;//记录无序区最大元素下标
        let min = left;//记录无序区最小元素下标
        let j = 0;
        for (j = left + 1; j <= right; j++) {
            //找最大元素下标
            if (arr[j] < arr[min])
            {
                min = j;
            }
            //找最小元素下标
            if (arr[j] > arr[max])
            {
                max = j;
            }
        }
        //最小值如果是第一个则没有必要交换
        if (min != left) {
            let tmp = arr[left];
            arr[left] = arr[min];
            arr[min] = tmp;
        }
        //这里很重要，如果最大元素下标是left,前面已经和最小元素交换了，此时最大元素下标应该是min
        if (max == left) {
            max = min;
        }
        //最大值如果是最后一个则没必要交换
        if (max != right) {
            let tmp = arr[right];
            arr[right] = arr[max];
            arr[max] = tmp;
        }
        left++;
        right--;
    }
	return arr;
}

console.log(selectionSort(arr));
```

插入排序：

![insertSort.gif](https://upload-images.jianshu.io/upload_images/3100736-551606266d9282a5.gif)

```javacript
const arr=[3,44,38,5,47,15,36,26,27,2,46,4,19,50,48];

function insertSort(arr) {
    const len = arr.length;
    let preIndex, current;
    for (let i = 1; i < len; i++) {
        preIndex = i - 1;
        current = arr[i];
        while (preIndex >= 0 && arr[preIndex] > current) {
            arr[preIndex + 1] = arr[preIndex];
            preIndex--;
        }
        arr[preIndex + 1] = current;
    }
    return arr;
}

console.log(insertSort(arr));
```

3、 [css] [有哪几种常用的清除浮动方法？](https://github.com/daily-interview/fe-interview/issues/3)

- 父级元素添加伪元素
```css
.clear-float:after {
    content: '';
    display: block;
    clear: both;
}
```
- 在与浮动元素平级的最后面添加新元素 div.clear
```css
.clear {
    clear: both;
}
```
- 在父级元素添加样式 overflow: auto; 或者 overflow: hidden; 会存在兼容性问题。

4、 [js] [Object.assign 是浅拷贝还是深拷贝？实现深拷贝的方法有哪些？](https://github.com/daily-interview/fe-interview/issues/4)

>  Object.assign() 方法用于将所有可枚举属性的值从一个或多个源对象复制到目标对象。它将返回目标对象。

- 如果目标对象中的属性具有相同的键，则属性将被源对象中的属性覆盖。后面的源对象的属性将类似地覆盖前面的源对象的属性。

- Object.assign 方法只会拷贝源对象自身的并且可枚举的属性到目标对象。该方法使用源对象的[[Get]]和目标对象的[[Set]]，所以它会调用相关 getter 和 setter。因此，它分配属性，而不仅仅是复制或定义新的属性。如果合并源包含getter，这可能使其不适合将新属性合并到原型中。为了将属性定义（包括其可枚举性）复制到原型，应使用Object.getOwnPropertyDescriptor()和Object.defineProperty() 。

- String类型和 Symbol 类型的属性都会被拷贝。

- 在出现错误的情况下，例如，如果属性不可写，会引发TypeError，如果在引发错误之前添加了任何属性，则可以更改target对象。

- Object.assign 不会在那些source对象值为 `null `或 `undefined` 的时候抛出错误。

- 针对**深拷贝**，需要使用其他办法，因为 Object.assign()拷贝的是属性值。假如源对象的属性值是一个对象的引用，那么它也只指向那个引用。也就是说，如果对象的属性值为简单类型（如string， number），通过Object.assign({},srcObj);得到的新对象为`深拷贝`；如果属性值为对象或其它引用类型，那对于这个对象而言其实是`浅拷贝`的。

## 深拷贝的几种实现方法

### JSON.stringify 和 JSON.parse

>用 JSON.stringify 把对象转换成字符串，再用 JSON.parse 把字符串转换成新的对象。

可以转成 JSON 格式的对象才能使用这种方法，如果对象中包含 function 或 RegExp 这些就不能用这种方法了。

```
//通过js的内置对象JSON来进行数组对象的深拷贝
function deepClone(obj) {
  let _obj = JSON.stringify(obj);
  let objClone = JSON.parse(_obj);
  return objClone;
}
```

### Object.assign()拷贝

当对象中只有一级属性，没有二级属性的时候，此方法为深拷贝，但是对象中有对象的时候，此方法，在二级属性以后就是浅拷贝。

### 通过jQuery的extend方法实现深拷贝

```
let $ = require('jquery');
let obj1 = {
   a: 1,
   b: {
     f: {
       g: 1
     }
   },
   c: [1, 2, 3]
};
let obj2 = $.extend(true, {}, obj1);
```

### lodash.cloneDeep()实现深拷贝

```
let _ = require('lodash');
let obj1 = {
    a: 1,
    b: { f: { g: 1 } },
    c: [1, 2, 3]
};
let obj2 = _.cloneDeep(obj1);
```

### 使用递归的方式实现深拷贝

```
function _deepClone(source) {
  let target;
  if (typeof source === 'object') {
    target = Array.isArray(source) ? [] : {}
    for (let key in source) {
      if (source.hasOwnProperty(key)) {
        if (typeof source[key] !== 'object') {
          target[key] = source[key]
        } else {
          target[key] = _deepClone(source[key])
        }
      }
    }
  } else {
    target = source
  }
  return target
}
```

5、 [js] [promise和setTimeout执行顺序是怎样的？](https://github.com/daily-interview/fe-interview/issues/5)

写出下列程序运行结果并做出解释：

```javascript
setTimeout(function(){
    console.log(1);
},0); 

new Promise(function(resolve) { 
    console.log(2) 
    for(let i=0; i<10000 ; i++ ) { 
        i==9999 && resolve(); 
    } 
    console.log(3) 
}).then(function(){ 
    console.log(4) 
}); 
console.log(5); 
```

这个就涉及到**事件循环（Event Loop）**
> JS运行时，对代码执行顺序的一个算法（任务调度算法）

JS 分类：同步任务和异步任务
JS 的执行机制：
- 首先判断JS代码是同步还是异步，同步就进入主线程，异步就进入 event table
- 异步任务在 event table 中注册函数，当满足触发条件后，被推入event queue
- 同步任务进入主线程后一直执行，直到主线程空闲时，才回去 event queue 中查看是否有可执行的异步任务，如果有就推入主线程

event loop 里有维护两个不同的异步任务队列
- macro Tasks（宏任务）：script（整体代码）, setTimeout, setInterval, setImmediate, I/O, UI rendering
- micro Tasks（微任务）：process.nextTick, Promise（浏览器实现的原生Promise）, Object.observe,  MutationObserver, MessageChannel

每次执行一段代码（一个script标签）都是一个 macroTask
执行流程：
- event loop 开始
- 从macro Tasks 队列抽取一个任务，执行
- micro Tasks 清空队列执行，若有任务不可执行，推入下一轮 micro Tasks
- 结束 event loop

浏览器执行代码的过程如下整个流程
![image](https://user-images.githubusercontent.com/18480722/60965123-9f2c5900-a347-11e9-81d5-e93ec6c60840.png)

那么回到题目上去，就是
```js
setTimeout(function(){
    console.log(1);    // 1-放入宏任务队列，7-执行下一轮事件循环，宏任务输出1
},0); 

new Promise(function(resolve) { 
    console.log(2);    // 2-同步输出 2
    for(let i=0; i<10000 ; i++ ) { 
        i==9999 && resolve(); 
    } 
    console.log(3);    // 4-同步输出 3
}).then(function(){ 
    console.log(4);    // 3-放入微任务队列，6-回到微任务队列，执行剩余的微任务，输出4
}); 
console.log(5);    // 5-同步输出 5
```

6、 [ts] [说一说Typescript中的泛型的作用及使用场景。](https://github.com/daily-interview/fe-interview/issues/6)

## 什么是TypeScript

> TypeScript是由Microsoft Corporation开发和维护的面向对象的编程语言。它是JavaScript的超集，包含所有元素。

> TypeScript完全遵循OOPS概念，在TSC（TypeScript编译器）的帮助下，我们可以将Typescript代码（.ts文件）转换为JavaScript（.js文件）。

## 为什么要使用TypeScript

> TypeScript的设计目的应该是解决JavaScript的“痛点”：弱类型和没有命名空间，导致很难模块化，不适合开发大型程序。另外它还提供了一些语法糖来帮助大家更方便地实践面向对象的编程。

- TypeScript简化了JavaScript代码，使其更易于阅读和调试。

- TypeScript是开源的。

- TypeScript为JavaScript IDE和实践提供了高效的开发工具，例如静态检查。

- 使用TypeScript，我们可以比普通的JavaScript做出巨大的改进。

- TypeScript为我们提供了ES6（ECMAScript 6）的所有优点，以及更高的工作效率。

- TypeScript可以帮助我们避免开发人员通过类型检查代码编写JavaScript时经常遇到的痛苦错误。

- 强大的类型系统，包括泛型。

- TypeScript代码可以按照ES5和ES6标准进行编译，以支持最新的浏览器。

- 支持静态类型。

- TypeScript将节省开发人员的时间。

## 什么是泛型

泛型的本质是参数化类型，通俗的将就是所操作的数据类型被指定为一个参数，这种参数类型可以用在类、接口和方法的创建中，分别成为泛型类，泛型接口、泛型方法。

> TypeScript中的泛型跟java中的泛型基本类似。

## 为什么使用泛型

TypeScript 中不建议使用 any 类型，不能保证类型安全，调试时缺乏完整的信息。

TypeScript可以使用泛型来创建`可重用`的组件。支持当前数据类型，同时也能支持未来的数据类型。扩展灵活。可以在编译时发现你的类型错误，从而保证了类型安全。

## 泛型的使用

使用泛型可以创建泛型函数、泛型接口，泛型类

1.使用泛型变量

```
// 泛型变量的使用
function identity<T>(arg:T):T{
    console.log(typeof arg);
    return arg;
}
let output1=identity<string>('myString');
let output2=identity('myString');
let output3:number=identity<number>(100);
let output4:number=identity(200);
```

```
// 使用集合的泛型
function loggingIdentity<T>(arg:Array<T>):Array<T>{
    console.log(arg.length);
    return arg;
}
loggingIdentity([1,2,3]);
```

2.定义泛型函数

```
// 泛型函数
function identity<T>(arg:T):T{
    return arg;
}
let myIdentity:{<T>(arg:T):T}=identity;
```

3.定义泛型接口

```
// 泛型接口
interface GenericIdentityFn<T> {
    (arg: T): T;
}
function identity<T>(arg: T): T {
    return arg;
}
let myIdentity: GenericIdentityFn<number> = identity;
```

4.定义泛型类

```
// 泛型类
class GenericNumber<T>{
    zeroValue:T;
    add:(x:T,y:T)=>T;
}
let myGenericNumber=new GenericNumber<number>();
myGenericNumber.zeroValue=0;
myGenericNumber.add=function(x,y){return x+y;};
console.info(myGenericNumber.add(2,5));
let stringNumberic=new GenericNumber<string>();
stringNumberic.zeroValue='abc';
stringNumberic.add=function(x,y){return `${x}--${y}`};
console.info(stringNumberic.add('张三丰','诸葛亮'));
```

7、 [http] [说说你对http和https的理解](https://github.com/daily-interview/fe-interview/issues/7)

## 什么是HTTP?

> 超文本传输协议，是一个基于请求与响应，无状态的，应用层的协议，常基于TCP/IP协议传输数据，互联网上应用最为广泛的一种网络协议,所有的WWW文件都必须遵守这个标准。设计HTTP的初衷是为了提供一种发布和接收HTML页面的方法。

## 什么是HTTPS？

> HTTPS是一种通过计算机网络进行安全通信的传输协议，经由HTTP进行通信，利用SSL/TLS建立全信道，加密数据包。HTTPS使用的主要目的是提供对网站服务器的身份认证，同时保护交换数据的隐私与完整性。

PS:TLS是传输层加密协议，前身是SSL协议，由网景公司1995年发布，有时候两者不区分。

## 什么是TLS/SSL？

> TLS/SSL全称安全传输层协议Transport Layer Security, 是介于TCP和HTTP之间的一层安全协议，不影响原有的TCP协议和HTTP协议，所以使用HTTPS基本上不需要对HTTP页面进行太多的改造。

SSL有三种不同类型，需要了解下：

- 扩展验证型(EV)SSL证书，适用于大企业，像银行，证券网站都会使用这个证书，信任等级，安全等级是最高的。

- 组织验证型(OV)SSL证书，适用于企业网站，需要验证企业身份，安全等级比DV高些

- 域名验证型（DV）SSL证书 ，适用于个人网站，一般验证下网站信息就可以通过，很多免费版本

## 如果获取SSL证书？

一般分为三种价位的：贵的，便宜的，免费的

- 贵的（上千甚至上万的价）：Symantec、globalsign、comodo、geotrust，除非大企业需要，中小企业网站没必要购买

- 便宜的（大概50美元上下）：godday，RapaidSSL，Comodo positiveSSL

- 免费的：Let's Encrypt（比较推荐），Wosign，GlobeSSL

## HTTP特点

- 支持客户/服务器模式。（C/S模式）

- 简单快速：客户向服务器请求服务时，只需传送请求方法和路径。请求方法常用的有GET、HEAD、POST。每种方法规定了客户与服务器联系的类型不同。由于HTTP协议简单，使得HTTP服务器的程序规模小，因而通信速度很快。

- 灵活：HTTP允许传输任意类型的数据对象。正在传输的类型由Content-Type加以标记。

- 无连接：无连接的含义是限制每次连接只处理一个请求。服务器处理完客户的请求，并收到客户的应答后，即断开连接。采用这种方式可以节省传输时间。

- 无状态：HTTP协议是无状态协议。无状态是指协议对于事务处理没有记忆能力。缺少状态意味着如果后续处理需要前面的信息，则它必须重传，这样可能导致每次连接传送的数据量增大。另一方面，在服务器不需要先前信息时它的应答就较快

## HTTPS特点

- 内容加密：采用混合加密技术，中间者无法直接查看明文内容

- 验证身份：通过证书认证客户端访问的是自己的服务器

- 保护数据完整性：防止传输的内容被中间人冒充或者篡改

## HTTPS和HTTP的区别主要如下：

- HTTP 的URL 以http:// 开头，而HTTPS 的URL 以https:// 开头

- HTTP 是不安全的，而 HTTPS 是安全的

- HTTP 标准端口是80 ，而 HTTPS 的标准端口是443

- HTTP 无法加密，而HTTPS 对传输的数据进行加密

- HTTP无需证书，而HTTPS 需要CA机构(如Wosign)的颁发的SSL证书

## 总结

> HTTP + 加密 + 认证 + 完整性保护 = HTTPS

8、 [js] [说说你对 Promise 的理解](https://github.com/daily-interview/fe-interview/issues/8)

## Promise 核心

- Promise 概括来说是对异步的执行结果的描述对象。（这句话的理解很重要）
- Promise 规范中规定了，promise 的状态只有3种：
    - pending
    - fulfilled
    - rejected                          
    Promise 的状态一旦改变则不会再改变。
- Promise 规范中还规定了 Promise 中必须有 then 方法，这个方法也是实现异步的链式操作的基本。

## ES6 Promise细节

- Promise 构造器中必须传入函数，否则会抛出错误。(没有执行器还怎么做异步操作。。。)
- Promise.prototype上的 catch(onrejected) 方法是 then(null,onrejected) 的别名,并且会处理链之前的任何的reject。
- Promise.prototype 上的 then和 catch 方法总会返回一个全新的 Promise 对象。
- 如果传入构造器的函数中抛出了错误,该 promise 对象的[[PromiseStatus]]会赋值为 rejected，并且[[PromiseValue]]赋值为 Error 对象。
- then 中的回调如果抛出错误，返回的 promise 对象的[[PromiseStatus]]会赋值为 rejected，并且[[PromiseValue]]赋值为 Error 对象。
- then 中的回调返回值会影响 then 返回的 promise 对象。

## Promise优点

- Promise最大的好处是在异步执行的流程中，把执行代码和处理结果的代码清晰地分离了。

![promise.gif](https://www.liaoxuefeng.com/files/attachments/1027242914217888/l)

- 解决回调地狱（Callback Hell）问题 

Promise还可以做更多的事情，比如，有若干个异步任务，需要先做任务1，如果成功后再做任务2，任何任务失败则不再继续并执行错误处理函数。

要串行执行这样的异步任务，不用Promise需要写一层一层的嵌套代码。有了Promise，我们只需要简单地写：

```
job1.then(job2).then(job3).catch(handleError);
```

> 其中，job1、job2和job3都是Promise对象。

- Promise.all()并行执行异步任务

- Promise.race()获得先返回的结果即可

>eg.同时向两个URL读取用户的个人信息，只需要获得先返回的结果即可。

## Promise如何解决这两个问题

- 解决可读性的问题

这一点不用多说，用过Promise的人很容易明白。Promise的应用相当于给了你一张可以把解题思路清晰记录下来的草稿纸，你不在需要用脑子去记忆执行顺序。

- 解决信任问题

Promise并没有取消控制反转，而是把反转出去的控制再反转一次，也就是反转了控制反转。

这种机制有点像事件的触发。它与普通的回调的方式的区别在于，普通的方式，回调成功之后的操作直接写在了回调函数里面，而这些操作的调用由第三方控制。在Promise的方式中，回调只负责成功之后的通知，而回调成功之后的操作放在了then的回调里面，由Promise精确控制。

Promise有这些特征：只能决议一次，决议值只能有一个，决议之后无法改变。任何then中的回调也只会被调用一次。Promise的特征保证了Promise可以解决信任问题。

对于回调过早的问题，由于Promise只能是异步的，所以不会出现异步的同步调用。即便是在决议之前的错误，也是异步的，并不是会产生同步（调用过早）的困扰。
```
let a = new Promise((resolve, reject) => {
  let b = 1 + c;  // ReferenceError: c is not defined，错误会在下面的a打印出来之后报出。
  resolve(true);
})
console.log(1, a);
a.then(res => {
  console.log(2, res);
})
.catch(err => {
  console.log(err);
})
```
对于回调过晚或没有调用的问题，Promise本身不会回调过晚，只要决议了，它就会按照规定运行。至于服务器或者网络的问题，并不是Promise能解决的，一般这种情况会使用Promise的竞态APIPromise.race加一个超时的时间：
```
function timeoutPromise(delay) {
  return new Promise(function(resolve, reject) {
    setTimeout(function() {
      reject("Timeout!");
    }, delay);
  });
}

Promise.race([doSomething(), timeoutPromise(3000)])
.then(...)
.catch(...);
```
对于回调次数太少或太多的问题，由于Promise只能被决议一次，且决议之后无法改变，所以，即便是多次回调，也不会影响结果，决议之后的调用都会被忽略。


9、 [js] [说一下对bind，call，apply三个函数的认识，自己实现一下bind方法](https://github.com/daily-interview/fe-interview/issues/9)

粗略讲一下，希望大佬们能补充下。

首先这三个方法都是用来改变函数的 this 的绑定（指向）的。
它们的用法如下：
```js
func.apply(thisArg, [argsArray])

fun.call(thisArg, arg1, arg2, ...)

function.bind(thisArg[, arg1[, arg2[, ...]]])
```

区别：
- call 和 apply 的区别在于传参的形式不一样，apply 的参数形式是数组或类数组对象，call 的参数形式则是一个个排列的参数值；

- bind 返回的是原函数的拷贝，并拥有指定的 this 值和初始参数；而 call 和 apply 都是直接返回原函数的返回值，或 undefined；即 bind 是需要手动去调用的，而 apply 和 call 都是立即自动执行。

实现 bind 方法可以参考 [MDN bind polyfill](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Function/bind#Compatibility)

或者

```js
const bind = (fn, context, ...boundArgs) => (...args) => fn.apply(context, [...boundArgs, ...args]);
```


10、 [css] [说说对 BFC（Block formatting contexts） 的理解](https://github.com/daily-interview/fe-interview/issues/10)

## BFC是什么？

- BFC（Block Formatting Context）即“块级格式化上下文”

- IFC（Inline Formatting Context）即“行内格式化上下文”

- BFC是W3C CSS 2.1 规范中的一个概念，它决定了元素如何对其内容进行定位，以及与其他元素的关系和相互作用。当涉及到可视化布局的时候，Block Formatting Context提供了一个独立的渲染区域（作用范围或者盒子），HTML元素在这个独立的渲染区域中按照一定规则进行布局。并且与这个渲染区域外部毫不相干。

## 如何产生BFC

- 浮动元素：float 除 none 以外的值。
- 绝对定位元素：position (absolute、fixed)。
- display 为 inline-block、table-cells、flex。
- overflow 除了 visible 以外的值。


11、 [js] [什么是函数节流和函数防抖？应用场景是怎么样的？](https://github.com/daily-interview/fe-interview/issues/11)

## 防抖debounce

防抖(Debounce):  多次触发，只在最后一次触发时，执行目标函数。

函数防抖就是，延迟一段时间再执行函数，如果这段时间内又触发了该函数，则延迟重新计算。

### 应用场景

（1）通过监听某些事件完成对应的需求，比如：

- 通过监听 scroll 事件，检测滚动位置，根据滚动位置显示返回顶部按钮
- 通过监听 resize 事件，对某些自适应页面调整DOM的渲染（通过CSS实现的自适应不再此范围内）
- 通过监听 keyup 事件，监听文字输入并调用接口进行模糊匹配

（2）其他场景

- 表单组件输入内容验证
- 防止多次点击导致表单多次提交
- search模糊搜索，用户在不断输入值时，用防抖来节约请求资源
......

### 简单实现
```
function debounce(fn, wait) {
  let t;
  return () => {
    let context = this;
    let args = arguments;
    if (t) clearTimeout(t);
    t= setTimeout(() => {
        fn.apply(context, args);
    }, wait)
  }
}
```
### 完整实现

```
function debounce(func, wait, immediate) {
    let time;
    let debounced = function() {
        let context = this;
        if(time) clearTimeout(time);

        if(immediate) {
            let callNow = !time;
            if(callNow) func.apply(context, arguments);
            time = setTimeout(
                ()=>{time = null} //见注解
            , wait)
        } else {
            time = setTimeout(
                ()=>{func.apply(context, arguments)}
            , wait) 
        }
    };

    debounced.cancel = function() {
        clearTimeout(time);
        time = null;
    };
    return debounced;
}
```

// underscore.js debounce

```
//
// Returns a function, that, as long as it continues to be invoked, will not
// be triggered. The function will be called after it stops being called for
// N milliseconds. If `immediate` is passed, trigger the function on the
// leading edge, instead of the trailing.

_.debounce = function(func, wait, immediate) {
  var timeout, args, context, timestamp, result;

  // 处理时间
  var later = function() {
    var last = _.now() - timestamp;

    if (last < wait && last >= 0) {
      timeout = setTimeout(later, wait - last); // 10ms 6ms 4ms
    } else {
      timeout = null;
      if (!immediate) {
        result = func.apply(context, args);
        if (!timeout) context = args = null;
      }
    }
  };
```

## 节流 throttle

节流(Throttle)：函数间隔一段时间后才能再触发，避免某些函数触发频率过高，比如滚动条滚动事件触发的函数。

### 应用场景

- 鼠标不断点击触发，mousedown(单位时间内只触发一次)
- 监听滚动事件，比如是否滑到底部自动加载更多

```
### 简单实现
function throttle (fn, wait, mustRun) {
  let start = new Date()
  let timeout
  return () => {
    // 在返回的函数内部保留上下文和参数
    let context = this;
    let args = arguments;
    let current = new Date();

    clearTimeout(timeout);

    let remaining = current - start;
    // 达到了指定触发时间，触发该函数
    if (remaining > mustRun) {
      fn.apply(context, args);
      start = current;
    } else {
      // 否则wait时间后触发，闭包保留一个timeout实例
      timeout = setTimeout(fn, wait);
    }
  }
}
```
### 完整实现

```
function throttle(func, wait, options) {
    let time, context, args, result;
    let previous = 0;
    if (!options) options = {};

    let later = function () {
        previous = options.leading === false ? 0 : new Date().getTime();
        time = null;
        func.apply(context, args);
        if (!time) context = args = null;
    };

    let throttled = function () {
        let now = new Date().getTime();
        if (!previous && options.leading === false) previous = now;
        let remaining = wait - (now - previous);
        context = this;
        args = arguments;
        if (remaining <= 0 || remaining > wait) {
            if (time) {
                clearTimeout(time);
                time = null;
            }
            previous = now;
            func.apply(context, args);
            if (!time) context = args = null;
        } else if (!time && options.trailing !== false) {
            time = setTimeout(later, remaining);
        }
    };
    return throttled;
}
```

// underscore.js throttle

```
// Returns a function, that, when invoked, will only be triggered at most once
// during a given window of time. Normally, the throttled function will run
// as much as it can, without ever going more than once per `wait` duration;
// but if you'd like to disable the execution on the leading edge, pass
// `{leading: false}`. To disable execution on the trailing edge, ditto.

_.throttle = function(func, wait, options) {
  var context, args, result;
  var timeout = null;
  var previous = 0;
  if (!options) options = {};
  var later = function() {
    previous = options.leading === false ? 0 : _.now();
    timeout = null;
    result = func.apply(context, args);
    if (!timeout) context = args = null;
  };
  return function() {
    var now = _.now();
    if (!previous && options.leading === false) previous = now;
    var remaining = wait - (now - previous);
    context = this;
    args = arguments;
    if (remaining <= 0 || remaining > wait) {
      if (timeout) {
        clearTimeout(timeout);
        timeout = null;
      }
      previous = now;
      result = func.apply(context, args);
      if (!timeout) context = args = null;
    } else if (!timeout && options.trailing !== false) {
      timeout = setTimeout(later, remaining);
    }
    return result;
  };
};
```

[详情见我的简书-js防抖函数、节流函数实现, 以及在react项目中的使用](https://www.jianshu.com/p/38be6513992f)


12、 [css] [css中position属性值有哪些？各有什么特点。](https://github.com/daily-interview/fe-interview/issues/12)

 position 属性介绍

（1）position 属性自 CSS2 起就有了，该属性规定元素的定位类型。所有主流浏览器都支持 position 属性。

（2）position 的可选值有四个：static、relative、absolute、fixed。下面分别进行介绍。（其实还有个 inherit，不过这个是 IE 特有的，这里就不做讨论）

## static

<h3 id="position: static（默认值）"> position: static（默认值）</h3>

1，基本介绍
（1）static 是默认值。表示没有定位，或者说不算具有定位属性。
（2）如果元素 position 属性值为 static（或者未设 position 属性），该元素出现在正常的流中（忽略 top, bottom, left, right 或者 z-index 声明）。

2，使用样例

css: 
```
<style>
  div {
    width: 200px;
    height: 100px;
    background-color: #C9FFFF;
  }
</style>
```
html: 
```
<div></div>
<input type="text"/>
````

我们不设置元素的 postion 属性值，那么默认的显示效果如下：

[点我预览](https://artdong.github.io/blog/2018/07/23/css-position)

## relative 

1，基本介绍

（1）relative 生成相对定位的元素，相对于其正常位置进行定位。
（2）相对定位完成的过程如下：

    首先按默认方式（static）生成一个元素(并且元素像层一样浮动了起来)。
    然后相对于以前的位置移动，移动的方向和幅度由 left、right、top、bottom 属性确定，偏移前的位置保留不动。


2，样例代码

下面代码将文本输入框 position 设置为 relative（相对定位），并且相对于默认的位置向右、向上分别移动 15 个像素。

css:
```
  div {
    width: 200px;
    height: 100px;
    background-color: #C9FFFF;
  }
   
  input {
    position: relative;
    left: 15px;
    top: -15px;
  }
```
 html:
 ```
<div></div>
<input type="text" />
```

运行效果如下：

[点我预览](https://artdong.github.io/blog/2018/07/23/css-position)

## absolute 

1，基本介绍

（1）absolute 生成绝对定位的元素。
（2）绝对定位的元素使用 left、right、top、bottom 属性相对于其最接近的一个具有定位属性的父元素进行绝对定位。
（3）如果不存在这样的父元素，则相对于 body 元素，即相对于浏览器窗口。

2，样例代码

    下面代码让标题元素相对于它的父容器做绝对定位（注意父容器 position 要设置为 relative）。
    同时通过 top 属性让标题元素上移，使其覆盖在父容器的上边框。
    最后通过 left 和 margin-left 配合实现这个绝对定位元素的水平居中。

css:
```
  #box {
    width: 200px;
    height: 100px;
    -webkit-box-flex:1;
    border: 1px solid #28AE65;
    border-radius:6px;
    padding: 20px;
    position: relative;
    font-size: 12px;
  }
 
  #title {
    background: #FFFFFF;
    color: #28AE65;
    font-size: 15px;
    text-align: center;
    width: 70px;
    height: 20px;
    line-height: 20px;
    position: absolute;
    top: -10px;
    left: 50%;
    margin-left: -35px;
  }
```
html:
 ```
<div id="box">
  <div id="title">标题</div>
  欢迎访问我的博客
</div>
```
运行效果如下，标题元素虽然是在边框容器的内部。但由于其使用绝对定位，并做位置调整，最后显示效果就是覆盖在父容器边框上。


[点我预览](https://artdong.github.io/blog/2018/07/23/css-position)

## fixed 

1，基本介绍
（1）fixed 生成绝对定位的元素，该元素相对于浏览器窗口进行定位。
（2）固定定位的元素不会随浏览器窗口的滚动条滚动而变化，也不会受文档流动影响，而是始终位于浏览器窗口内视图的某个位置。

2，样例代码
（1）下面代码让输入框位于浏览器窗口的底部。
	
css:
```
  input {
    position: fixed;
    bottom: 10px;
  }
```
html:
 ```
<ol>
  <li>数据</li><li>数据</li><li>数据</li><li>数据</li><li>数据</li><li>数据</li>
  <li>数据</li><li>数据</li><li>数据</li><li>数据</li><li>数据</li><li>数据</li>
  <li>数据</li><li>数据</li><li>数据</li><li>数据</li><li>数据</li><li>数据</li>
  <li>数据</li><li>数据</li><li>数据</li><li>数据</li><li>数据</li><li>数据</li>
</ol>
<input type="text" />
```
（2）可以看到不管滚动条如何滚动，输入框始终处于窗口的最下方。

[点我预览]( https://artdong.github.io/blog/2018/07/23/css-position)


13、 [js] [谈一谈你对this指针的理解](https://github.com/daily-interview/fe-interview/issues/13)

## 为什么要用this

> this提供了一种更优雅的方法来隐式`传递`一个对象的引用，因此可以将API设计得更加简洁并且易于复用。

## 什么是 this

> this 就是一个指针，指向我们调用函数的对象。

## this的值由什么决定

> this的值并不是由函数定义放在哪个对象里面决定，而是函数执行时由谁来唤起决定。

## 什么是执行上下文

> 执行上下文 是语言规范中的一个概念，用通俗的话讲，大致等同于函数的执行“环境”。具体的有：变量作用域（和 作用域链条，闭包里面来自外部作用域的变量），函数参数，以及 this 对象的值。

现在起，我们专注于查明 this 关键词到底指向哪。因此，我们现在要思考的就一个问题：

- 是什么调用函数？是哪个对象调用了函数？

为了理解这个关键概念，我们来测一下下面的代码。

```
let person = {
    name: "Jay",
    greet: function() {
        console.log("hello, " + this.name);
    }
};
person.greet();
```

谁调用了 greet 函数？是 person 这个对象对吧？在 greet() 调用的左边是一个 person 对象，那么 this 关键词就指向 person，this.name 就等于 "Jay"。现在，还是用上面的例子，我加点料：

```
let greet = person.greet; // 将函数引用存起来;
greet(); // 调用函数
```

你觉得在这种情况下控制台会输出什么？“Jay”？undefined？还是别的？

正确答案是 undefined。这说明this 的值并不是由函数定义放在哪个对象里面决定，而是函数执行时由谁来唤起决定。

## 思考题

找出 this 的指向

```
let name = "Jay Global";
let person = {
    name: 'Jay Person',
    details: {
        name: 'Jay Details',
        print: function() {
            return this.name;
        }
    },
    print: function() {
        return this.name;
    }
};
console.log(person.details.print());  // ?
console.log(person.print());          // ?
let name1 = person.print;
let name2 = person.details;
console.log(name1()); // ?
console.log(name2.print()) // ?
```

## 词法作用域

> 词法作用域也就是在词法阶段定义的作用域，也就是说词法作用域在代码书写时就已经确定了。箭头函数就是遵循词法作用域。 

## this 和 箭头函数

在 ES6 里面，不管你喜欢与否，箭头函数被引入了进来。对于那些还没用惯箭头函数或者新学 JavaScript 的人来说，当箭头函数和 this 关键词混合使用时会发生什么，这个点可能会给你带来小小的困惑和蛋蛋的忧伤。

当涉及到 this 关键词，箭头函数 和 普通函数 主要的不同是什么？

> 箭头函数按词法作用域来绑定它的上下文，所以 this 实际上会引用到原来的上下文。

## 思考题

找出this指向

```
let object = {
    data: [1,2,3],
    dataDouble: [1,2,3],
    double: function() {
        console.log("this inside of outerFn double()");
        console.log(this);
        return this.data.map(function(item) {
            console.log(this);      // 这里的 this 是什么？？
            return item * 2;
        });
    },
    doubleArrow: function() {
        console.log("this inside of outerFn doubleArrow()");
        console.log(this);
        return this.dataDouble.map(item => {
            console.log(this);      // 这里的 this 是什么？？
            return item * 2;
        });
    }
};
object.double();
object.doubleArrow();
```

14、 [js] [你遇到过跨域问题吗？跨域请求资源的方式有哪些？](https://github.com/daily-interview/fe-interview/issues/14)

## 什么是跨域

> 在JavaScript中，有一个很重要的安全性限制，被称为“Same-Origin Policy”（同源策略）。它是一种约定，由Netscape公司1995年引入浏览器，是浏览器最核心也最基本的安全功能，如果缺少了同源策略，浏览器很容易受到XSS、CSFR等攻击。所谓同源是指"协议+域名+端口"三者相同，即便两个不同的域名指向同一个ip地址，也非同源。

## 常用的几种跨域解决方案：

- JSONP
- CORS策略
- Nginx代理跨域

## 跨域的原理解析及实现方法

1. 通过JSONP(JSON with padding)跨域

> 通常为了减轻web服务器的负载，我们把js、css，img等静态资源分离到另一台独立域名的服务器上，在html页面中再通过相应的标签从不同域名下加载静态资源，而被浏览器允许，基于此原理，我们可以通过动态创建script，再请求一个带参网址实现跨域通信。

> 而jsonp就是利用了script标签的src属性是没有跨域的限制的，从而达到跨域访问的目的。因此它的最基本原理就是：动态添加一个<script>标签来实现。

原生实现：

```
 <script>
    let script = document.createElement('script');
    script.type = 'text/javascript';

    // 传参一个回调函数名给后端，方便后端返回时执行这个在前端定义的回调函数
    script.src = 'http://www.domain2.com:3000/login?user=admin&callback=handleCallback';
    document.head.appendChild(script);

    // 回调执行函数
    function handleCallback(res) {
        alert(JSON.stringify(res));
    }
 </script>
```

服务端返回如下（返回时即执行全局函数）：

```
handleCallback({"status": true, "user": "admin"})
```

后端node.js代码示例：

```
let querystring = require('querystring');
let http = require('http');
let server = http.createServer();

server.on('request', function(req, res) {
    var params = qs.parse(req.url.split('?')[1]);
    let fn = params.callback;

    // jsonp返回设置
    res.writeHead(200, { 'Content-Type': 'text/javascript' });
    res.write(fn + '(' + JSON.stringify(params) + ')');

    res.end();
});

server.listen('3000');
console.log('Server is running at port 3000...');
```

JSONP的不足之处：

- 只能使用get方法，不能使用post方法：我们知道 script，link, img 等等标签引入外部资源，都是 get 请求的，那么就决定了 jsonp 一定是 get 的。但有时候我们使用的 post 请求也成功，为啥呢？这是因为当我们指定dataType:'jsonp',不论你指定：type:"post" 或者type:"get"，其实质上进行的都是 get 请求！

- 没有关于 JSONP 调用的错误处理。如果动态脚本插入有效，就执行调用；如果无效，就静默失败。失败是没有任何提示的。例如，不能从服务器捕捉到 404 错误，也不能取消或重新开始请求。不过，等待一段时间还没有响应的话，就不用理它了。

2. CORS策略

- 原理：

     CORS是一个W3C标准，全称是"跨域资源共享"（Cross-origin resource sharing）。它允许浏览器向跨源服务器，发出XMLHttpRequest请求，从而克服了AJAX只能同源使用的限制。它为Web服务器定义了一种方式，允许网页从不同的域访问其资源.
　　CORS系统定义了一种浏览器和服务器交互的方式来确定是否允许跨域请求。 它是一个妥协，有更大的灵活性，但比起简单地允许所有这些的要求来说更加安全。

- 实现方法：

　　CORS需要浏览器和服务器同时支持。目前，所有浏览器都支持该功能，IE浏览器不能低于IE10（IE8/9需要使用XDomainRequest对象来支持CORS）。

　　整个CORS通信过程，都是浏览器自动完成，不需要用户参与。对于开发者来说，CORS通信与同源的AJAX通信没有差别，代码完全一样。浏览器一旦发现AJAX请求跨源，就会自动添加一些附加的头信息，有时还会多出一次附加的请求，但用户不会有感觉。

- 前端[www.domain1.com]设置：

原生ajax

// 前端设置是否带cookie
xhr.withCredentials = true;

示例代码：

```
let xhr = new XMLHttpRequest(); // IE8/9需用window.XDomainRequest兼容

// 前端设置是否带cookie
xhr.withCredentials = true;

xhr.open('post', 'http://www.domain2.com:3000/login', true);
xhr.setRequestHeader('Content-Type', 'application/x-www-form-urlencoded');
xhr.send('user=admin');

xhr.onreadystatechange = function() {
    if (xhr.readyState == 4 && xhr.status == 200) {
        alert(xhr.responseText);
    }
};
```

- Nodejs后台示例：

```
let http = require('http');
let server = http.createServer();
let qs = require('querystring');

server.on('request', function(req, res) {
    let postData = '';

    // 数据块接收中
    req.addListener('data', function(chunk) {
        postData += chunk;
    });

    // 数据接收完毕
    req.addListener('end', function() {
        postData = qs.parse(postData);

        // 跨域后台设置
        res.writeHead(200, {
            'Access-Control-Allow-Credentials': 'true',     // 后端允许发送Cookie
            'Access-Control-Allow-Origin': 'http://www.domain1.com',    // 允许访问的域（协议+域名+端口）
            /* 
             * 此处设置的cookie还是domain2的而非domain1，因为后端也不能跨域写cookie(nginx反向代理可以实现)，
             * 但只要domain1中写入一次cookie认证，后面的跨域接口都能从domain2中获取cookie，从而实现所有的接口都能跨域访问
             */
            'Set-Cookie': 'l=a123456;Path=/;Domain=www.domain2.com;HttpOnly'  // HttpOnly的作用是让js无法读取cookie
        });

        res.write(JSON.stringify(postData));
        res.end();
    });
});

server.listen('3000');
console.log('Server is running at port 3000...');
```

- CORS策略的优缺点：

 > 优点：

　1. CORS支持所有类型的HTTP请求。

　2. 使用CORS，开发者可以使用普通的XMLHttpRequest发起请求和获得数据，比起JSONP有更好的错误处理。

> 缺点： 兼容性方面相对差一点，ie10或以上才支持

3. nginx代理跨域

- nginx配置解决iconfont跨域

浏览器跨域访问js、css、img等常规静态资源被同源策略许可，但iconfont字体文件(eot|otf|ttf|woff|svg)例外，此时可在nginx的静态资源服务器中加入以下配置。

```
location / {
  add_header Access-Control-Allow-Origin *;
}
```

- nginx反向代理接口跨域

跨域原理： 同源策略是浏览器的安全策略，不是HTTP协议的一部分。服务器端调用HTTP接口只是使用HTTP协议，不会执行JS脚本，不需要同源策略，也就不存在跨越问题。

实现思路：通过nginx配置一个代理服务器（域名与domain1相同，端口不同）做跳板机，反向代理访问domain2接口，并且可以顺便修改cookie中domain信息，方便当前域cookie写入，实现跨域登录。

nginx具体配置：

```
#proxy服务器
server {
    listen 81;
    server_name  www.domain1.com;

    location / {
        proxy_pass   http://www.domain2.com:3000;  #反向代理
        proxy_cookie_domain www.domain2.com www.domain1.com; #修改cookie里域名
        index  index.html index.htm;

        # 当用webpack-dev-server等中间件代理接口访问nignx时，此时无浏览器参与，故没有同源限制，下面的跨域配置可不启用
        add_header Access-Control-Allow-Origin http://www.domain1.com;  #当前端只跨域不带cookie时，可为*
        add_header Access-Control-Allow-Credentials true;
    }
}
```

1.) 前端代码示例：

```
let xhr = new XMLHttpRequest();

// 前端开关：浏览器是否读写cookie
xhr.withCredentials = true;

// 访问nginx中的代理服务器
xhr.open('get', 'http://www.domain1.com:81/?user=admin', true);
xhr.send();
```

2.) Nodejs后台示例：

```
let http = require('http');
let server = http.createServer();
let qs = require('querystring');

server.on('request', function(req, res) {
    let params = qs.parse(req.url.substring(2));

    // 向前台写cookie
    res.writeHead(200, {
        'Set-Cookie': 'l=a123456;Path=/;Domain=www.domain2.com;HttpOnly'   // HttpOnly:脚本无法读取
    });

    res.write(JSON.stringify(params));
    res.end();
});

server.listen('3000');
console.log('Server is running at port 3000...');
```

15、 [http] [什么是强缓存和协商缓存？](https://github.com/daily-interview/fe-interview/issues/15)

## 什么是浏览器缓存

浏览器缓存(Brower Caching)是浏览器在本地磁盘对用户最近请求过的文档进行存储，当访问者再次访问同一页面时，浏览器就可以直接从本地磁盘加载文档。

## 为什么要使用浏览器缓存

1.减少了冗余的数据传输，节省了网费

2.减少了服务器的负担，大大提升了网站的性能

3.加快了客户端加载网页的速度

4.更好的用户体验

## 浏览器缓存类型

> 浏览器缓存主要有两类：缓存协商和彻底缓存，也有称之为协商缓存和强缓存。

1.强缓存：强制缓存整体流程比较简单，就是在第一次访问服务器取到数据之后，在过期时间之内不会再去重复请求。实现这个流程的核心就是如何知道当前时间是否超过了过期时间。

> 强制缓存的过期时间通过第一次访问服务器时返回的响应头获取。在 http 1.0 和 http 1.1 版本中通过不同的响应头字段实现。

- http 1.0

在 http 1.0 版本中，强制缓存通过 Expires 响应头来实现。 expires 表示未来资源会过期的时间。也就是说，当发起请求的时间超过了 expires 设定的时间，即表示资源缓存时间到期，会发送请求到服务器重新获取资源。而如果发起请求的时间在 expires 限定的时间之内，浏览器会直接读取本地缓存数据库中的信息（from memory or from disk），两种方式根据浏览器的策略随机获取。

- http 1.1

在 http 1.1 版本中，强制缓存通过 Cache-Control 响应头来实现。Cache-Control 拥有多个值：

    private：客户端可以缓存
    public：客户端和代理服务器均可缓存；
    max-age=xxx：缓存的资源将在 xxx 秒后过期；
    no-cache：需要使用协商缓存来验证是否过期；
    no-store：不可缓存

最常用的字段就是 max-age=xxx ，表示缓存的资源将在 xxx 秒后过期。一般来说，为了兼容，两个版本的强制缓存都会被实现。

> 强制缓存只有首次请求才会跟服务器通信，读取缓存资源时不会发出任何请求，资源的 Status 状态码为 200，资源的 Size 为 from memory 或者 from disk ，http 1.1 版本的实现优先级会高于 http 1.0 版本的实现。

2.协商缓存：协商缓存与强制缓存的不同之处在于，协商缓存每次读取数据时都需要跟服务器通信，并且会增加缓存标识。在第一次请求服务器时，服务器会返回资源，并且返回一个资源的缓存标识，一起存到浏览器的缓存数据库。当第二次请求资源时，浏览器会首先将缓存标识发送给服务器，服务器拿到标识后判断标识是否匹配，如果不匹配，表示资源有更新，服务器会将新数据和新的缓存标识一起返回到浏览器；如果缓存标识匹配，表示资源没有更新，并且返回 304 状态码，浏览器就读取本地缓存服务器中的数据。

在 http 协议的 1.0 和 1.1 版本中也有不同的实现方式。

- http 1.0

在 http 1.0 版本中，第一次请求资源时服务器通过 Last-Modified 来设置响应头的缓存标识，并且把资源最后修改的时间作为值填入，然后将资源返回给浏览器。在第二次请求时，浏览器会首先带上 If-Modified-Since 请求头去访问服务器，服务器会将 If-Modified-Since 中携带的时间与资源修改的时间匹配，如果时间不一致，服务器会返回新的资源，并且将 Last-Modified 值更新，作为响应头返回给浏览器。如果时间一致，表示资源没有更新，服务器返回 304 状态码，浏览器拿到响应状态码后从本地缓存数据库中读取缓存资源。

这种方式有一个弊端，就是当服务器中的资源增加了一个字符，后来又把这个字符删掉，本身资源文件并没有发生变化，但修改时间发生了变化。当下次请求过来时，服务器也会把这个本来没有变化的资源重新返回给浏览器。

- http 1.1

在 http 1.1 版本中，服务器通过 Etag 来设置响应头缓存标识。Etag 的值由服务端生成。在第一次请求时，服务器会将资源和 Etag 一并返回给浏览器，浏览器将两者缓存到本地缓存数据库。在第二次请求时，浏览器会将 Etag 信息放到 If-None-Match 请求头去访问服务器，服务器收到请求后，会将服务器中的文件标识与浏览器发来的标识进行对比，如果不相同，服务器返回更新的资源和新的 Etag ，如果相同，服务器返回 304 状态码，浏览器读取缓存。

> 协商缓存每次请求都会与服务器交互，第一次是拿数据和标识的过程，第二次开始，就是浏览器询问服务器资源是否有更新的过程。每次请求都会传输数据，如果命中缓存，则资源的 Status 状态码为 304 而不是 200 。同样的，一般来讲为了兼容，两个版本的协商缓存都会被实现，http 1.1 版本的实现优先级会高于 http 1.0 版本的实现。

> 两者的共同点是，都是从客户端缓存中读取资源；区别是强缓存不会发请求，协商缓存会发请求。


16、 [js] [了解js闭包吗？谈谈你对js闭包的理解。](https://github.com/daily-interview/fe-interview/issues/16)

## 什么是闭包

MDN的解释：闭包是`函数`和`声明该函数的词法环境`的组合。

简单讲，闭包就是指有权访问另一个函数作用域中的变量的函数。

它由两部分构成：函数，以及创建该函数的环境。环境由闭包创建时在作用域中的所有局部变量组成。

理解闭包的关键在于：外部函数调用之后其变量对象本应该被销毁，但闭包的存在使我们仍然可以访问外部函数的变量对象，这就是闭包的重要概念。

## 如何产生一个闭包函数

> 创建闭包最常见方式，就是在一个函数内部创建另一个函数。

```
function outer() {
    let name = "hello"; // 闭包创建时所能访问的局部变量
    function sayHello() { // 闭包函数
        alert(name);
    }
    return sayHello; // 返回闭包函数
}

let myFunc = outer();
myFunc();
```

> 闭包的作用域链包含着它自己的作用域，以及包含它的函数的作用域和全局作用域。

outer有了myFunc的引用，内存一直得不到释放，咋办呢？这样的函数多了是不是会造成内存溢出？
手动释放一下：

```
myFunc = null;
```

## 闭包的注意事项（如何防止内存泄漏）

通常，函数的作用域及其所有变量都会在函数执行结束后被销毁。但是，在创建了一个闭包以后，这个函数的作用域就会一直保存到闭包不存在为止。

```
function makeAdder(x) {
  return function(y) {
    return x + y;
  };
}

let add5 = makeAdder(5);
let add10 = makeAdder(10);

console.log(add5(2));  // 7
console.log(add10(2)); // 12

add5 = null;
add10 = null;
```

add5 和 add10 都是闭包。它们共享相同的函数定义，但是保存了不同的词法环境。在 add5 的环境中，x 为 5。而在 add10 中，x 则为 10。

最后通过 null 释放了 add5 和 add10 对闭包的引用。

在javascript中，如果一个对象不再被引用，那么这个对象就会被垃圾回收机制回收；

如果两个对象互相引用，而不再被第3者所引用，那么这两个互相引用的对象也会被回收。

## 闭包中的this对象

```
let name = "window";
let obj = {
	name: 'object',
	getName: function() {
		return function() {
			return this.name;
		}
	}
}
obj.getName()();  // window
```

在上面这段代码中，obj.getName()()实际上是在全局作用域中调用了匿名函数，this指向了window。
window才是匿名函数功能执行的环境。

如果想使this指向外部函数的执行环境，可以这样改写：

```
let name = "window";
let obj = {
	name: 'object',
	getName: function() {
		var that = this;
		return function() {
			return that.name;
		}
	}
}
obj.getName()();
```

## 函数内部的定时器

当函数内部的定时器引用了外部函数的变量对象时，该变量对象不会被销毁。

```
(function() {
	let a = 0;
	setInterval(function(){
		console.log(a++);
	}, 1000)
})()
```

## 闭包的用途

- 模拟块级作用域

```
var isShow = true;
if(isShow){    
	var a=1000;
	console.log(a);
}
console.log(a); // 在if定义的变量在外部可以访问
```

```
(function(){  // a在外部就不认识啦
        var isShow = true;
        if(isShow){    
        	var a=10000;
        	console.log(a);
        }
  })();  
  console.log(a); // 报错，无法访问
```

- 让变量的值始终保持在内存中，对结果进行缓存

```
function fn(){
    let count = 0;
    return function(){
        count++;
        return count;
    }
}
let add=fn();
add();  // 1
add(); // 2
add(); // 3
```

-  封装工具函数

```
let counter = (function(){
    let privateCounter = 0; // 私有变量
    function change(val){
        privateCounter += val;
    }
    return {
        increment:function(){   // 三个闭包共享一个词法环境
            change(1);
        },
        decrement:function(){
            change(-1);
        },
        value:function(){
            return privateCounter;
        }
    };
})();

counter.value();  // 0
counter.increment();
counter.value();  // 1
```

17、 [nodejs] [用过nginx吗？nginx负载均衡如何实现？](https://github.com/daily-interview/fe-interview/issues/17)

## 什么是nginx？

Nginx("engine x")是一款是由俄罗斯的程序设计师Igor Sysoev所开发高性能的Web和反向代理服务器，也是一个 IMAP/POP3/SMTP 代理服务器。

在高连接并发的情况下，Nginx是Apache服务器不错的替代品。

## nginx服务器基本特征

- 处理静态文件，索引文件以及自动索引；打开文件描述符缓冲
- 无缓存的反向代理加速，简单的负载均衡和容错
- FastCGI，简单的负载均衡和容错
- 模块化的结构。包括gzipping, byte ranges, chunked responses,以及 SSI-filter等filter。如果由FastCGI或 其它代理服务器处理单页中存在的多个SSI，则这项处理可以并行运行，而不需要相互等待
- 支持SSL 和 TLSSNI

## nginx常用功能

1、Http代理，反向代理：作为web服务器最常用的功能之一，尤其是反向代理。

Nginx在做反向代理时，提供性能稳定，并且能够提供配置灵活的转发功能。Nginx可以根据不同的正则匹配，采取不同的转发策略，比如图片文件结尾的走文件服务器，动态页面走web服务器，只要你正则写的没问题，又有相对应的服务器解决方案，你就可以随心所欲的玩。并且Nginx对返回结果进行错误页跳转，异常判断等。如果被分发的服务器存在异常，他可以将请求重新转发给另外一台服务器，然后自动去除异常服务器。

2、负载均衡 

Nginx的负载均衡是通过upstream实现的。

eg.

```
upstream test.aaa { 
    ip_hash;  ## 调度算法
    server 192.168.1.10:80; 
    server 192.168.1.11:80 down; 
    server 192.168.1.12:8009 max_fails=3 fail_timeout=20s; 
    server 192.168.1.13:8080; 
 } 
server { 
    listen       80;
    server_name  localhost;
    location / { 
    proxy_pass http://test.aaa; 
    } 
 } 
```

upstream 支持的负载均衡算法：

- 轮询（默认）

> 每个请求按时间顺序逐一分配到不同的后端服务器，如果后端某台服务器宕机，故障系统被自动剔除，使用户访问不受影响。

- weight

> 指定轮询几率，weight和访问比率成正比，用于后端服务器性能不均的情况。

- fair(第三方)

> 按后端服务器的响应时间来分配请求，响应时间短的优先分配。Nginx本身是不支持fair的，如果需要使用这种调度算法，必须下载Nginx的upstream_fair模块。

- url_hash(第三方)

> 按访问URL的hash结果来分配请求，使每个URL定向到同一个后端服务器，后端服务器为缓存时比较适用。另外，在upstream中加入hash语句后，server语句不能写入weight等其他参数。Nginx本身是不支持url_hash的，如果需要使用这种调度算法，必须安装Nginx 的hash软件包。

upstream 支持的状态参数

- down，表示当前的server暂时不参与负载均衡。
- backup，预留的备份机器。当其他所有的非backup机器出现故障或者忙的时候，才会请求backup机器，因此这台机器的压力最轻。
- max_fails，允许请求失败的次数，默认为1。当超过最大次数时，返回proxy_next_upstream 模块定义的错误。
- fail_timeout，在经历了max_fails次失败后，暂停服务的时间。max_fails可以和fail_timeout一起使用。

> 注，当负载调度算法为ip_hash时，后端服务器在负载均衡调度中的状态不能是weight和backup。

3、web缓存

Nginx可以对不同的文件做不同的缓存处理，配置灵活，并且支持FastCGI_Cache，主要用于对FastCGI的动态程序进行缓存。配合着第三方的ngx_cache_purge，对制定的URL缓存内容可以的进行增删管理。

18、 [h5] [如果图片加载失败，如何做统一处理及优化？](https://github.com/daily-interview/fe-interview/issues/18)

## 项目中遇到的问题

在实际项目中，不可避免的会遇到在页面中加载大量图片，但可能由于网络问题，或者图片文件缺失等问题，导致图片不能正常展示。

我们希望有一种降级处理的方式，可以在图片加载失败后显示一张我们预先设定好的默认图片。

## 如何解决

> 监听图片的 error 事件

由于图片加载失败后，会抛出一个 error 事件，我们可以通过监听 error 事件的方式来对图片进行降级处理。

```
<img id="img" src="//xxx/img.png">
let img = document.getElementById('img');
img.addEventListener('error',function(e){
    e.target.src = '//xxx/default.png';  // 为当前图片设定默认图
})
```

这种方式，确实实现了对异常图片的降级处理，但每张图片都需要通过 JS 进行获取，并且监听 error 事件，对于大量图片的情况并不适用。

为此，我们可以使用内联事件来监听 error 事件

```
<img src="//xxx/img.png" onerror="this.src = '//xxx/default.png'">
```

我们可以看到，完全不需要单独去写 JS 的监听，我们就实现了异常图片的降级处理，但这种方式还不够好，因为我们仍然需要手动的向 img 标签中添加内联事件，在实际开发过程中，很难保证每张图片都不漏写。

## 优化方案

> 通过在全局监听的方式，来对异常图片做降级处理

DOM2级事件规定事件流包含三个阶段：

事件捕获阶段
处于目标阶段
事件冒泡阶段

首先发生的是事件捕获，为截获事件提供了机会。然后是实际的目标接收到的事件。最后一个阶段是冒泡阶段。

我们上文中的监听图片自身的 error 事件，实际上在事件流中是处于目标阶段。

对于 img 的 error 事件来说，是无法冒泡的，但是是可以捕获的，我们的实现如下:

```
window.addEventListener('error',function(e){
    // 当前异常是由图片加载异常引起的
    if( e.target.tagName.toUpperCase() === 'IMG' ){
        e.target.src = '//xxx/default.jpg';
    }
},true)
```
最后，我们在思考一个问题，当网络出现异常的时候，必然会出现什么网络图片都无法加载的情况，这样就会导致我们监听的 error 事件。被无限触发，所以我们可以设定一个计数器，当达到期望的错误次数时停止对图片赋予默认图片的操作，改为提供一个Base64的图片。

实现起来也很简单，如下：

```
window.addEventListener('error',function(e){
    let target = e.target, // 当前dom节点
        tagName = target.tagName,
        count = Number(target.dataset.count ) || 0, // 以失败的次数，默认为0
        max= 3; // 总失败次数，此时设定为3
    // 当前异常是由图片加载异常引起的
    if( tagName.toUpperCase() === 'IMG' ){
        if(count >= max){
            target.src = 'data:image/jpeg;base64,/9j/4AAQSkZJRgABAQEAYABgAAD//AK3/ALYH+5hX6FV5N4Y/5GHwx/vyf+iJa9ZrysPhoYVShDZu/potDmwWFhhIzhT2bv6aLQ//Z';
        }else{
            target.dataset.count = count + 1;
            target.src = '//xxx/default.jpg';
        }
    }
},true)
```

19、 [js] [从输入URL到页面加载完成发生了什么？](https://github.com/daily-interview/fe-interview/issues/19)

## 从输入 URL 到页面加载完成的过程

- 首先通过DNS解析获得网址的对应IP地址，如果这一步做了智能 DNS 解析的话，会提供访问速度最快的 IP 地址。

- 接下来是 TCP 握手 （3次握手4次挥手），应用层会下发数据给传输层，这里 TCP 协议会指明两端的端口号，然后下发给网络层。网络层中的 IP 协议会确定 IP 地址，并且指示了数据传输中如何跳转路由器。然后包会再被封装到数据链路层的数据帧结构中，最后就是物理层面的传输了。

- TCP 握手结束后会进行 TLS 握手，然后就开始正式的传输数据。

- 数据在进入服务端之前，可能还会先经过负责负载均衡的服务器，它的作用就是将请求合理的分发到多台服务器上，这时假设服务端会响应一个 HTML 文件。

- 首先浏览器会判断状态码是什么，如果是 200 那就继续解析，如果 400 或 500 的话就会报错，如果 300 的话会进行重定向，这里会有个重定向计数器，避免过多次的重定向，超过次数也会报错。

- 浏览器开始解析文件，如果是 gzip 格式的话会先解压一下，然后通过文件的编码格式知道该如何去解码文件。

- 文件解码成功后会正式开始渲染流程，先会根据 HTML 构建 DOM 树，有 CSS 的话会去构建 CSSOM 树。如果遇到 script 标签的话，会判断是否存在 async 或者 defer ，前者会并行进行下载并执行 JS，后者会先下载文件，然后等待 HTML 解析完成后顺序执行，如果以上都没有，就会阻塞住渲染流程直到 JS 执行完毕。遇到文件下载的会去下载文件，这里如果使用 HTTP 2.0 协议的话会极大的提高多图的下载效率。

-  初始的 HTML 被完全加载和解析后会触发 DOMContentLoaded 事件。

- CSSOM 树和 DOM 树构建完成后会开始生成 Render 树，这一步就是确定页面元素的布局、样式等等诸多方面的东西。

- 在生成 Render 树的过程中，浏览器就开始调用 GPU 绘制，合成图层，将内容显示在屏幕上。
