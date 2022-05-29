JavaScript

**js代码要写在script标签中**

```html
<!DOCTYPE html>
<html>
    <head>
        <meta charset="UTF-8">
        <title></title>
        <!--该行为注释,注意前后都有-->
        <script type="text/javascript">
            /*  不写type默认
            *
            */
            alert("输出警告");/*弹出警告*/
            document.write("");/*在body中写内容*/
            console.log("")；/*向控制台输出内容，不在页面里*/
            
        </script>
    </head>
</html>
```

也可写在body中

```html
<!DOCTYPE html>
<html>
    <head>
        <meta charset="UTF-8">
        <title></title>
    </head>
    <body>
        <!--可以将js代码写在标签的onclick属性中-->
        <button onclick="alert('讨厌');">点我一下</button>
        <!--可以将js代码写在超链接的href属性中-->
        <a href="javascript:alert('让你点我')">点我一下</a>
        <!--这种属于结构和行为耦合，不方便维护-->
    </body>
</html>
```

也可以和CSS一样，存在外部文件，然后再通过script标签引入（最佳）

```js
//JS文件
alert("输出警告");
```

```html
<!DOCTYPE html>
<html>
    <head>
        <meta charset="UTF-8">
        <title></title>
        <!--该行为注释,注意前后都有-->
        <script type="text/javascript" src='文件地址/script.js'></script>
        <!--外部文件中可以在不同的页面中同时引用,利用浏览器的缓存机制
		一但引用了外部文件，同一个script标签执行内部代码-->
    </head>
</html>
```

## 基本语法

### 字面量和变量

字面量：不可改变的值，可以直接使用

```js
//使用 var 声明一个变量
var a;
```

标识符： 可以由数字、字母、下划线、$ 组成

JS底层保存标识符时，**采用的unicode编码**

### 数据类型

基本数据类型：

| String | Number | Boolean | Null | Undefined |
| ------ | ------ | ------- | ---- | --------- |

引用数据类型

> Object

强制类型转换 

- parseFloat()   parseInt()
- Number()
- Plus sign(+)

```js
var str = "Hello";		//字符串变量需要引号
console.log(Number.MAX_VALUE);//输出最大数，如果超过，则返回 Infinity
//Null 专门表示为空的对象，用typeof 检查返回object

//强制类型转换
//调用被转换数据类型的toString方法，该方法不会影响原变量[只适用String, Number,Boolean]
var a = 123;
a = a.toString();
//调用String()函数
a = 123;
a = String(a);
//
a = "123";
a = Number(a);
//parseInt()   parseFloat()专门对付字符串
a = "123px";
a = parseInt(a);//123
a = "123b456px";
a = parseInt(a);//123
a = "123.456px";
a = parseFloat(a);//123.456，也可用于Float转Int
```

### Math Object

```js
//Math Object provides a lots of methods to work with numbers.

const PI = Math.PI;

//取整操作 round  四舍五入
//floor 向下取整
//ceil  向上取整
//Absolute value
console.log(Math.abs(-10))      // 10

//Square root
console.log(Math.sqrt(100))     // 10

console.log(Math.sqrt(2))       // 1.4142135623730951

// Power
console.log(Math.pow(3, 2))     // 9

console.log(Math.E)             // 2.718

// Logarithm
// Returns the natural logarithm with base E of x, Math.log(x)
console.log(Math.log(2))        // 0.6931471805599453
console.log(Math.log(10))       // 2.302585092994046

// Trigonometry
Math.sin(0)
Math.sin(60)

Math.cos(0)
Math.cos(60)
```

```js
let randomNum = Math.random()         // generates 0 to 0.999
let numBtnZeroAndTen = randomNum * 11

console.log(numBtnZeroAndTen)         // this gives: min 0 and max 10.99

let randomNumRoundToFloor = Math.floor(numBtnZeroAndTen)
console.log(randomNumRoundToFloor)    // this gives between 0 and 10
```

长段文字，在最后使用\表示字符串没有结束

```js
const paragraph = "My name is Asabeneh Yetayeh. I live in Finland, Helsinki.\
I am a teacher and I love teaching. I teach HTML, CSS, JavaScript, React, Redux, \
Node.js, Python, Data Analysis and D3.js for anyone who is interested to learn. \
It was one of the most rewarding and inspiring experience.\
I hope you are enjoying too."

console.log(paragraph)
```

### 模板插入

```js
console.log(`The sum of 2 and 3 is 5`);
let a = 2;
let b = 3;
console.log(`The sum of ${a} and  ${b} is ${a + b}`)
```

