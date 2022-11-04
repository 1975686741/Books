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
- 参数
     1. 当函数被调用时，会得到一个“免费”配送的参数，就是arguments数组。
     函数可以通过此参数访问所有它被调用时传递给它的参数列表，包括那些没有被分配给函数声明时定义的形式参数的多余参数。
- 返回
      1. return语句可用来使函数提前返回。当return被执行时，函数立即返回而不再执行余下的语句。
     如果函数调用时在前面加上了new前缀，且返回值不是一个对象，则返回this（该新对象）。
- 异常
       throw{
        name:'TypeError',
        message:'add needs numbers'
       } 
     throw语句中断函数的执行。
- 扩充类型的功能
     1. 通过给Object.prototype添加方法，可以让该方法对所有对象都可用。这样的方式对函数、数组、字符串、数字、正则表达式和布尔值同样适用。
     2. 通过Function.prototype增加方法来使得该方法对所有函数可用：
     Function.prototype.method = function (name,func){
        this.peototype[name] = func;
        return this;
     }
     通过给Function.prototype增加一个method方法，我们下次给对象增加方法的时候就不必键入prototype这几个字符，节省了时间。
     给Number.prototype增加一个integer方法，根据数字的正负来判断是使用Math.ceil还是Math.floor：
     Number.method('integer',function(){
        return Math[this<0 ? 'ceil' : 'floor'](this);
     });
     document.writeln((-10 / 3).integer());     //-3
     3. JavaScript缺少一个移除字符串首尾空白的方法。这个小疏忽很容易弥补：
      String.method('trim',function(){
        return this.replace(/^\s+|\s+$/g,'');
      });
      document.writeln('"' + "neat".trim() + '"');
      我们的trim方法使用了一个正则表达式
      通过给基本类型增加方法，我们可以极大地提高语言的表现力。因为JavaScript原型继承的动态本质，新的方法立刻被赋予到所有的对象实例上，哪怕对象实例是在方法被增加之前就创建好了。
      基本类型的原型是公用结构，所以在类库混用时务必小心一个保险的做法就是只在确定没有该方法时才添加它。

      //  符合条件时才增加方法
      Function.prototype.method = funtion(name,func){
        if(!this.prototpe[nmae]){
            this.prototype[name] = func;
        }
        return this;
      };
      另一个要注意的就是 for in语句用在原型上时表现德会很糟糕。第三章中学习过几个可以减轻这个问题的影响的方法： 可以使用hasOwnproperty方法筛选出继承而来的属性，或者我们可以查找特定的类型。
- 递归
      1. 递归函数就是会直接或间接地调用自身地一种函数
      2. 递归是一种强大的编程技术，它把一个问题分解为一组相似的子问题，每一个都用一个【寻常解】去解决。一般来说一个递归函数调用自身去解决它的子问题。
      3. 递归函数可以非常高效的操作树形结构，比如浏览器端的文档对象模型（dom）。每一次递归调用时处理指定的树的一小段。
         //定义walk_the_DOM函数，它从某个指定的节点开始，按HTNL源码中的顺序访问该树的每个节点
         //它会调用一个函数，并依次传递每个节点给它。walk_the_DOM调用自身去处理每一个子节点

         var walk_the_DOM = funcion walk(node,func){
            func(node);
            node = node.firstChild;
            while(node){
                walk(node,func);
                node=node.nextSibling;
            }
         };
         //定义 grtElementsByAttribute函数。它以一个属性名称字符串和一个可选的匹配值作为参数
         //它调用walk_the_DOM，传递一个用来查找节点属性名的函数
         //匹配的节点会累加到一个结果数组中

           var grtElementsByAttribute = function (alt,value){
            var results = [];

            walk_the_DOM(document.body,function (node){
                var actual = node.nodeType === 1 && node.getAttribute(att);
                if(typeOf actual === 'string' && (actual === value || typeOf value !== 'string'))
                results.push(node);
                }
            });
            return results;
         }
