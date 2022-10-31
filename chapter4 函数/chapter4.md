# 函数
     函数用于指定对象的行为。一般来说，所谓的编程就是将一组需求分解成一组函数与数据结构的技能。
- 函数字面量
     1. 函数对象通过函数字面量来创建：
         var add = function (a,b){
           return a+b;
         };
     2. 函数字面量包括4个部分：保留字function、函数名、包围在圆括号中的一组参数和包围在花括号中的一组语句。
     3. 通过函数字面量创建的函数对象包含一个连到外部上下文的连接。这被称为 闭包(closure)。
- 调用
       1. 除了声明时定义的形式参数，每个函数还接收两个附加的参数：this和arguments。参数this的值取决于调用的模式。JavaScript中一共有四种调用模式：1.方法调用模式、2.函数调用模式、3。构造器调用模式和4.apply调用模式。这些模式在如何初始化关键参数this上存在差异。
       2. 调用运算符是跟在任何产生一个函数值的表达式之后的一对圆括号。圆括号内可包含零个或多个用逗号隔开的表达式。每个表达式产生一个参数值。每个参数值被赋予函数声明时定义的形式参数名。
       3. 当实参的个数和形参的个数不匹配时，不会导致运行错误。但是如果实参值过多了，超出的参数值会被忽略。如果实参过少，缺少的值会被替换为undefined。
       对参数值不会进行类型检查：任何类型的值都可以被传递给任何参数。
  1. 方法调用模式
     当一个函数被保存为对象的一个属性时，我们称它为一个方法。当一个方法被调用时，this被绑定到该对象。
     如果调用表达式包含一个提取属性的动作（即包含一个.点表达式或[subscript]下标表达式），那么它就是被当作一个方法来调用。
     this到对象的绑定发生在调用的时候。这个“超级”延迟绑定使得函数可以对this高度复用。通过this可取得它们所属对象的上下文的方法称为公共方法
  2. 函数调用模式
     var sum = add(3，4);    //sum的值为7.
     当一个函数并非一个对象的属性时，那么它就是被当作一个函数哎调用的：
     以此模式调用函数时，this被绑定到全局对象。这个语言设计上的一个错误。如果正确的话，当内部函数被调用时，this应该仍然绑定到外部函数this变量。这个错误的后果就是 方法不能利用内部函数来帮助它工作，因为颞部函数的this被绑定了错误的值，所以不能共享该方法对对象的访问权。
     那么思考一下：如果该方法定义一个变量并给它赋值为this，那么内部函数就可以通过那个变量访问到this。我们把这个变量命名为that：
     //给myObject增加一个double方法
     myObject.double = function(){
        var that = this;    //解决方法
        var helper = function(){
            that.value = add(that.value,that.value);
        };
        help();   //以函数的形式调用helper
     }；
     //以方法的形式调用double
     myObject.double();
     document.write(myObject.value);    //6
  3. 构造器调用模式
     如果在一个函数前面带上new来调用，那么背地里将会创建一个连接到该函数的prototype成员的新对象，同时this会被绑定到那么新对象上。   new前缀也会改变return语句的行为。
         //创建一个名为Quo的构造器函数。它构造一个带有status属性的对象
         var Quo = function(string){
            this.status = string;
         };
         //给Quo的所有实例提供一个名为get_status的公共方法
         Quo.prototype.get_status = function(){
            return this.status;
         };
         //构造一个Quo实例
         var myQuo = new Quo("confused");
         document.write(myQuo.get_status());   //打印显示"confused"
     如果一个函数，创建的目的就是希望结合new前缀来调用，那么它就被称为构造器函数。
     一般不推荐。
   4. Apply调用模式
     apply方法让我们可以 构建一个参数数组传递给调用模式。它也允许我们选择this的值。apply方法接受两个参数，第1个是要绑定给this的值，第2个就是第一个参数数组。
     //构造一个包含两个数字的数组，并将它们相加
     var array = [3,4];
     var sum = add.apply(null,array);   //sum值为7
     //构造一个包含status成员的对象
     var statusObject = {
        status: 'A-OK'
     };
     //statusObject并没有继承自Quo.peototype，但我们可以在statusObject上调用get_status方法，尽管statusObject并没有一个名为get_status的方法
     //var status = Quo.prototype.get_status.apply(statusObject);
     //status值为'A-OK'