可添加表达式

```js
let a = 2
let b = 3
console.log(`${a} is greater than ${b}: ${a > b}`)
```

### String函数

toUpperCase()

toLowerCase()

subString():注意下标

```js
let string = 'JavaScript'
let firstLetter = string[0]
console.log(firstLetter)           // J

let country = 'Finland'
console.log(country.toUpperCase())    // FINLAND

let string = 'JavasCript'
console.log(string.toLowerCase())     // javascript
// substr() 函数
let string = 'JavaScript'
console.log(string.substr(4,6))    // Script

```

*split()*:

```js
let string = '30 Days Of JavaScript'

console.log(string.split())   // Changes to an array -> ["30 Days Of JavaScript"]
console.log(string.split(' '))  // Split to an array at space -> ["30", "Days", "Of", "JavaScript"]

```

*trim()*:修建多余的空格

```js
let string = '   30 Days Of JavaScript   '
console.log(string)//   30 Days Of JavasCript   
console.log(string.trim(' '))//30 Days Of JavasCript
```

*includes()*: 包含子序列则返回true

*replace()*:替换旧子序列

*charAt()*: 根据下标返回字符

```js
let string = '30 Days Of JavaScript'
console.log(string.charAt(0))        // 3
```

*charCodeAt()*: 根据下标返回字符的ASCII码

*indexOf()*:根据字串返回所在位置（第一次出现）

*lastIndexOf()*:根据字串返回所在位置（最后一次出现）

*concat()*: 将多个字串链接成一个

*startsWith*():检查是否以该字串起始 

*endsWith()*:检查是否以该字串为末尾

*search()*:寻找字串，返回第一个下标位置，其括号内可以为正则表达式

match():

```js
//用法
string.match(substring)

let string = 'I love JavaScript. If you do not love JavaScript what else can you love.'
console.log(string.match('love'))

//["love", index: 2, input: "I love JavaScript. If you do not love JavaScript what else can you love.", groups: undefined]

let pattern = /love/gi
console.log(string.match(pattern))   // ["love", "love", "love"]
```

*repeat(n)*:重复复制n遍

### ==与=

```js
console.log(3 == '3')           // true, compare only value
console.log(3 === '3')          // false, compare both value and data type
console.log(0 == false)         // true, equivalent
console.log(0 === false)        // false, not exactly the same
console.log(undefined == null)  // true
console.log(undefined === null) // false
```

### 三元运算符

```js
number > 0
  ? console.log(`${number} is a positive number`)
  : console.log(`${number} is a negative number`)
```

## Window Method

### prompt()

```js
let number = prompt('Enter number', 'number goes here')//返回保存值
console.log(number)
```

```js
 //使用窗口方法询问用户base和height来返回area
let base = prompt('Enter base','');
let height = prompt('Enter height');
let area = base*height*0.5;
alert(`The area of the triangle is ${area}`)
```



### confirm()

```js
const agree = confirm('Are you sure you like to delete? ')
console.log(agree) // 根据确定和取消返回true 获或 false
```

## Date Object

| Method            | 描述                     | 例子          |
| ----------------- | ------------------------ | ------------- |
| getFullYear()     | (yyyy)                   | 2020          |
| getMonth()        | (0-11)月份-1             | 0             |
| getDate()         | (1-31)                   | 4             |
| getHours()        | (0-23)                   | 0             |
| getMinutes()      | (0-59)                   | 56            |
| getSeconds()      | (0-59)                   | 43            |
| getMilliseconds() | (0-999)                  | 234           |
| getTime()         | 从(1970,1,1)开始的毫秒值 | 1231412412324 |
| getDay()          | 以星期几                 | 6             |

创建一个time object

```js
const now = new Date()
console.log(now)//Tue Jan 11 2022 14:57:53 GMT+0800 (中国标准时间)
console.log(now.getFullYear())//2022
```

练习

```js
/*1.Write a code which can give grades to students according to theirs scores:
80-100, A
70-89, B
60-69, C
50-59, D
0-49, F*/
let score = prompt('your score','');
a = Math.floor(score/10);
switch (a){
    case 10:console.log("A");break;
    case 9:console.log("A");break;
    case 8:console.log("B");break;
    case 7:console.log("B");break;
    case 6:console.log("C");break;
    case 5:console.log("D");break;
    default:console.log("F");break;
}
/*2Check if the season is Autumn, Winter, Spring or Summer. If the user input is :
September, October or November, the season is Autumn.
December, January or February, the season is Winter.
March, April or May, the season is Spring
June, July or August, the season is Summer*/
const now = new Date();
let mon = Date.
```