- 作用域  
      1. 作用域控制着变量与参数的可见性及生命周期。对程序员来说这是一项重要的服务，因为它减少了名称冲突，并且提供了自动内存管理。
        var  foo = function(){
            var a = 3, b = 5;
            var bar = function(){
                var b =7,c=11;    //此时 a为3，b为7，c为11
                a += b+c;         //此时 a为21，b为7，c为11
            };
                                  //此时 a为3，b为5，c还没有定义
            bar();                //此时 a为21，b为5
        }；
      2. 大多数c语言语法的语言都拥有块级作用域。在一个代码块中（括在一对花括号中的一组语句）定义的所有变量在代码块的外部是不可见的。定义在代码块中的变量在代码块执行结束之后会被释放掉。这是件好事，然而糟糕的是：尽管javascript的代码块语法貌似支持块级作用域，但实际上JavaScript并不支持。
      3. JavaScript确实有函数作用域。那意味着函数内部任何位置定义的变量，在该函数内部任何地方都可见。很多现代语言都推荐尽可能延迟声明变量。而用在JavaScript上的话却会成为糟糕的建议，因为它缺少块级作用域。 最好的做法就是在函数体的顶部声明函数中可能用到的所有变量
- 闭包
       1. 作用域的好处是：内部函数可以访问定义它们的外部函数的参数和变量（除了this和arguemnts）
       2. 内部函数比外部函数拥有更长的生命周期
       3. 和以对象字面量形式去初始化myObject不同，通过调用一个函数的形式去初始化myObject，该函数会返回一个对象字面量。函数里定义了一个value变量，该变量对increment和getValue方法总是可用的，但函数的作用域使得它对其他程序来说是不可见的
          var myObject = (function(){
            var value = 0;
            return{
                increment:function(inc){
                    value += typeOf inc === 'number' ? inc : 1;
                },
                getValue : function(){
                    return value;
                }
            };
          }());
          我们并没有把一个函数赋值给myObject。我们是把调用该函数后返回的结果赋值给它。
          最后一行的()  该函数返回一个包含两个方法的对象，并且这些方法继续享有访问value变量的特权

         再来看一个更有用的例子：
         //定义一个函数，它设置一个DOM节点为黄色，然后把它渐变为白色
         var fade = function (node) {
            var level = 1;
            var step = function(){
                var hex = level.toString(16);
                node.style.backgroundColor = '#FFF' + hex + hex;
                if(level<15){
                    level += 1;
                    setTimeout(step,100);
                }
            };
            setTimeout(step,100);
         };
         fade(document.body);
         我们调用fade，把document.body作为参数传递给它（HTML<body>标签所创建的节点）fade函数设置level为1.它定义了一个step函数；接着调用setTimeout，并传递step函数和一个时间（100毫秒)给它。然后它返回，fade函数结束。
         在大约十分之一秒后，step函数被调用。它把fade函数的level变量转化为16位字符。接着，它修改fade函数得到的节点的背景颜色。然后查看fade函数的level变量。如果背景色尚未变成白色，那么它增大fade函数的level变量，接着用setTimeout预定让它自己再次运行。
         step函数很快再次被调用了。但这次，fade函数的level变量值变为2。fade函数在之前就已经返回了，但只要fade的内部函数需要，它的变量就会持续保留。
         为了避免下面的问题，理解内部函数能访问外部函数的实际变量而 无须复制是很重要的：

//糟糕的例子
//构造一个函数，用错误的方式给一个数组中的节点设置事件处理 
//当点击一个节点时，按照预期，应该弹出一个对话框显示节点的 
//但它总是会显示节点的数目。
var   add_t he_handlers   =   function  ( nodes )   {
var   i ;
for   ( i	=   0;	i	<   nodes.lengt h;	i	+=   1)   {
nodes [ i ] . onclick   =   function  ( e)   {
aler t( i ) ;
} ;
}
} ;
/ /   结束糟糕的例子。

