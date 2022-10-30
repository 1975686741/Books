# Object 对象

**- Date 日期对象**

     定义一个时间对象 :
     var Udate=new Date(); 
     注意:使用关键字new，Date()的首字母必须大写。
     方法名称                功能描述
   get/setDate()        返回/设置日期
   get/setFullYear()    返回/设置年份，用四位数表示
   get/setYear()        返回/设置年份，两位数表示
   get/setMonth()       返回/设置月份。0：一月···11：十二月，所以要+1
   get/setDay()         返回/设置星期。返回的是0-6的数字，0 表示星期天。
   get/setHours()       返回/设置小时，24小时制
   get/setminutes()     返回/设置分钟数
   get/setSeconds()     返回/设置秒钟数
   get/setTime()        返回/设置时间(毫秒)

**- String 字符串对象**
     toUpper/LowerCase()  字符串大/小写
     str.charAt()   返回指定位置的字符(0~str.length-1)
     str.indexOf(substring,b)  字符在字符串中首次出现的位置 b:字符串开始检索的位置，省略则从首字符开始
     str.split('',num)  字符串分割  '':分割的地方  num:分割几下
     str.substring(num1,num2) 提取字符串两个指定下标之间的字符 没有num2则提取num1后面全部字符
     str.substr(num1,num2)  提取指定数目的字符串 num1：起始位置 num2:数目，没有则num1后面全部

**- Math对象**
     Math 对象用于执行数学任务。
     Math 对象并不像 Date 和 String 那样是对象的类，因此没有构造函数Math()
     语法
         var x = Math.PI;   // 返回 PI
         var y = Math.sqrt(16);   // 返回 16 的平方根
    1. Math对象属性
属性	描述
E	返回算术常量 e，即自然对数的底数（约等于2.718）。
LN2	返回 2 的自然对数（约等于0.693）。
LN10	返回 10 的自然对数（约等于2.302）。
LOG2E	返回以 2 为底的 e 的对数（约等于 1.4426950408889634）。
LOG10E	返回以 10 为底的 e 的对数（约等于0.434）。
PI	返回圆周率（约等于3.14159）。
SQRT1_2	返回 2 的平方根的倒数（约等于 0.707）。
SQRT2	返回 2 的平方根（约等于 1.414）。
   2. Math对象方法
方法	描述
abs(x)	返回 x 的绝对值。
acos(x)	返回 x 的反余弦值。
asin(x)	返回 x 的反正弦值。
atan(x)	以介于 -PI/2 与 PI/2 弧度之间的数值来返回 x 的反正切值。
atan2(y,x)	返回从 x 轴到点 (x,y) 的角度（介于 -PI/2 与 PI/2 弧度之间）。
ceil(x)	对数进行上舍入。
cos(x)	返回数的余弦。
exp(x)	返回 Ex 的指数。
floor(x)	对 x 进行下舍入。
log(x)	返回数的自然对数（底为e）。
max(x,y,z,...,n)	返回 x,y,z,...,n 中的最高值。
min(x,y,z,...,n)	返回 x,y,z,...,n中的最低值。
pow(x,y)	返回 x 的 y 次幂。
random()	返回 0 ~ 1 之间的随机数。
round(x)	四舍五入。
sin(x)	返回数的正弦。
sqrt(x)	返回数的平方根。
tan(x)	返回角的正切。
tanh(x)	返回一个数的双曲正切函数值。
trunc(x)	将数字的小数部分去掉，只保留整数部分。
 **- Array 数组对象**
     数组对象是一个对象的集合，里边的对象可以是不同类型的。数组的每一个成员对象都有一个“下标”，用来表示它在数组中的位置，是从零开始的。
 数组定义的方法：
