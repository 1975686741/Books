# 继承

1. 在那些基于类的语言（比如Java）中，继承（inheritance或 extends）提供了两个有用的服务。首先，它是代码重用的一种形式。如 果一个新的类与一个已存在的类大部分相似，那么你只需具体说明其不 同点即可。代码重用的模式极为重要，因为它们可以显著地减少软件开 发的成本。类继承的另一个好处是引入了一套类型系统的规范。由于程 序员无需编写显式类型转换的代码，他们的工作量将大大减轻，这是一 件很好的事情，因为类型转换会丧失类型系统在安全上的优势。
2. JavaScript是一门弱类型语言，从不需要类型转换。对象继承关系变 得无关紧要。对于一个对象来说重要的是它能做什么，而不是它从哪里来。
在基于类的语言中，对象是类的实例，并且类可以从另一个类继承。JavaScript是一门基于原型的语言，这意味着对象直接从其他对象继承.

- 伪类
   1. JavaScript的原型存在着诸多的矛盾。某些复杂的语法看起来就像那些基于类的语言，这些语法问题掩盖了它的原型机制。它不直接让对线从其他对象继承，反而插入了一个多余的间接层：通过构造器函数产生对象。
   2. 使用构造器函数存在一个严重的危害。如果在调用构造器函数时忘记了前面加上new前缀，那么this、将不会被绑定到一个新对象上，这样的话，不但没有扩充新对象，反而破坏了全局变量环境。 发生那样的情况时，即没有编译时警告，也没有运行时警告。这是一个严重的语言设计错误。
   3. 为了降低这个问题带来的风险， 所有的构造器函数都约定 命名成首字母大写的形式，并且不以首字母大写的形式拼写任何其他的东西。这样我们至少可以通过目视检查去发现是否缺少了new前缀。 一个更好的备选方案是根本不使用new。
   4. “伪类”形式可以给不熟悉javascript的程序员提供便利，但它也隐藏了该语言的真实的本质。
   5. 借鉴类的表示法可能误导程序员去编写过于深入该复杂的层次结构。许多复杂的层次结构产生的原因就是静态类型检查的约束，而javascript完全摆脱了那些约束。在基于类的语言中，类继承是代码重用的唯一方式，而javascript有着更多且更好的选择。

- 对象说明符
   1. 编写构造器的时候让它接受一个简单的对象说明符  那个对象包含了将要构建的对象规格说明
         var myObject = maker({
            first: f,
            middle: m,      // var myObject = maker({f,,m,l,s,c)};
            last: l,
            state: s,
            city: c
         });   
   2. 当与JSON一起工作时，这是形式有一个好处是： JSON文本只能描述数据，但有时数据表示的是一个对象，把该数据与它的方法关联起来是有用的。如果构造器取得一个对象说明符，就能让它轻松实现，因为我们可以简单地把JSON对象传递给构造器，而它将返回一个构造完全的对象。

- 原型 Prototypal
   1. 基于原型的继承相对于基于类的继承在概念上更为简单：一个新对象可以继承一个旧对象的属性。
   2. 通过构造一个有用的对象，接着可以构造更多和那个对象类似的对象。这就可以完全避免把一个应用拆解成一系列嵌套抽象类的分类过程
   3.  用对象字面量去构造一个有用的对象：
      var myMammal = {
         name : 'Herb the Mammal',
         get_name : function () {
            return this.name;
         },
         says : function () {
            return this.saying || '' ;
         }
      };
      一旦有了一个想要的对象，就可以用Object.create方法构造出更多的实例来。 接下来可以定制新的实例：
      var myCat = Object.create(myMammal);
      myCat.name = 'Henrietta';
      myCat.saying = 'meow';
      myCat.purr = function (n) {
         var i,s = '';
         for(i = 0; i < n; i +=1){
            if(s){
               s += '-';
            }
            s += 'r';
         }
         return s;
      };
      myCat.get_name = function () {
         return this.says + '' + this.name + '' + this.says;
      };
      这是一种“差异化继承”。通过定制一个新的对象，我们指明它与所基于对象的区别。
   4. 定义在一个作用域中的条目在该作用域之外是不可见的。 一个内部作用域会继承它的外部作用域。
   5. 当遇到一个左花括号时 block函数被调用。 parse函数将从scope中寻找符号，并且当它定义了新的符号时扩充scope:
      var block = function () {
         // 记住当前作用域。构造了一个包含当前作用域中所有对象的新作用域
         var oldScope = scope;
         scope = Object.begey(scope);
         //传递左花括号作为参数调用 advance
         advance('{');
         //使用新的作用域进行解析
         parse(scope);
         //传递右花括号作为参数调用advance并抛弃新作用域，恢复原来老的作用域
         advance('}');
         scope = oldScope;
      };