add_the_handlers函数的本意是想传递给每个事件处理器一个唯一值 （i）。但它未能达到目的，因为事件处理器函数绑定了变量i本身，而 不是函数在构造时的变量i的值。
/ /   改良后的例子
/ /   构造一个函数，用正确的方式给一个数组中的节点设置事件处理 / /   点击一个节点，将会弹出一个对话框显示节点的序号。
var   add_t he_handlers   =   function  ( nodes )   {
var   helper   =   function( i )   {
return  function(e) {
alert ( i ) ;
} ;
} ;
var   i ;
for   ( i= 0;	i<   nodes . length;i	+=   1)   {
nodes [ i ] . onclick   =   helper ( i ) ;
}
} ;
避免在循环中创建函数，它可能只会带来无谓的计算，还会引起混 淆，正如上面那个糟糕的例子。我们可以先在循环之外创建一个辅助函 数，让这个辅助函数再返回一个绑定了当前i值的函数，这样就不会导 致混淆了。
- 回调
     1. 函数使得对不连续事件的处理变得更容易。例如，假定有这么一个 序列，由用户交互行为触发，向服务器发送请求，最终显示服务器的响 应。最自然的写法可能会是这样的：
request  =  prepare_the_request(   );
response  =  send_request _synchronously(request);
display( response);

这种方式的问题在于，网络上的同步请求会导致客户端进入假死状 态。如果网络传输或服务器很慢，响应会慢到让人不可接受。
更好的方式是发起异步请求，提供一个当服务器的响应到达时随即 触发的回调函数。异步函数立即返回，这样客户端就不会被阻塞。
request  =  prepare_the_request(   ) ;
send_r equest _asynchronously(request,function(response) {
display(response);
});
我们传递一个函数作为参数给send_request_asynchronously函数，一 旦接收到响应，它就会被调用。


- 模块 Module

1. 我们可以使用函数和闭包来构造模块。模块是一个提供接口却隐藏 状态与实现的函数或对象。通过使用函数产生模块，我们几乎可以完全 摒弃全局变量的使用，从而缓解这个JavaScript的最为糟糕的特性之一所 带来的影响。
举例来说，假定我们想要给String增加一个deentityify方法。它的任 务是寻找字符串中的HTML字符实体并把它们替换为对应的字符。这就 需要在一个对象中保存字符实体的名字和它们对应的字符。但我们该在 哪里保存这个对象呢？我们可以把它放到一个全局变量中，但全局变量 是魔鬼。我们可以把它定义在该函数的内部，但是那会带来运行时的损 耗，因为每次执行该函数的时候该字面量都会被求值一次。理想的方式 是把它放入一个闭包，而且也许还能提供一个增加更多字符实体的扩展 方法：

String. method( 'deentityify' ,	function(   ) {
/ /  字符实体表。它映射字符实体的名字到对应的字符。
varentity  = {
quot:' " ' ,
lt:	' <' ,
gt:	' >'
} ;
/ / 返回deentityify  方法。
return  function(   )   {
/ /   这才是  deentityify  方法。它调用字符串的  replace  方法，
/ /   查找‘   &’   开头和‘   ;’   结束的子字符串。如果这些字符可以在字 / /   那么就将该字符实体替换为映射表中的值。它用到了一个正则表
return this.replace( / &( [ ^&; ] +) ; / g,
 function  ( a,	b)   {
var   r  =   entity[ b] ;
return  typeOf   r  ===  'string'	?   r   :	a;
}
) ;
} ;
} (   ) ) ;


请注意最后一行。我们用(  )运算法立刻调用我们刚刚构造出来的函 数。这个调用所创建并返回的函数才是deentityify方法。
document. writeln(
'&lt;&quot; &gt ;'.deentityify(   ));/ / <" >