## Array

```js
//定义
const arr = Array();
let arr = new Array();
//创建一个空列表
const arr = []
//列表可以有不同数据类型
const arr = [
    'Asabeneh',
    250,
    true,
    { country: 'Finland', city: 'Helsinki' },
    { skills: ['HTML', 'CSS', 'JS', 'React', 'Python'] }
] // arr containing different data types
console.log(arr)
```

通过split创建

```js
let js = 'JavaScript'
const charsInJavaScript = js.split('')
```

方法：*Array, length, concat, indexOf, slice, splice, join, toString, includes, lastIndexOf, isArray, fill, push, pop, shift, unshift*

`Array()`：创建

```js
const eightEmptyValues = Array(8)//创建 [empty x 8]
```

`fill()`:创建时静态填充

```js
const eightXvalues = Array(8).fill('X') 
console.log(eightXvalues) // ['X', 'X','X','X','X','X','X','X']
```

`concat()`:连接两个数组

```js
const firstList = [1,2,3]
const secondList = [4,5,6]
const thirdList = firstlist.concat(secondList)
```

`length`:返回长度

`indexOf()`:返回该字符（第一次出现）的下标，如果不存在返回-1

`lastIndexOf()`：返回该字符（最后一次出现）的下标，如果不存在返回-1

`includes()`:存在元素，返回true

`isArray()`:检查是否Array，返回true

`toString()`:转化为字符串

```js
const numbers = [1, 2, 3, 4, 5]
console.log(numbers.toString()) // 1,2,3,4,5

const names = ['Asabeneh', 'Mathias', 'Elias', 'Brook']
console.log(names.toString()) // Asabeneh,Mathias,Elias,Brook
```

`join()`:根据传入参数来连接数组返回字符串，默认加逗号

```js
const numbers = [1, 2, 3, 4, 5]
console.log(numbers.join()) // 1,2,3,4,5

const names = ['Asabeneh', 'Mathias', 'Elias', 'Brook']

console.log(names.join()) // Asabeneh,Mathias,Elias,Brook
console.log(names.join('')) //AsabenehMathiasEliasBrook
console.log(names.join(' ')) //Asabeneh Mathias Elias Brook
console.log(names.join(', ')) //Asabeneh, Mathias, Elias, Brook
console.log(names.join(' # ')) //Asabeneh # Mathias # Elias # Brook
```

`slice()`:根据两个参数（首位位置）切片序列（不包含最后一个位置）

```js
const numbers = [1,2,3,4,5]
console.log(numbers.slice()) //[1,2,3,4,5]
console.log(numbers,slice(0))//[1,2,3,4,5]
console.log(numbers.slice(1,4)) //[2,3,4] 
```

`splice()`:三个参数{起始位置，移除的元素个数，添加的元素（多个）}

```js
const numbers = [1, 2, 3, 4, 5]
console.log(numbers.splice())                // -> remove all items

const numbers = [1, 2, 3, 4, 5]
console.log(numbers.splice(0,1))            // remove the first item

const numbers = [1, 2, 3, 4, 5, 6];
console.log(numbers.splice(3, 3, 7, 8, 9))  // -> [1, 2, 3, 7, 8, 9] //it removes three item and replace three items
```

`push()`:添加元素到已存在序列尾     `pop()`:移除返回对尾元素

```js
const arr = []
const arr  = ['item1', 'item2','item3']
arr.push('new item')

console.log(arr) // ['item1', 'item2','item3','new item']
```

`shift()`:从队头移除元素     	`unshift()`:从队头添加元素

```js
const numbers = [1, 2, 3, 4, 5]
numbers.shift() // -> remove one item from the beginning

console.log(numbers) // -> [2,3,4,5]
```

`reverse()`:反转

`sort()`:排序（默认递增）

## Loop

for of 循环

```js
const number = [1,2,3,4,5]
for(const num of number){
    console.log(num*num)
}
```

循环打印金字塔

```js
for(let i = 1;i<7;i++){
    for (let j=0;j<i;j++){
        document.write('#');
    }
    document.write('<br>');//注意在页面打印用<br>作换行
}
```

生成随机字符串

```js
Math.random().toString(36).substring(2)
//toString将随机数转化为36进制，subString截取前两位（0.）
```