1. 定义了一个空数组:
var  数组名= new Array();
2. 定义时指定有n个空元素的数组：
var 数组名 =new Array(n);
3. 定义数组的时候，直接初始化数据：
var  数组名 = [<元素1>, <元素2>, <元素3>...];
我们定义myArray数组，并赋值，代码如下：
var myArray = [2, 8, 6]; 
说明：定义了一个数组 myArray，里边的元素是：myArray[0] = 2; myArray[1] = 8; myArray[2] = 6。
数组元素使用：
数组名[下标] = 值;
注意: 数组的下标用方括号括起来，从0开始。
数组方法
下表列出了一些常用的数组方法：
序号	方法 & 描述	实例
1.	concat()
连接两个或更多的数组，并返回结果。
var alpha = ["a", "b", "c"]; 
var numeric = [1, 2, 3];
var alphaNumeric = alpha.concat(numeric); 
console.log("alphaNumeric : " + alphaNumeric );    // a,b,c,1,2,3   
2.	every()
检测数值元素的每个元素是否都符合条件。
function isBigEnough(element, index, array) { 
        return (element >= 10); 
}        
var passed = [12, 5, 8, 130, 44].every(isBigEnough); 
console.log("Test Value : " + passed ); // false
3.	filter()
检测数值元素，并返回符合条件所有元素的数组。
function isBigEnough(element, index, array) { 
   return (element >= 10); 
}         
var passed = [12, 5, 8, 130, 44].filter(isBigEnough); 
console.log("Test Value : " + passed ); // 12,130,44
4.	forEach()
数组每个元素都执行一次回调函数。
let num = [7, 8, 9];
num.forEach(function (value) {
    console.log(value);
}); 
编译成 JavaScript 代码：
var num = [7, 8, 9];
num.forEach(function (value) {
    console.log(value);  // 7   8   9
});
5.	indexOf()
搜索数组中的元素，并返回它所在的位置。
如果搜索不到，返回值 -1，代表没有此项。
var index = [12, 5, 8, 130, 44].indexOf(8); 
console.log("index is : " + index );  // 2
6.	join()
把数组的所有元素放入一个字符串。
var arr = new Array("Google","Runoob","Taobao");         
var str = arr.join(); 
console.log("str : " + str );  // Google,Runoob,Taobao       
var str = arr.join(", "); 
console.log("str : " + str );  // Google, Runoob, Taobao        
var str = arr.join(" + "); 
console.log("str : " + str );  // Google + Runoob + Taobao
7.	lastIndexOf()
返回一个指定的字符串值最后出现的位置，在一个字符串中的指定位置从后向前搜索。
var index = [12, 5, 8, 130, 44].lastIndexOf(8); 
console.log("index is : " + index );  // 2
8.	map()
通过指定函数处理数组的每个元素，并返回处理后的数组。
var numbers = [1, 4, 9]; 
var roots = numbers.map(Math.sqrt); 
console.log("roots is : " + roots );  // 1,2,3
9.	pop()
删除数组的最后一个元素并返回删除的元素。
var numbers = [1, 4, 9];       
var element = numbers.pop(); 
console.log("element is : " + element );  // 9         
var element = numbers.pop(); 
console.log("element is : " + element );  // 4
10.	push()
向数组的末尾添加一个或更多元素，并返回新的长度。
var numbers = new Array(1, 4, 9); 
var length = numbers.push(10); 
console.log("new numbers is : " + numbers );  // 1,4,9,10 
length = numbers.push(20); 
console.log("new numbers is : " + numbers );  // 1,4,9,10,20
11.	reduce()
将数组元素计算为一个值（从左到右）。
var total = [0, 1, 2, 3].reduce(function(a, b){ return a + b; }); 
console.log("total is : " + total );  // 6
12.	reduceRight()
将数组元素计算为一个值（从右到左）。
var total = [0, 1, 2, 3].reduceRight(function(a, b){ return a + b; }); 
console.log("total is : " + total );  // 6
13.	reverse()
反转数组的元素顺序。
var arr = [0, 1, 2, 3].reverse(); 
console.log("Reversed array is : " + arr );  // 3,2,1,0
14.	shift()
删除并返回数组的第一个元素。
var arr = [10, 1, 2, 3].shift(); 
console.log("Shifted value is : " + arr );  // 10
15.	slice()
选取数组的的一部分，并返回一个新数组。
var arr = ["orange", "mango", "banana", "sugar", "tea"]; 
console.log("arr.slice( 1, 2) : " + arr.slice( 1, 2) );  // mango
console.log("arr.slice( 1, 3) : " + arr.slice( 1, 3) );  // mango,banana
16.	some()
检测数组元素中是否有元素符合指定条件。
function isBigEnough(element, index, array) { 
   return (element >= 10);          
}           
var retval = [2, 5, 8, 1, 4].some(isBigEnough);
console.log("Returned value is : " + retval );  // false         
var retval = [12, 5, 8, 1, 4].some(isBigEnough); 
console.log("Returned value is : " + retval );  // true
17.	sort()
对数组的元素进行排序。
var arr = new Array("orange", "mango", "banana", "sugar"); 
var sorted = arr.sort(); 
console.log("Returned string is : " + sorted );  // banana,mango,orange,sugar
18.	splice()
从数组中添加或删除元素。
var arr = ["orange", "mango", "banana", "sugar", "tea"];  
var removed = arr.splice(2, 0, "water");  
console.log("After adding 1: " + arr );    // orange,mango,water,banana,sugar,tea 
console.log("removed is: " + removed);           
removed = arr.splice(3, 1);  
console.log("After removing 1: " + arr );  // orange,mango,water,sugar,tea 
console.log("removed is: " + removed);  // banana
19.	toString()
把数组转换为字符串，并返回结果。
var arr = new Array("orange", "mango", "banana", "sugar");         
var str = arr.toString(); 
console.log("Returned string is : " + str );  // orange,mango,banana,sugar
20.	unshift()
向数组的开头添加一个或更多元素，并返回新的长度。
var arr = new Array("orange", "mango", "banana", "sugar"); 
var length = arr.unshift("water"); 
console.log("Returned array is : " + arr );  // water,orange,mango,banana,sugar 
console.log("Length of the array is : " + length ); // 5
    