2. 模块模式利用了函数作用域和闭包来创建被绑定对象与私有成员的 关联，在这个例子中，只有deentityify方法有权访问字符实体表这个数 据对象。
模块模式的一般形式是：一个定义了私有变量和函数的函数；利用 闭包创建可以访问私有变量和函数的特权函数；最后回这个特权函 数，或者把它们保存到一个可访问到的地方。
使用模块模式就可以摒弃全局变量的使用。它促进了信息隐藏和其 他优秀的设计实践。对于应用程序的封装，或者构造其他单例(5)对象， 模块模式非常有效。
模块模式也可以用来产生安全的对象。假定我们想要构造一个用来 产生序列号的对象：
var   serial _maker = function(   ){
/ /   返回一个用来产生唯一字符串的对象。
/ /   唯一字符串由两部分组成：前缀+序列号。
/ /   该对象包含一个设置前缀的方法，一个设置序列号的方法 / /   和一个产生唯一字符串的  gensym  方法。

var   prefix ='';
var   seq =  0;
return {
set _prefix: function(p)  {
prefix  = String( p) ;
} ,
set _seq:	function( s )   {
seq= s ;
} ,
gens ym:function(   )   {
var   result   =   prefix+ seq;
seq  +=   1;
return  resul t ;
}
} ;
} ;
var   seqer =  serial _maker (   ) ;
seqer . set _pref i x( ' Q' ) ;
seqer . set _seq( 1000) ;
var   unique  = seqer.gens ym(   ) ;	/ /   unique   是" Q1000"

seqer包含的方法都没有用到this或that，因此没有办法损害seqer。除 非调用对应的方法，否则没法改变prefix或seq的值。seqer对象是可变 的，所以它的方法可能会被替换掉，但替换后的方法依然不能访问私有 成员。seqer就是一组函数的集合，而且那些函数被授予特权，拥有使用 或修改私有状态的能力。
如果我们把seqer.gensym作为一个值传递给第三方函数，那个函数 能用它产生唯一字符串，但却不能通过它来改变prefix或seq的值。

- 级联 Cascade