```js
//随机生成不定长字符串（制定10-18位）
for (let j = 0;j<10;j++){
let len = Math.random()*8+10;//生成长度10-18的数
for (let i =0;i<len;i++){
    let str = Math.random().toString(36).substring(2,3);//这里就取一个字符
    document.write(str);
}
document.write('<br>')
}
```

```js
//稍作修改生成16进制数（4位）
for (let j = 0;j<10;j++){
document.write('#');
for (let i =0;i<4;i++){
    let str = Math.random().toString(16).substring(2,3);
    document.write(str);
}
document.write('<br>')
}
```

```js
//按格式要求生成rgb数：    rgb(233,12,123)
for (let j = 0;j<10;j++){
        let num1 = Math.round(Math.random()*255);
        let num2 = Math.round(Math.random()*255);
        let num3 = Math.round(Math.random()*255);
        document.write(`rgb(${num1},${num2},${num3})`)
    document.write('<br>')
}
```

```js
//通过给定的字符串序列，求出每个元素的长度
//['Chian','hands','name','rounds']
const arr = ['Chian','hands','name','rounds']
const len = []
for (let i=0;i<arr.length;i++){
    len.push(arr[i].length)
}
document.write(len)
```

## Function

参数 长度不定

```js
function sumAllNums(){
    let sum = 0
    for (let i = 0;i<arguments.length;i++){
        sum+=arguments[i]
    }
    return sum
}

console.log(sumAllNums(1,2,3,4,5,5))
console.log(sumAllNums(223,14,12,4,2))
```

### Arrow  Function

```js
const sumAllNums =(...arguments)=>{
    console.log(arguments)
}
sumAllNums(1,2,3,4,5)
```

### Anonymous Function

```js
const af  = function(){
    console.log('wwwwww')
}
af()
```

### Expression Function

```js
const square = function(n){
    return n*n
}
console.log(square(2))
```

### Self Involking Function

(函数定义)(参数)  定义同时能计算，但返回值不能保留

```js
(function(n){
    console.log(n*n)
})(2)
```

```js
let squaredNum = (function(n){
    return n*n
})(10)
```

**常规函数定义**

```js
function square(n){
    return n*n
}
console.log(square(3))

const square2 = n =>{
    return n*n
}
console.log(square2(4))
// const 函数名 = 参数 => 返回值
const square3 = n =>n*n
console.log(square3(5))
```

### 默认参数函数

```js
function fName(param = defaultValue){//定义时带有默认参数
    //codes
}
fName()
fName(arg)
```

带有默认参数的表达式函数

```js
const 函数名 = (param= 默认参数) =>{
    //cod
}
```

练习

```js
function showDateTime(){
    const now = new Date();
    const year = now.getFullYear()
    let mon = now.getMonth()
    const day = now .getDay()
    const hour = now.getUTCHours()
    const min = now.getMinutes()
    mon = parseInt(mon)+1
    console.log(`${year}-${mon}-${day} ${hour}:${min}`)
}

showDateTime()      //Thu Jan 13 2022 20:37:07 GMT+0800 (中国标准时间)
//转换为标准格式  年 月 日  小时：分钟
```

```js
//实现列表内元素累加
const numbers = [1,2,3,4]
const sumArray = arr =>{
    let sum = 0
    const callback =function(element){
        sum +=element
    }
    arr.forEach(callback)
    return sum
}

console.log(sumArray(numbers))
```

### Functional Programming

#### forEach

```js
let sum =0
const numbers=[1,2,3,4]
numbers.forEach(num => sum+=num)
console.log(sum)
```

#### map

如何将一个列表的单纯全部转化为大写

```js
const countries =[
    'china','england','america',
]

const countriesToUpperCase = countries.map((country)=>country.toUpperCase())
console.log(countriesToUpperCase)
```

#### filter

筛选

```js
const countries =[
    'china','england','america',
]

const countriesFilter =  countries.filter((country) => country.includes('na'))
console.log(countriesFilter)
```

#### reduce

```js
arr.reduce((acc, cur) => {
  // some operations goes here before returning a value
 return 
}, initialValue)
```

```js
const numbers = [1, 2, 3, 4, 5]
const sum = numbers.reduce((acc, cur) => acc + cur, 0)

console.log(sum)
```

```js
15
```

#### every

检测每一个元素是否满足然后返回Booleam

```js
const bools = [true, true, true, true]
const areAllTrue = bools.every((b) => b === true) // Are all true? 

console.log(areAllTrue) // true
```

#### find

