# 对象
   JavaScript的简单类型包括数字、字符串、布尔值、null和undefined值，其他所有的值都是对象。
   对象的属性：反映该对象某些特定的性质的，如：字符串的长度、图像的长宽等；
   对象的方法：能够在对象上执行的动作。例如，表单的“提交”(Submit)，时间的“获取”(getYear)等；
   JavaScript 提供多个内建对象，比如 String、Date、Array 等等，使用对象前先定义，如下使用数组对象：
   var objectName =new Array();//使用new关键字定义对象
   或者
   var objectName =[];
   1. 访问对象属性的语法:
   objectName.propertyName
   2. 访问对象的方法：
   objectName.methodName()

   对象是属性的容器,每个属性都用户名字和值，JavaScript里的对象是无类型的。
   对象适用于汇集和管理数据。
   JavaScript包含一种原型链的特性，允许对象继承另一个对象的属性，正确地使用它能减少对象初始化时消耗的时间和内存。
1. 对象字面量 Object Literals
     一个对象字面量就是包围在一对花括号中的零或多个'名/值'对。对象字面量可以出现在任何允许表达式出现的地方
     对象可嵌套
2. 检索 Retrieval
    stooge["firstname"]
    stooge.firstname
    ||运算符可以用来填充默认值
    var middle = stooge["middle-name"]||"(none)";
    var middle = stooge["middle-name"]||"unknown";
    从undefined的成员属性中取值会导致TypeError异常。这时可以通过&&运算符来避免错误
    stooge.equipment           //undefined
    stooge.equipment.model           //undefined
    stooge.equipment && stooge.equipment.model           //undefined
3. 更新 Update
    对象里的值通过赋值语句来更新，如果属性名已经存在于对象里，那么这个属性的值会被替换。
4. 引用 Reference
5. 原型 Prototype
    每个对象都连接到一个原型对象，并可以从中继承属性,所有通过对象字面量创建的对象都连接到Object.prototype，它是javascript中的标配对象。
    Object的create方法  创建一个使用原对象作为其原型的对象。
    原型关系是一种动态的关系。添加一个新的属性到原型中，该属性会立即对所有基于该原型创建的对象可见。
    什么是原型链：
    原型链，所有的原型构成了一个链条，这个链条我们称之为原型链（prototype chain)。
    如果我们执行下面这段代码,因为没有定义address这个属性，程序结果理所当然的是undefined。
let obj = {
    name : 'harry',
    age:18
}
console.log(obj.address);  //undefined
这个时候经历了什么呢？JS引擎线从Obj.address里寻找，发现没有找到，然后接着去找obj.__ proto __ 里面寻找，发现还是没找到，所以结果为undefined。我们可以给obj.__ proto __ 赋值
let obj = {
    name : 'harry',
    age:18
}
obj.__proto__ = {
    address:'上海'
}
console.log(obj.address); //上海
或者这样
obj.__proto__ = {
    //这里一定要开辟一个空间，不能直接写obj.__proto__.__proto__ = {}
}
obj.__proto__.__proto__= {
    address:'上海'
}
console.log(obj.address); //上海
接着套娃
let obj = {
    name : 'harry',
    age:18
}

obj.__proto__ = {

}
obj.__proto__.__proto__= {
    
}
obj.__proto__.__proto__.__proto__= {
    address:'上海'
}
console.log(obj.address); //上海

js引擎会顺着这些原型不断的往上找，直到address这个属性。这些原型构成了原型链。
6. 反射 Reflection
    原型链中的任何属性都会产生值，处理掉一些不需要的属性的方法：
      1. 让你程序做检查并丢弃值为函数的属性
      2. hasOwnProperty方法，如果对象拥有独有的属性，它将返回true。hasOwnPrototype方法不会检查原型链
      flight.hasOwnProperty('number')   //true
      flight.hasOwnProperty('constructor')   //true
7. 枚举 Enumeration
    for in语句可用来遍历一个对象中的所有属性名。该枚举过程将会列出所有的属性——包括函数和原型中的属性
    所以要过滤掉不想要的值
    就可以用到hasOwnProperty方法，以及typeof来排除函数：
    var name;
    for (name in another_stooge){
      if(typeof another_stooge[name] !=='function'){
        document.write(name + ':' + another_stooge[name]);
      }
    }
    属性名出现的顺序是不确定的，最好避免使用for in 而是创建一个数组，在其中以正确的顺序包含属性名
    可以得到我们想要的属性，而不用担心可能发掘出原型链中的属性，并且可以按正确的顺序取得了它们的值。
8. 删除 Delete
    删除对象的属性可能会让来自原型链中的属性透现出来
9. 减少全局变量污染
    全局变量削弱了程序的灵活性，应该避免使用。
    最小化使用全局变量：为应用只创建一个唯一的全局变量
    只要把全局性的资源都纳入一个名称空间下，程序与其他应用程序、组件或类库之间发生冲突的可能性就会显著降低
    


    


  