1. 有一些方法没有返回值。例如，一些设置或修改对象的某个状态却 不返回任何值的方法就是典型的例子。如果我们让这些方法返回this而 不是undefined，就可以启用级联。在一个级联中，我们可以在单独一条 语句中依次调用同一个对象的很多方法。一个启用级联的Ajax类库可能 允许我们以这样的形式去编码：
getElement ('myBoxDiv')
.move(350,150)
. widt h(100)
. height ( 100)
. color ( ' red' )
. border ( ' 10px   outset ' )
. padding( ' 4px' )
. appendText ( " Pleaestand by" )
. on(' mousedown' ,	function( m)   {
this .s t ar t Dr ag( m,this. getNinth( m) ) ;
} )
. on( ' mous emove' ,	' drag' )
. on( ' mous eup' ,	' stopDrag' )
. later ( 2000,function(   ){
this
.
在这个例子中，getElement函数产生一个对应于id="myBoxDiv"的 DOM元素且给其注入了其他功能的对象。该方法允许我们移动元素， 修改它的尺寸和样式，并添加行为。这些方法每一个都返回该对象，所 以每次调用返回的结果可以被一次调用所用。
级联技术可以产生出极富表现力的接口。它也能给那波构造“全 能”接口的热潮降降温，一个接口没必要一次做太多事情。

- 柯里化(6) Curry


1. 函数也是值，从而我们可以用有趣的方式去操作函数值。柯里化允 许我们把函数与传递给它的参数相结合，产生出一个新的函数。
2. curry方法通过创建一个保存着原始函数和要被套用的参数的闭包来 工作。它返回另一个函数，该函数被调用时，会返回调用原始函数的结 果，并传递调用curry时的参数加上当前调用的参数。它使用Array的 concat方法连接两个参数数组。
糟糕的是，就像我们先前看到的那样，arguments数组并非一个真正 的数组，所以它并没有concat方法。要避开这个问题，我们必须在两个 arguments数组上都应用数组的slice方法。这样产生出拥有concat方法的 常规数组

- 记忆
1. 函数可以将先前操作的结果记录在某个对象里，从而避免无谓的重 复运算。这种优化被称为记忆(7)（memoization）。JavaScript的对象和数 组要实现这种优化是非常方便的。
比如说，我们想要一个递归函数来计算Fibonacci数列(8)。一个 Fibonacci数字是之前两个Fibonacci数字之和。最前面的两个数字是0和 1。
var   fibonacci	= function ( n)   {
return n < 2 ? n :fibonacci ( n-1)   +   fibonacci( n- 2) ;
} ;
for   ( var  i= 0;i<= 10;	i +=  1)  {
document . writeln( '/ /'	+  i+ ':'+   fibonacci ( i ) ) ;
}
/ /   0:	0
/ /   1:	1
/ /   2:	1
/ /   3:	2
/ /   4:	3
/ /   5:	5
/ /   6:	8
/ /   7:	13
/ /   8:	21
/ /   9:	34
/ /   10:	55
这样是可以工作的，但它做了很多无谓的工作。fibonacci函数被调 用了453次。我们调用了11次，而它自身调用了442次去计算可能已被刚 计算过的值。如果我们让该函数具备记忆功能，就可以显著地减少运算 量。
我们在一个名为memo的数组里保存我们的存储结果，存储结果可 以隐藏在闭包中。当函数被调用时，这个函数首先检查结果是否已存 在，如果已经存在，就立即返回这个结果。
var   fibonacci	= function(   ){
var   memo =  [0,1] ;
var   fib =  function( n){
var   result = memo[ n] ;
if (typOf result ! == 'number '){
result = fib( n-1) + fib( n - 2) ;
memo[n] = result;
}
return  result;
} ;
return  fib;
} (   ) ;

**总结**
————————————————————
(1)     JavaScript创建一个函数对象时，会给该对象设置一个“调用”属性。当JavaScript调用一 个函数时，可理解为调用此函数的“调用”属性。详细的描述请参阅ECMAScript规范的“13.2 Creating Function Objects”。

(2)  原文中使用了“trivial  solution”，该词组为数学中的术语，可翻译为寻常解或明显解。作 者用在此处意在说明递归用一般的方式去解决每个子问题。具体可参 考http://zh.wikipedia.org/wiki/格林函数。
(3)          汉诺塔是印度一个古老传说，也是程序设计中的经典递归问题。详细的说明请参见 http://baike.baidu.com/view/191666.htm。

(4)  尾递归（tail  recursion或tail-end  recursion）是一种在函数的最后执行递归调用语句的特 殊形式的递归。参见http://en.wikipedia.org/wiki/Tail_recursion。
(5) 模块模式通常结合单例模式（Singleton Pattern）使用。JavaScript的单例就是用对象字面 量表示法创建的对象，对象的属性值可以是数值或函数，并且属性值在该对象的生命周期中不 会发生变化。它通常作为工具为程序其他部分提供功能支持。单例模式的更多内容请参见 http://zh.wikipedia.org/wiki/单例模式。

(6)  柯里化，也常译为“局部套用”，是把多参数函数转换为一系列单参数函数并进行调用的 技术。这项技术以数学家Haskell	Curry（Haskell编程语言也是以该数学家命名）的名字命名。 更多内容请参考http://zh.wikipedia.org/wiki/柯里化。本书的上一版中译为“套用”，再版采用开发 人员更为认可的“柯里化”的翻译。
(7)     在计算机领域，记忆（memoization）是主要用于加速程序计算的一种优化技术，它使 得函数避免重复演算之前已被处理的输入，而返回已缓存的结果——摘自 http://en.wikipedia.org/wiki/Memoization。

(8)  Fibonacci数列，中文名为斐波那契数列。它的特点是，前面相邻两项之和等于后一项的 值。更多请参考http://zh.wikipedia.org/wiki/斐波那契数列。