```js
const ages = [24, 22, 25, 32, 35, 18]
const age = ages.find((age) => age < 20)

console.log(age)
```

#### findIndex

```js
const names = ['Asabeneh', 'Mathias', 'Elias', 'Brook']
const ages = [24, 22, 25, 32, 35, 18]

const result = names.findIndex((name) => name.length > 7)
console.log(result) // 0

const age = ages.findIndex((age) => age < 20)
console.log(age) // 5
```

#### some

```js
const names = ['Asabeneh', 'Mathias', 'Elias', 'Brook']
const bools = [true, true, true, true]

const areSomeTrue = bools.some((b) =>  b === true)

console.log(areSomeTrue) //true
```

#### sort

区分对象，字符串，数值的sort

```js
//Sorting string values
const products = ['Milk', 'Coffee', 'Sugar', 'Honey', 'Apple', 'Carrot']
console.log(products.sort()) // ['Apple', 'Carrot', 'Coffee', 'Honey', 'Milk', 'Sugar']
```

```js
//sorting Numeric numbers
//如果不加参数的话会导致数值转化为字符串比较，这是100<23，因为100开头为1
//采用如下方法
const numbers = [9.81, 3.14, 100, 37]
// Using sort method to sort number items provide a wrong result. see below
console.log(numbers.sort()) //[100, 3.14, 37, 9.81]
numbers.sort(function (a, b) {
  return a - b
})

console.log(numbers) // [3.14, 9.81, 37, 100]

numbers.sort(function (a, b) {
  return b - a
})
console.log(numbers) //[100, 37, 9.81, 3.14]
```



### document

每个载入浏览器的 HTML 文档都会成为 Document 对象。

Document 对象使我们可以从脚本中对 HTML 页面中的所有元素进行访问。

例子

```html
<!--实时获取时间并刷新，直到手动停止-->
<!DOCTYPE html>
<html>
    <body>
        <input type="text" id="clock" size="35"/>
        <script language = javascript>
            var int = self.setInterval("clock()",50)
            function clock()
            {
                var t =new Date()
                document.getElementById("clock").value=t
            }
        </script>
        </form>
        <button onclick="int = window.clearInterval(int)">stop interval</button>
    </body>
</html>
```



## Object

### 生存范围

变量的生存空间为：全局，局部，窗口，任何不是const,let,var都是窗口范围

在函数内（if，loop语句）内定义的变量不会超出外部

```js
const Person ={			//创建对象   object ={   ...}
    firstName : 'Ash',	//逗号分割
    lastName : 'Fire',
    age : 22,
    skills : [			//列表
        'HTML',
        'CSS',
        'JavaScript',
        'Node'
    ],
    getFullName : function(){		//定义函数
        return `${this.firstName} ${this.lastName}`
    },
    'phone number':'18888888888'
}
```

### Object 方法

一些Object方法

> Object.assign()
>
> Object.keys()
>
> Object.values()
>
> Object.entries()

```js
const person = {
  firstName: 'Asabeneh',
  age: 250,
  country: 'Finland',
  city:'Helsinki',
  skills: ['HTML', 'CSS', 'JS'],
  title: 'teacher',
  address: {
    street: 'Heitamienkatu 16',
    pobox: 2002,
    city: 'Helsinki'
  },
  getPersonInfo: function() {
    return `I am ${this.firstName} and I live in ${this.city}, ${this.country}. I am ${this.age}.`
  }
}

//Object methods: Object.assign, Object.keys, Object.values, Object.entries
//hasOwnProperty

const copyPerson = Object.assign({}, person)
console.log(copyPerson)
```

```
 Object
address:
city: "Helsinki"
pobox: 2002
street: "Heitamienkatu 16"
[[Prototype]]: Object
age: 250
city: "Helsinki"
country: "Finland"
firstName: "Asabeneh"
getPersonInfo: ƒ ()
skills: (3) ['HTML', 'CSS', 'JS']
title: "teacher"
[[Prototype]]: Object
```

## 10.Set

```js
//创建
let a = [1,2,3,4]
let A = new Set(a)
//增加、删除元素、清空集合
A.add(5)
A.delete(2)
A.has(1)
A.clear()
//筛选(交集)
let a = [1, 2, 3, 4, 5]
let b = [3, 4, 5, 6]
let A = new Set(a)
let B = new Set(b)

let c = a.filter((num) => B.has(num))
let C = new Set(c)//[3,4,5]
//做差
let a = [1, 2, 3, 4, 5]
let b = [3, 4, 5, 6]
let A = new Set(a)
let B = new Set(b)

let c = a.filter((num) => !B.has(num))
let C = new Set(c)
console.log(C)//{1,2}
```

