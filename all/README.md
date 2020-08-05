# fe-interview

[![mnt-image](https://img.shields.io/maintenance/yes/2020.svg)](../../commits/master)
[![GitHub stars](https://img.shields.io/github/stars/daily-interview/fe-interview.svg)](https://github.com/daily-interview/fe-interview/stargazers)
[![GitHub forks](https://img.shields.io/github/forks/daily-interview/fe-interview.svg)](https://github.com/daily-interview/fe-interview/network)
[![GitHub license](https://img.shields.io/badge/license-MIT-blue.svg)](https://github.com/daily-interview/fe-interview/blob/master/LICENSE)

## 所有面试题

- [js] [介绍一下 JS 的基本数据类型。](https://github.com/daily-interview/fe-interview/issues/1)

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

- [js] [js实现几种常见排序算法。( 手写 )](https://github.com/daily-interview/fe-interview/issues/2)


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

- [css] [有哪几种常用的清除浮动方法？](https://github.com/daily-interview/fe-interview/issues/3)

- [js] [Object.assign 是浅拷贝还是深拷贝？实现深拷贝的方法有哪些？](https://github.com/daily-interview/fe-interview/issues/4)

- [js] [promise和setTimeout执行顺序是怎样的？](https://github.com/daily-interview/fe-interview/issues/5)

- [ts] [说一说Typescript中的泛型的作用及使用场景。](https://github.com/daily-interview/fe-interview/issues/6)

- [http] [说说你对http和https的理解](https://github.com/daily-interview/fe-interview/issues/7)

- [js] [说说你对 Promise 的理解](https://github.com/daily-interview/fe-interview/issues/8)

- [js] [说一下对bind，call，apply三个函数的认识，自己实现一下bind方法](https://github.com/daily-interview/fe-interview/issues/9)

- [css] [说说对 BFC（Block formatting contexts） 的理解](https://github.com/daily-interview/fe-interview/issues/10)

......

- [js] [图片懒加载原理及如何实现](https://github.com/daily-interview/fe-interview/issues/51)

- [js] [JS获取url参数的方法](https://github.com/daily-interview/fe-interview/issues/52)

- [js] [手写实现一个合乎规范的Promise](https://github.com/daily-interview/fe-interview/issues/53)

- [js] [requestAnimationFrame原理及兼容性封装](https://github.com/daily-interview/fe-interview/issues/54)

- [webpack优化] [用过HappyPack吗？HappyPack有什么优点?](https://github.com/daily-interview/fe-interview/issues/55)

- [webpack配置] [webpack配置路径别名](https://github.com/daily-interview/fe-interview/issues/57)

- [webpack配置] [webpack添加路径别名后，vscode不能智能提示，如何解决？](https://github.com/daily-interview/fe-interview/issues/58)

- [js] [如何只用两行代码实现判断js中所有数据类型?](https://github.com/daily-interview/fe-interview/issues/59)

- [js] [不用window.open打开新窗口](https://github.com/daily-interview/fe-interview/issues/60)