- 函数化
      函数构造器的伪代码模板：
      var constructor = function (spec, my){
         var that,其他的私有实例变量;
         my = my || {};

         把共享的变量和函数添加到my中

         that = 一个新对象

         添加给that的特权方法

         return thar;
      };

      接下来声明该对象私有的实例变量和方法。构造器的变量和内部函数变成了该实例的私有成员。内部函数可以访问spec、my、that以及其他私有变量
      接下里，给my对象添加共享的秘密成员。这是通过赋值语句来实现的：
      my.member = value;
      接下来，我们扩充that，加入该对象接口的特权方法。分配一个新函数成为that的成员方法。或者更安全地，先把函数定义为私有方法，然后再把它们分配给that：
      var methodical = function () {
         ...
      };
      that.methodical = methodical;
      分两步去定义methodical，可以保护私有的methodical不受该实例被修改的影响
      name和saying属性现在是完全私有的。只有通过get_name和says两个特权方法才可以访问它们
      var mammal = function (spec) {
         var that = {}；

         that.get_name = function () {
            return spec.name;
         };
         that.says = function () {
            return spec.saying || '',
         };

         return that;
      };
      var myMammal = mammal({name: 'Herb'});
      在伪类模式里，构造器Cat不得不重复构造器Mammal以及完成的工作。
      在函数化模式里不再需要了，因为构造器Cat将会调用构造器Mammal，让它去做对象创建中的大部分工作，所以Cat只需关注自身的差异就可以了。
      var cat = function (spec) {
         spec.saying = spec.saying || 'meow';
         var that = mammal(spec);
         that.purr = function (n) {
            var i, s = '';
            for(i = 0; i < n; i += 1){
               if (s) {
                  s += '-';
               }
               s += 'r';
            }
            return s;
         };
         that.get_name = function () {
            return that.says() + '' + spec.name + '' + that.says
         };
         return that;
      };
      var myCat = cat({name: 'Henrietta'});
      构造一个superior方法，它取得一个方法名并返回调用那个方法的函数。该函数会调用原来的方法，尽管属性以及变化了。
      Object.method('superior', function (name){
         var that = this,
         method = that[name];
         return function () {
            return method.apply(that, arguments);
         };
      });
      在coolcat上试验一下
      var coolcat = function (spec) {
         var that = cat(spec),
         super_get_name = that.superior('get_namne');
         that.get_name = function (n) {
            return 'like' + super_get_name() + 'baby';
         };
         return that;
      };
      var myCoolCat = coolcat({name: 'Bix'});
      var name = myCoolCat.get_name();
      //'like meow Bix meow baby'
      函数化模式有很大的灵活性。它相比伪类模式不仅带来的工作更少，还让我们得到更好的封装和信息隐藏，以及访问父类的能力

- 部件 Parts'
      // 构造一个给任何对象添加简单事件处理特性的函数。 给对象添加一个on方法、fire方法和一个私有的事件注册表对象：
         var eventuality = function (that) {
            var registry = {};
            that.fire = function (event) {
               //在一个对象上触发一个事件。该事件可以是一个包含事件名称的字符串
               //或者是一个拥有包含事件名称的type属性的对象
               //通过'on'方法注册的事件处理程序中匹配事件名称的函数将被调用
            var array,
                 func, 
                 handler, 
                 i,
                 type = typeof event === 'string' ? event : event.type;
                //如果这个事件存在一组事件处理程序，那么就遍历它们并按顺序依次执行。
            if (registry.hasOwnProperty(type)) {
                array = registry[type];
                for (i = 0; i < array.length; i += 1){
                    handler = array[i];
                //每个处理程序包含一个方法和一组可选的参数
                //如果该方法是一个字符串形式的名字，那么寻找到该函数
                func = handler.method;
                if (typeof func === 'string'){
                    func = this[func];
                }
                //调用一个处理程序。 如果该条目包含参数，那么传递它们过去。否则，传递该事件对象
                func.apply(this, handler.parameters || [event]);                  
                  }
                }
                return this;
                };
                that.on = function (type, method, parameters) {
                    //注册一个事件。构造一条处理程序条目。将它插入到处理程序数组中
                    //如果这种类型的事件还不存在，就构造一个
                var handler = {
                    method: method,
                    parameters: parameters
                };
                if (registry.hasOwnProperty(type)) {
                    registry[type].push(handler);
                } else{
                    registry[type] = [handler];
                };
                return that;
                };
                eventuality(that);
            }
    我们可以在任何单独的对象上调用eventuality,授予它事件处理方法
    也可以赶在that被返回前在一个构造器函数中调用它。
    用这种方式，一个构造器函数可以从一套部件中组装出对象来。
    JavaScript的弱类型在此处是一个巨大的优势，因为我们无须花费精力去关注一个类型系统中系谱类。
    相反，我们可以关注它们的个性化内容
    如果我们需要eventuality去访问该对象的私有状态，则可以把私有成员集my传递给它     