### map

```js
//创建空map
const map = new Map()
//根据Array 创建Map
countries = [
  ['Finland', 'Helsinki'],
  ['Sweden', 'Stockholm'],
  ['Norway', 'Oslo'],
]
const map = new Map(countries)
console.log(map)
console.log(map.size)
//添加新元素，用set
const countriesMap = new Map()
countriesMap.set('Finland','Helsinki')
countriesMap.set('Sweden','Stockholm')
//根据key得到value
console.log(countriesMap.get('Finland'))//Helsinki
//打印全部--->输出多个array，每个包含两元素
for(const country of countriesMap){
    console.log(country)
}
//注意这与上写法不一样的输出---》打印四行字符串输出
for(const[country, city] of countriesMap){
    console.log(country, city)
}
```

## 11.Destructuring

### Destructing Arrays

```js
  const numbers = [1, 2, 3]
  let [numOne, numTwo, numThree] = numbers

  console.log(numOne, numTwo, numThree)
```

```sh
  1 2 3
```

We can not assign variable to all the elements in the array. We can destructure few of the first and we can get the remaining as array using spread operator(...).

```js
const nums = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
let [num1, num2, num3, ...rest] = nums

console.log(num1, num2, num3)
console.log(rest)
```

```sh
1 2 3
[4, 5, 6, 7, 8, 9, 10]
```

同时改名

```js
const rectangle = {
    width:20,
    height:10,
    area:200
}
let {width:w, height:h ,area:a, perimeter: p} = rectangle
console.log(w,h,a,p)
```

包含函数

```js
const rect = {
    width : 20,
    height: 10
}
const fun = rectangle =>{
    return 2*(rectangle.width+rectangle.height)
}
console.log(fun(rect))
```

```js
//Another Example
const person = {
  firstName: 'Asabeneh',
  lastName: 'Yetayeh',
  age: 250,
  country: 'Finland',
  job: 'Instructor and Developer',
  skills: [
    'HTML',
    'CSS',
    'JavaScript',
    'React',
    'Redux',
    'Node',
    'MongoDB',
    'Python',
    'D3.js'
  ],
  languages: ['Amharic', 'English', 'Suomi(Finnish)']
}
// Lets create a function which give information about the person object without destructuring

const getPersonInfo = obj => {
  const skills = obj.skills
  const formattedSkills = skills.slice(0, -1).join(', ')
  const languages = obj.languages
  const formattedLanguages = languages.slice(0, -1).join(', ')

  personInfo = `${obj.firstName} ${obj.lastName} lives in ${obj.country}. He is  ${
    obj.age
  } years old. He is an ${obj.job}. He teaches ${formattedSkills} and ${
    skills[skills.length - 1]
  }. He speaks ${formattedLanguages} and a little bit of ${languages[2]}.`

  return personInfo
}

console.log(getPersonInfo(person))
```

**`slice(0,-1)`表示取整个列表**

在for循环

```js
const todoList = [
{
  task:'Prepare JS Test',
  time:'4/1/2020 8:30',
  completed:true
},
{
  task:'Give JS Test',
  time:'4/1/2020 10:00',
  completed:false
},
{
  task:'Assess Test Result',
  time:'4/1/2020 1:00',
  completed:false
}
]

for (const {task, time, completed} of todoList){//尝试了下这里不需要按顺序
  console.log(task, time, completed)
}
```

用分隔符拷贝

```js
const evens = [0, 2, 4, 6, 8, 10]
const evenNumbers = [...evens]
//拷贝全部
const frontEnd = ['HTML', 'CSS', 'JS', 'React']
const backEnd = ['Node', 'Express', 'MongoDB']
const fullStack = [...frontEnd, ...backEnd]
console.log(fullStack)
```

用于拷贝对象

```js
const user  = {
    Name : 'Abe',
    title : 'ps'
}

const copyed = {...user}
```

拷贝同时替换

```js
const user = {
  name:'Asabeneh',
  title:'Programmer',
  country:'Finland',
  city:'Helsinki'
}

const copiedUser = {...user, title:'instructor'}//同时修改
console.log(copiedUser)
```

利用分隔符接受不定长参数

```js
const sumAllNums = (...args) => {
  let sum = 0
  for (const num of args){
    sum += num
  }
  return sum
  
}

console.log(sumAllNums(1, 2, 3,4,5))
```

## 12.regular Expressions

