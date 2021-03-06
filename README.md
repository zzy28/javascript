# javascript the good parts
第一章 精华


分析JavaScript
JavaScript建立在一些非常优秀的想法和少数非常糟糕的想法之上。
那些优秀的想法包括函数，弱类型，动态对象和富有表现力的对象字面量表示法。那些糟糕的想法包括基于全局变量的编程模型。
JavaScript的函数是（主要）基于词法作用域(lexical scoping)的顶级对象。JavaScript是第一个成为主流的lambda语言。实际上，相对于Java而言，JavaScript与lisp和scheme有更多的共同点。他是披着c外衣的lisp。这使得JavaScript成为一个非常强大的语言。
现今大部分编程语言中都流行要求强类型。其原理在于强类型允许编译器在编译时检测错误。我们能越早检测和修复错误，付出的代价就越小。JavaScript是一门弱类型的语言，所以JavaScript编译器不能检测出类型错误。这可能让强类型语言转向JavaScript的开发人员感到恐慌。但事实证明，强类型并不会让你的测试工作变得轻松。而且我在工作中发现，强类型检查到的错误并不是令我头痛的错误。另一方面，我发现弱类型是自由的。我无需建立复杂的类层次，我永远不用做强制造型，也不用疲于应付系统以得到想要的行为。
JavaScript有非常强大的对象字面量表示法。通过列出对象的组成部分，他们就能简单地被创建出来。这种表示法是json的灵感来源，他现在已经成为流行的数据交换格式。
原型继承是JavaScript中一个有争议的特性。JavaScript有一个无类型的对象系统，在这个系统中，对象直接从其他对象继承属性。这真的很强大，但是对那些被训练使用类去创建对象的程序员们来说，原型继承是一个陌生的概念。如果你尝试对JavaScript直接应用基于类的设计模式，你将会遭受挫折。但是，如果你学会了自如的使用JavaScript原型，你的努力将会有回报。
JavaScript在关键思想的选择上饱受争议。虽然在大多数情况下，这些选择是合适的。但是有一个选择相当糟糕：JavaScript依赖于全局变量来进行连接。所有编译单元的所有顶级变量被撮合到一个被称为全局对象的公共命名空间中。这是一件糟糕的事情，因为全局变量是魔鬼，但他们在JavaScript却是基础。幸好，我们接下来会看到，JavaScript也给我们提供了缓解这个问题的处理方法。
在某些情况下，我们可能无法忽略糟粕，还有一些毒瘤难以避免，当涉及这些部分时，我会将他们指出来。它们也被总结在附录a中。但是我们将成功地避免本书中提到的大多数糟粕，它们中的大部分被总结在附录b中。如果你想学习那些糟粕，以及如何拙劣的使用。。。

第二章 语法
空白
空白可能表现为被格式化的字符或注释的形式。空白通常没有意义，但是有时候必须要用它来分隔字符序列，否则他们就会被合并成一个符号。例如，对如下代码来说：
var that  = this;
var和that之间的空格是不能移除的，但是其他空格都可以移除。
建议避免使用/* */注释，而用//注释代替他。
标识符
标识符由一个字母开头，其后可选择性地加上一个或多个字母，数字或下划线。标识符不能使用下面这些保留字：
abstract
boolean break byte
case catch char class const continue
debugger default delete do double
else enum export extends
false final finally float for function
goto
if implements import in instanceof int interface
long
native new null
package private protected public
return 
short static super switch synchronized
this throw throws transient true try typeof
var volatile void
while with
在这个列表中的大部分保留字尚未用在这门语言中。这个列表不包括一些本应被保留而没有保留的字，诸如undefined,NaN,Infinity。JavaScript不允许使用保留字来命名变量或参数。更糟糕的事，JavaScript不允许在对象字面量中，或者用点运算符提取对象属性时，使用保留字作为对象的属性名。
标识符被用于语句，变量，参数，属性名，运算符和标记。
数字
JavaScript只有一个数字类型。他在内部被表示为64位的浮点数，和java的double数字类型一样。与其他大多数编程语言不同的是，他没有分离出整数类型，所以1和1.0的值相同。这提供了很大的方便，因为他完全避免了短整型的溢出问题，你只需要知道他是一种数字。这避免了一大堆因数字类型导致的错误。
如果一个数字字面量有指数部分，那么这个字面量的值等于e之前的数字与10的e之后数字的次方相乘。所以100和1e2是相同的数字。
负数可以用前置运算符－加数字构成。
NaN是一个数值他表示一个不能产生结果的运算结果。NaN不等于任何值，包括他自己。你可以用函数isNaN检测NaN.
Infinity表示所有大于1.79769313486231570e+308的值。
数字拥有方法。JavaScript有一个对象Match，它包含一套作用于数字的方法。例如，可以用Match.floor方法把一个数字转换成一个整数。
字符串
字符串字面量可以被包在一堆单引号或双引号中，他可能包含0个或多个字符。\反斜线符号是转义字符。JavaScript在被创建的时候，Unicode是一个16位的字符集，所以JavaScript中的所有字符都是16位的。
JavaScript没有字符类型。要表示一个字符，只需创建仅包含一个字符的字符串即可。
转义字符用来把那些正常情况下不被允许的字符插入到字符串中，比如反斜线，引号和控制字符。\u约定用来指定数字字符编码。
“A” === “\u0041”
字符串中有一个length属性。例如，”seven”.length是5.
字符串是不可变的。一旦字符串被创建，就永远无法改变它。但你可以很容易地通过＋运算符链接其他字符串来创建一个新字符串。两个包含着完全相同的字符且字符顺序也相同的字符串被认为是相同的字符串。所以’c’+’a’+’t’ === ‘cat’ 是true。
字符串有一些方法’cat’.toUpperCase ( ) ===‘CAT'
语句
一个编译单元包含一组可执行的语句。在web浏览器中，每个<script>标签提供一个被编译且立即执行的编译单元。因为缺少连接器，JavaScript把她们一起抛到一个公共的全局名字空间中。
当var语句被用在函数内部时，它定义的是这个函数的私有变量。
switch,while,for,do语句允许有一个可选的前置标签，他配合break语句来使用。
语句通常按照从上到下的顺序被执行。JavaScript可以通过条件语句，循环语句，强制跳转语句和函数调用来改变执行序列。
代码块是包在一对花括号中的一组语句。不像其他语言，JavaScript中的代码块不会创建新的作用域，因此变量应该被定义在函数的头部，而不是在代码块中。
if语句根据表达式的值改变程序流程。表达式的值为真时执行跟在其后的代码块，否则执行可选的else分支。
下面列出的值被当作假：
false
null
undefined
空字符串’ ‘
数字0
数字NaN
其他所有的值都被当作真，包括true,字符串’false’，以及所有的对象。
switch
case break;
while
for
for in
do 
try catch
throw
return 没有指定返回表达式，那么返回值是undefined
JavaScript不允许在return 或break关键字和表达式之间换行。

表达式
最简单的表达式是字面量值（比如字符串或数字），变量，内置的值，以new开头的调用表达式，以delete开头的属性提取表达式，包在圆括号中的表达式，以一个前置运算符作为前导的表达式，或者表达式后面跟着：
一个中置运算符与另一个表达式；三元运算符？后面跟着另一个表达式，然后接一个：，然后接第三个表达式；
一个函数调用；一个属性提取表达式。
三元运算符？有三个运算数，如果第一个运算数值为真，产生第二个运算数的值，但如果第一个运算数值为假，则产生第三个运算数的值。
运算符优先级
typeof运算符产生的值有’number’,’string’,’boolean’,’undefined’,’function’,’object’，如果运算数是一个数组或null，那么结果是’object’，这其实是不对的。
！
＋
／运算符可能会产生一个非整数结果，即使两个运算数都是整数。
如果第一个运算数的值为假，那么运算符&&产生他第一个运算数的值，否则产生第二个运算数的值。
如果第一个运算数的值为真，那么运算符｜｜产生第一个运算数的值，否则产生第二个运算数的值。
字面量
对象字面量是一种可以方便地按照指定规格创建新对象的表示法。属性名可以是标识符或字符串。这些名字被当作字面量名而不是变量名来对待，所以对象的属性名在编译时才能知道。属性的值就是表达式。
函数
函数字面量定义了函数值。它可以有一个可选的名字，用于递归的调用自己。它可以制定一个参数列表，这些参数就像变量一样，在调用时有传递的实际参数初始化。函数的主体包括变量定义和语句。

第三章 对象
JavaScript的简单数据类型包括数字，字符串，布尔值，null值和undefined值。其他所有的值都是对象。数字，字符串和布尔值貌似对象，因为他们拥有方法，但他们是不可变的。JavaScript中的对象是可变的键控集合。在JavaScript中，数组是对象，函数是对象，正则表达式是对象。
对象是属性的容器，其中每个属性都拥有名字和值。属性的名字可以是包括空字符串在内的任意字符串。属性值可以是除undefined值之外的任何值。
JavaScript里的对象是无类型的。它对新属性的名字和属性的值没有限制。对象适合用于汇集和管理数据。对象可以包含其他对象，所以他们可以容易地表示成树状或图形结构。
JavaScript包含一种原型链的特性，允许对象继承另一个对象的属性。正确的使用它能减少对象初始化时消耗的时间和内存。
对象字面量
对象字面量提供了一种非常方便地创建新对象值的表示法。一个对象字面量就是包围在一对花括号中的零或多个“名／值”对。对象字面量可以出现在任何允许表达式出现的地方。
var empty_object = { };

var stooge = {
“first-name”:”Jerome”,
“last-name”:”Howard”
};
属性名可以是包括空字符串在内的任何字符串。在对象字面量中，如果属性名是一个合法的JavaScript标识符且不是保留字，则并不强制要求用引号括住属性名。所以用引号括住“first-name”是必须的，但是否括住first_name则是可选的。逗号用来分隔多个“名／值”对。
属性的值可以从包括另一个对象字面量在内的任意表达式中获得。对象是可嵌套的：
var flight = {
airline:”Oceanic”,
number:815,
departure:{
IATA:”SYD”,
time:”2004-09-22 14:55”,
city:”Sydney”
},
arrival:{
IATA:”LAX”,
time:”2004-09-23 10:42”,
city:”Los Angeles”
}
};
检索
要检索对象里包含的值，可以采用在［］后缀中括住一个字符串表达式的方式。如果字符串表达式是一个字符串字面量，而且它是一个合法的JavaScript标识符且不是保留字，那么也可以用 . 表示法代替。优先考虑使用 . 表示法，因为它更紧凑且可读性更好。
stooge[“first-name”]   //“Jerome”
flight.departure.IATA   //“SYD”
如果你尝试检索一个并不存在的成员属性的值，将返回undefined
stooge[“middle-name”]   //undefined
||运算符可以用来填充默认值：
var middle = stooge[“middle-name”] || “(none)”;
var status = flight.status || “unknown”;
尝试从undefined的成员属性中取值将会导致typeerror异常。这时可以通过&&运算符在避免错误。
flight.equipment //undefined
flight.equipment.model //throw”TypeError”
flight.equipment && flight.equipment.model //undefined
更新
对象里的值可以通过赋值语句来更新。如果属性名已经存在于对象里，那么这个属性的值就会被替换。
stooge[‘first-name’] = ‘Jerome’;
如果对象之前没有拥有这个属性名，那么该属性就被扩充到对象中。
stooge[‘middle-name’] = ‘Lester’;
stooge.nickname = ‘Curly’;
flight.equipment = {
model:’Boeing 777’
};
flight.status = ‘overdue’;
引用
对象通过引用来传递。它们永远不会被复制：
var x = stooge;
x.nickname = ‘Curly’;
var nick = stooge.nickname;
//因为x和stooge是指向同一个对象的引用，所以nick为curly。
var a = { }, b = { }, c = { };
//abc每个都引用一个不同的空对象。
a = b = c = { };
//abc都引用同一个空对象。
原型
每个对象都连接到一个原型对象，并且它可以从中继承属性。所有通过对象字面量创建的对象都连接到Object.prototype,它是JavaScript中的标配对象。
当你创建一个新对象时，你可以选择某个对象作为他的原型。JavaScript提供的实现机制杂乱而复杂，但其实可以被明显的简化。我们将给object增加一个create方法。这个方法创建一个使用原对象作为其原型的新对象。
if (typeof Object.beget !== ‘function’){
Object.create = function (o){
var F = function (){};
F.prototype = o;
return new F();
};
}
var another_stooge = Object.create(stooge);
原型连接在更新时是不起作用的。我们对某个对象做出改变时，不会触及该对象的原型：
another_stooge[‘first-name’] = ‘Harry’;
another_stooge[‘middle-name’] = ‘Moses’;
another_stooge.nickname = ‘Moe’;
原型连接只有在检索值的时候才被用到。如果我们尝试去获取对象的某个属性值，但该对象没有此属性名，那么JavaScript会试着从原型对象中获取属性值。如果那个原型对象也没有该属性，那么再从它的原型中寻找，以此类推，知道该过程最后到达终点object.prototype。如果想要的属性完全不存在于原型链中，那么结果就是undefined值。这个过程称为委托。
原型关系是一种动态的关系。如果我们添加一个新的属性到原型中，该属性会立即对所有基于该原型创建的对象可见。
stooge.profession = ‘actor’;
another_stooge.profession  // ‘actor’
反射
检查对象并确定对象有什么属性是很容易的事情，只要去检索该属性并验证取得的值。
typeof操作符对确定属性的类型很有帮助：
typeof flight.number //‘number’
typeof flight.status //‘string’
typeof flight.arrival //‘object’
typeof flight,manifest // ‘undefined’
请注意原型链中的任何属性都会产生值：
typeof flight.toString //‘function’
typeof flight.constructor //‘function’
有两种方法去处理掉这些不需要的属性。第一个是让你的程序做检查并丢弃值为函数的属性。一般来说，当你想让对象在运行时动态获取自身信息时，你关注更多的是数据，而你应该意识到一些值可能会是函数。
另一个方法是使用hasOwnProperty方法，如果对象拥有独有的属性，它将返回true。该方法不会检查原型链。
flight.hasOwnProperty(‘number’) //true
flight.hasOwnProperty(‘constructor’) //false
枚举
for in语句可用来遍历一个对象中的所有属性名。该枚举过程将会列出所有的属性－包括函数和你可能不关心的原型中的属性－所以有必要过滤掉那些你不想要的值。最为常用的过滤器是hasOwnProperty方法，以及使用typeof来排除函数：
var name;
for (name in another_stooge){
if (typeof another_stooge[name] !== ‘function’){
document.writeln(name + ‘:’ +another_stooge[name]);
}
}
属性名出现的顺序是不确定的，因此要对任何可能出现的顺序有所准备。如果你想要确保属性以特定的顺序出现，最好的办法就是完全避免使用for in语句，而是创建一个数组，在其中以正确的顺序包含属性名：
var i;
var properties = [
‘first-name’,
‘middle-name’,
‘last-name’,
‘profession’
];
for (i = 0;i < properties.length;i +=1){
document.writeln(properties[i] + ‘:’ + another_stooge[properties[i]);
}
通过使用for而不是for in可以得到我们想要的属性，而不用担心可能发掘出原型链中的属性，并且我们按正确的顺序取得了它们的值。
删除
delete运算符可以用来删除对象的属性。如果对象包含该属性，那么该属性就会被移除。他不会触及原型链中的任何对象。
删除对象的属性可能会让来自原型链中的属性透现出来。
another_stooge.nickname  //‘Moe’
//删除another_stooge的nickname属性，从而暴露出原型的nickname属性。
delete another_stooge.nickname;
another_stooge.nickname  //‘Curly’
减少全局变量污染
JavaScript可以很随意地定义全局变量来容纳你的应用的所有资源。遗憾的是，全局变量削弱了程序的灵活性，应该避免使用。
最小化使用全局变量的方法之一是为你的应用只创建一个唯一的全局变量：
var MYAPP ={ };
该变量此时变成了你的应用的容器：
MYAPP = stooge = {
‘first-name’:’Joe’,
‘last-name’:’Howard’
};
MYAPP.flight = {
airline:”Oceanic”,
number:815,
departure:{
IATA:”SYD”,
time:”2004-09-22 14:55”,
city:”Sydney”
},
arrival:{
IATA:”LAX”,
time:”2004-09-23 10:42”,
city:”Los Angeles”
}
};
只要把全局性的资源都纳入一个名称空间之下，你的程序与其他应用程序，组件或类库之间发生冲突的可能性就会显著降低。你的程序也会变得更容易阅读，因为很明显，MYAPP.stooge指向的是顶层结构。

第四章 函数
JavaScript设计得最出色的就是他的函数的实现。他几乎接近于完美。但是，想必你也能预料到，JavaScript的函数也存在瑕疵。
函数包含一组语句，它们是JavaScript的基础模块单元，用于代码复用，信息隐藏和组合调用。函数用于指定对象的行为。一般来说，所谓编程，就是将一组需求分解成一组函数与数据结构的技能。
函数对象
JavaScript中的函数就是对象。对象是’名／值’对的集合并拥有一个连接到原型对象的隐藏连接。对象字面量产生的对象连接到object.prototype。函数对象连接到Function.protptype该原型对象本身连接到Object.prototype。每个函数在创建时会附加两个隐藏属性：函数的上下文和实现函数行为的代码。
每个函数对象在创建时也随配有一个prototype属性。他的值是一个拥有constructor属性且值即为该函数的对象。这和隐藏连接到Function.prototype完全不同。令人费解。
因为函数是对象，所以他们可以像任何其他的值一样被使用。函数可以保存在变量，对象和数组中。函数可以被当作参数传递给其他函数，函数也可以再返回函数。而且，因为函数是对象，所以函数可以拥有方法。
函数的与众不同之处在于他们可以被调用。
函数字面量
函数对象通过函数字面量来创建：
//创建一个名为add的变量，并用来把两个数字相加的函数赋值给他。
var add = function(a,b){
return a + b;
};
函数字面量包括四个部分。第一个部分是保留字function。
第二个部分是函数名，它可以被省略。函数可以用他的名字来递归地调用自己。此名字也能被调试器和开发工具用来识别函数。如果没有给函数命名，比如上面这个例子，它被称为匿名函数。
第三个部分是包围在圆括号中的一组参数。多个参数用逗号分隔。这些参数的名称将被定义为函数中的变量。它们不像普通的变量那样将被初始化为undefined，而是在该函数被调用时初始化为实际提供的参数的值。
第四个部分是包围在花括号中的一组语句。这些语句是函数的主体，它们在函数被调用时执行。
函数字面量可以出现在任何允许表达式出现的地方。函数也可以被定义在其他函数中。一个内部函数除了可以访问自己的参数和变量，同时他也能自由访问把它嵌套在其中的父函数的参数和变量。通过函数字面量创建的函数对象包含一个连到外部上下文的连接。这被称为闭包。它是JavaScript强大表现力的来源。
调用
调用一个函数会暂停当前函数的执行，传递控制权和参数给新函数。除了声明时定义的形式参数，每个函数还接受两个附加的参数：this和arguments。参数this在面向对象编程中非常重要，它的值取决于调用的模式。在JavaScript中一共有四种调用模式：方法调用，函数调用，构造器调用和apply调用模式。这些模式在如何初始化关键参数this上存在差异。
调用运算符是跟在任何产生一个函数值的表达式之后的一对圆括号。圆括号内可包含零个或多个用逗号隔开的表达式。每个表达式产生一个参数值。每个参数值被赋予函数声明时定义的形式参数名。当实际参数的个数与形式参数的个数不匹配时，不会导致运行时错误。如果实际参数值过多了，超出的参数值会被忽略。如果实际参数值过少，缺失的值会被替换为undefined。对参数值不会进行类型检查：任何类型的值都可以被传递给任何参数。
方法调用模式
当一个函数被保存为对象的一个属性时，我们称它为一个方法。当一个方法被调用时，this被绑定到该对象。如果调用表达式包含一个提取属性的动作（即包含一个 . 点表达式或[]下标表达式），那么他就是被当作一个方法来调用。
／／创建myobject对象。他有一个value属性和一个increment方法。
／／increment方法接受一个可选的参数。如果参数不是数字，那么默认使用数字1。
var myObject = {
value: 0,
increment:function (inc) {
this.value +=typeof inc ===‘number’ ? inc : 1;
}
};
myObject.increment( );
document.writeln(myObject.value);  //1 
myObject.increment(2);
document.writeln(myObject.value);  //3
方法可以使用this访问自己所属的对象，所以它能从对象中取值或对对象进行修改。this到对象的绑定发生在调用的时候。这个超级延迟绑定使得函数可以对this高度复用。通过this可取得他们所属对象的上下文的方法称为公共方法。
函数调用模式
当一个函数并非一个对象的属性时，那么它就是被当作一个函数来调用的：
var sum = add(3,4); // sum = 7
以此模式调用函数时，this被绑定到全局对象。这是语言设计上的一个错误。倘若语言设计正确，那么当内部函数被调用时，this应该仍然绑定到外部函数的this变量。这个设计错误的后果就是方法不能利用内部函数来帮助他工作，因为内部函数的this被绑定了错误的值，所以不能共享该方法对对象的访问权。幸运的事，有一个很容易的解决方案：如果该方法定义一个变量并给他赋值为this，那么内部函数就可以通过那个变量访问到this。按照约定：我把那个变量命名为that：
／／给myobject增加一个double方法。
myObject.double = function(){
var that = this; //解决方法
var helper = function(){
that.value = add(that.value,that.value);
};
helper(); //以函数的形式调用helper。
};
／／以方法的形式调用double。
myObject.double ;
document.writeln(myObject.value);  // 6
构造器调用模式
JavaScript是一门基于原型继承的语言。这意味着对象可以直接从其他对象继承属性。该语言是无类型的。
这偏离了当今编程语言的主流风格。当今大多数语言都是基于类的语言。尽管原型继承极富表现力，但他并未被广泛理解。JavaScript本身对它原型的本质也缺乏信心，所以它提供了一套和基于类的语言类似的对象构建语法。有类型化语言编程经验的程序员们很少有愿意接受原型继承的，并且认为借鉴类型化语言的语法模糊了这门语言真实的原型本质。真是两边都不讨好。
如果在一个函数前面带上new来调用，那么背地里将会创建一个连接到该函数的prototype成员的新对象，同时this会被绑定到那个新对象上。
new前缀也会改变return语句的行为。我们将会在后面看到更多的相关内容。
／／创建一个名为Quo的构造器函数。它构造一个带有status属性的对象。
var Quo = function(string){
this.status = string;
};
//给Quo的所有实例提供一个名为get_status的公共方法。
Quo.prototype.get_status = function(){
return this.status;
};
//构造一个Quo实例。
var myQuo = new Quo(“confused”);
document.writeln(myQuo.get_status()); //打印显示”confused”
一个函数，如果创建的目的就是希望结合new前缀来调用，那它就被称为构造器函数。按照约定，它们保存在以大写格式命名的变量里。如果调用构造器函数时没有在前面加上new，可能会发生非常糟糕的事情，既没有编译时警告，也没有运行时警告，所以大写约定非常重要。我不推荐使用这种形式的构造器函数。
Apply调用模式
因为JavaScript是一门函数式的面向对象编程语言，所以函数可以拥有方法。
apply方法让我们构造一个参数数组传递给调用函数。它也允许我们选择this的值。apply方法接收两个参数，第一个是要绑定给this的值，第二个就是一个参数数组。
／／构造一个包含两个数字的数组，并将它们相加。
var array = [3,4];
var sum = add.apply(null,array);  //sum = 7
／／构造一个包含status成员的对象。
var statusObject = {
status: ‘A-OK’
};
／／statusObject并没有继承自Quo.prototype，但我们可以在statusObject上
／／调用get_status方法，尽管statusObject并没有一个名为get_status的方法。
var status = Quo.prototype.get_status.apply(statusObject);
参数
当函数被调用时，会得到一个免费配送的参数，那就是arguments数组。函数可以通过此参数访问所有它被调用时传递给它的参数列表，包括那些没有被分配给函数声明时定义的形式参数的多余参数。这使得编写一个无需指定参数个数的函数成为可能：
／／构造一个大量的值想家的函数。
／／注意该函数内部定义的变量sum不会与函数外部定义的sum产生冲突。
／／该函数只会看到内部的那个变量。
var sum = function(){
var i,sum = 0;
for(i =0;i<arguments.length;i+=1){
sum +=arguments[i];
}
return sum;
};
document.writeln(sum(4,8,15,16,23,42)); // 108
这不是一个特别有用的模式。在第六章中，我们将会看到如何给数组添加一个相似的方法来达到同样的效果。
因为语言的一个设计错误，arguments并不是一个真正的数组。它只是一个类似数组的对象。arguments拥有一个length属性，但他没有任何数组的方法。我们将在本章结尾看到这个设计错误导致的后果。
返回
当一个函数被调用时，它从第一个语句开始执行，并在遇到关闭函数题的｝时结束。然后函数把控制权交还给调用该函数的程序。
return语句可用来使函数提前返回。当return被执行时，函数立即返回而不再执行余下的语句。
一个函数总是会返回一个值。如果没有制定返回值，则返回undefined。
如果函数调用时在前面加上了new前缀，且返回值不是一个对象，则返回this（该新对象）。
异常
JavaScript提供了一套异常处理机制。异常是干扰程序的正常流程的不寻常的事故。当发现这样的事故时，你的程序应该抛出一个异常：
throw语句中断函数的执行。他应该抛出一个exception对象，该对象包含一个用来识别异常类型的name属性和一个描述性的message属性。你也可以添加其他的属性。
该exception对象将被传递到一个try语句的catch从句。
扩充类型的功能
JavaScript允许给语言的基本类型扩充功能。在第三章中，我们已经看到，通过给object.prototype添加方法，可以让该方法对所有对象都可用。这样的方式对函数，数组，字符串，数字，正则表达式和布尔值同样适用。
举例来说，我们可以通过给Function.prototype增加方法来使得该方法对所有函数可用:
Function.prototype.method = function(name,func){
this.prototype[name] = func;
return this;
};
通过给Function.prototype增加一个method方法，我们下次给对象增加方法的时候就不必键入prototype这几个字符，省掉了一点麻烦。
JavaScript没有专门的整数类型，但有时候确实只需要提取数字中的整数部分。JavaScript本身提供的取整方法有些丑陋。我们可以通过给Number.prototype增加一个integer方法来改善它。它会根据数字的政府来判断是使用Math.ceiling还是Math.floor。
Number.method(‘integer’,function(){
return Math[this<0 ? ‘ceil’ : ‘floor’](this);
});
document.writeln((-10/3).integer()); // -3
JavaScript缺少一个移除字符串首尾空白的方法。这个小疏忽很容易弥补：
String.method(‘trim’,function(){
return this.replace(/^\s+|\s+$/g,’ ‘);
});
document.writeln(‘ ‘’ ‘ + ‘’  neat   ‘’.trim() + ‘ ‘’ ‘);
我们的trim方法是用了一个正则表达式。
通过给基本类型增加方法，我们可以极大地提高语言的表现力。因为JavaScript原型继承的动态本质，新的方法立刻被赋予到所有的对象实例上，哪怕对象实例是在方法被增加之前就创建好了。
基本类型的原型是公用结构，所以在类库混用时务必小心。一个保险的做法就是只在确定没有该方法时才添加它。
／／符合条件时才添加方法。
Function.prototype.method = function(name,func){
if (!this.prototype[name]){
this.prototype[name] = func;
}
return this;
};
另一个要注意的就是for in语句在原型上时表现很糟糕。我们在第三章已经看到了几个减轻这个问题的影响的方法：hasOwnProperty.
递归
递归函数就是会直接或间接地调用自身的一种函数。递归是一种强大的编程技术，他把一个问题分解为一组相似的子问题，每一个都用一个寻常解去解决。一般来说，一个递归函数调用自身去解决它的子问题。
汉诺塔是一个著名的益智游戏。塔上有三根柱子和一套直径各不相同的空心圆盘。开始时源柱子上的所有圆盘都按照从小到大的顺序堆叠。目标是通过每次移动一个圆盘道另一根柱子上，最终把一堆圆盘移动到目标柱子上，过程中不允许把较大的圆盘放置在较小的圆盘之上。这个问题有一个寻常解。
var hanoi = function (disc , src , aux , dst){
if ( disc>0){
hanoi (disc - 1, src , dst, aux);
document.writeln(‘Move disc ‘+ disc + ‘ from ‘ +src + ‘ to ‘ +dst);
hanoi (disc -1,aux,src,dst);
}
};
hanoi(3, ‘Src’,’Aux’,’Dst’);
圆盘数量为3时它返回这样的解法：
Move disc 1 from Src to Dst
Move disc 2 from Src to Aux
Move disc 1 from Dst to Aux
Move disc 3 from Src to Dst
Move disc 1 from Aux to Src
Move disc 2 from Aux to Dst
Move disc 1 from Src to Dst
hanoi函数把一堆圆盘从一根柱子移到另一根柱子
，必要时使用辅助的柱子。它把该问题分解成三个子问题。首先，它移动一对圆盘中较小的圆盘移动到辅助柱子上，从而露出下面较大的圆盘，然后移动下面的圆盘到目标柱子上。最后，它将刚才较小的圆盘从辅助柱子上再移动到目标柱子上。通过递归地调用自身去处理一堆圆盘的移动，从而解决那些子问题。
传递给hanoi函数的参数，包括当前移动的圆盘编号和它将要用到的三根柱子。当它调用自身的时候，它去处理当前正在处理的圆盘之上的圆盘。最终，它会以一个不存在的圆盘编号去调用。在这样的情况下，他不执行任何操作。由于该函数对非法值不予理会，我们也就不必担心它会导致死循环。
递归函数可以非常高效地操作树形结构，比如浏览器端的文档对象模型（DOM）。每次递归调用时处理指定的树的一小段。
／／定义walk_the_DOM函数，它从某个指定的节点开始，按html源码中的顺序
／／访问该树的每个节点
／／它会调用一个函数，并依次传递每个节点给它。walk_the_DOM调用自身去处理
／／每一个字节点。
var walk_the_DOM = function walk(node, func){
func(node);
node = node.firstChild;
while(node){
walk(node,func);
node = node.nextSibling;}
};

／／定义getElementByAttribute函数。它以一个属性名称字符串
／／和一个可选的匹配值作为参数。
／／它调用walk_the_DOM，传递一个用来查找节点属性名的函数作为参数。
／／匹配的节点会累加到一个结果数组中。
var getElementByAttribute = function (att,value){
var results = [ ];
walk_the_DOM(document.body,function (node){
var actual = node.nodeType ===1 &&node.getAttribute(att);
if (typeof actual ===‘string’ && (actual ===value || typeof value !== ‘string’)){
results.push(node);
}
});
return results;
};

一些语言提供了尾递归优化。这意味着如果一个函数返回自身递归调用的结果，那么调用的过程会被替换为一个循环，它可以显著提高速度。遗憾的事，JavaScript当前并没有提供尾递归优化。深度递归的函数可能会因为堆栈溢出而运行失败。
／／构建一个带尾递归的函数。因为它会返回自身调用的结果，所以它时尾递归。
／／JavaScript当前没有对这种形式的递归做出优化。
var factorial = function factorial(i,a){
a = a || 1;
if(i<2){
return a;
}
return factorial (i - 1,a * i);
};
document.writeln(factorial(4));  //24

作用域
在编程语言中，作用域控制着变量与参数的可见性及生命周期。对程序员来说是一项重要的服务，因为它减少了名称冲突，并且提供了自动内存管理。
var foo = function ( ){
var a = 3, b = 5;
var bar = function ( ){
var b = 7,c = 11;
／／此时，a为3,b为7，c为11。
a += b + c；
／／此时，a为21，b为7，c为11。
｝；
／／此时a为3，b为5，而c还没有定义。
bar( );
／／此时，a为21，b为5.
};
大多数类c语言语法的语言都拥有块级作用域。在一个代码中（括在一对花括号中的一组语句）定义的所有变量在代码块的外部时不可见的。定义在代码块中的变量在代码块之后结束后会被释放掉。这是件好事。
糟糕的事，尽管JavaScript的代码块语法貌似支持块级作用域，但实际上JavaScript并不支持。这个混淆之处可能成为错误之源。
JavaScript确实有函数作用域。那意味着定义在函数中的参数和变量在函数外部是不可见的，而在一个函数内部任何位置定义的变量，在该函数内部任何地方都可见。
很多现代语言都推荐尽可能延迟声明变量。而用在JavaScript上的话却会成为糟糕的建议，因为它缺少块级作用域。所以，最好的做法是在函数体的顶部声明函数中可能用到的所有变量。

闭包
作用域的好处是内部可以访问定义它们的外部函数的参数和变量（除了this和arguments）。这太美妙了。
我们的getElementByAttribute函数可以工作，是因为它声明了一个results变量，而传递给walk_the_DOM的内部函数也可以访问results变量。
一个更有趣的情形是内部函数拥有比它的外部函数更长的生命周期。
之前，我们构造了一个myObject对象，它拥有一个value属性和一个increment方法。假定我们希望该值不会被非法更改。
和以对象字面量形式去初始化myObject不同，我们通过调用一个函数的形式去初始化myObject，该函数会返回一个对象字面量。函数里定义了一个value变量。该变量对increment和getValue方法总是可用的，但函数的作用域使得它对其他程序来说是不可见的。
var myObject = (function( ){
var value = 0;
return {
increment: function( inc){
value += typeof inc === ‘number’ ? inc : 1;},
getValue: function ( ){
return value ;
}};
} ( ));
我们并没有把一个函数赋值给myObject。我们是把调用该函数后返回的结果赋值给它。注意最后一行的（）。该函数返回一个包含两个方法的对象，并且这些方法继续享有访问value变量的特权。
本章之前的Quo构造器产生了一个带有status属性和get_status方法的对象。但那看起来并不是十分有趣。为什么要用一个getter方法去访问你本可以直接访问到的属性呢？如果status是私有属性，它才是更有意义的。所以，让我们定义另一种形式的quo函数来做此事：
／／创建一个名为quo的构造函数。
／／它构造出带有get_status方法和status私有属性的一个对象。
var quo = function (status){
return {
get_status: function ( ) {
return status;
}}};
／／构造一个quo实例
var myQuo = quo(“amazed”);
document.writeln(myQuo.get_status ( ));
这个quo函数被设计成无须在前面加上new来使用，所以名字也没有首字母大写。当我们调用quo时，它返回包含get_status方法的一个新对象。该对象的一个引用保存在myQuo中。即使quo已经返回了，但get_status方法依然享有访问quo对象的status属性的特权。get_status方法并不是访问该参数的一个副本，它访问的就是该参数本身。这是可能的，因为该函数可以访问它被创建时所处的上下文环境。这被称为闭包。让我们来看一个更有用的例子：
／／定义一个函数，它设置一个DOM节点为黄色，然后把它渐变为白色。
var fade = function (node){
var level = 1;
var step = function ( ){
var hex = level.toString(16);
node.style.backgroundColor = ‘#FFFF’ + hex +hex;
if( level < 15){
level +=1;
setTimeout(step,100);
}
};
setTimeout(step,100);
};
fade(document.body);
我们调用fade，把document.body作为参数传递给它（html的dody标签所创建的节点）。fade函数设置level为1。它定义了一个step函数；接着调用setTimeout，并传递step函数和一个时间（100毫秒）给它。然后它返回，fade函数结束。
在大约十分之一秒后，step函数被调用。它把fade函数的level变量转化为16位字符。接着，它修改fade函数得到的节点的背景颜色。然后查看fade函数的level变量。如果背景色尚未变成白色，那么它增大fade函数的level变量，接着用setTimeout预定让它自己再次运行。
step函数很快再次被调用。但这次，fade函数的level变量值变成2。fade函数在之前已经返回了，但只要fade的内部函数需要，它的变量就会持续保留。
为了避免下面的问题，理解内部函数能访问外部函数的实际变量而无需复制是很重要的。
／／糟糕的例子
／／构造一个函数，用错误的方式给一个数组中的节点设置时间处理程序。
／／当点击一个节点时，按照预期，应该弹出一个对话框显示节点的序号，
／／但它总是会显示节点的数目。
var add_the_handlers = function( nodes ) {
var i;
for (i = 0; i< nodes.length; i+=1){
nodes[ i ].onclick = function (e ) {
alert ( i );
};
}
};
／／结束糟糕的例子。
add_the_handlers函数的本意是想传递给每个时间处理器一个唯一值( i )。但它未能达到目的，因为事件处理器函数绑定了变量 i 本身，而不是函数在构造时的变量 i 的值。
／／改良后的例子
／／构造一个函数，用正确的方式给一个数组中的节点设置时间处理程序。
／／点击一个节点，将会弹出一个对话框显示节点的序号。
var add_the_handlers = function ( nodes ){
var helper = function ( i){
return function (e ){
alert ( i);
};
};
var i ;
for ( i = 0;i< nodes.length;i+=1){
nodes[i].onclick = helper(i);
}
};
避免在循环中创建函数，它可能只会带来无谓的计算，还会引起混淆，正如上面那个糟糕的例子。我们可以先在循环之外创建一个辅助函数，让这个辅助函数再返回一个绑定了当前i值的函数，这样就不会导致混淆了。
回调
函数使得对不连续事件的处理变得更容易。例如，假定有这么一个序列，由用户交互行为触发，向服务器发送请求，最终显示服务器的响应。最自然的写法可能会是这样：
request = prepare_the_request( );
response = send_request_synchronously(request);
display(response);
这种方式的问题在于，网络上的同步请求会导致客户端进入假死状态。如果网络传输或服务器很慢，响应会慢到让人不可接受。
更好的方式是发起异步请求，提供一个当服务器的响应到达时随即触发的回调函数。异步函数立即返回，这样客户端就不会被阻塞。
request = prepare_the_request( );
send_request_asynchronously(request,function (response) {
display(response);
});
我们传递一个函数作为参数给sen_request_asynchronously函数，一旦接收到响应，它就会被调用。
模块
我们可以使用函数和闭包来构造模块。模块是一个提供接口却隐藏状态与实现的函数或对象。通过使用函数产生模块，我们几乎可以完全摒弃全局变量的使用，从而缓解这个JavaScript的最为糟糕的特性之一所带来的影响。
举例来说，假定我们想要给String增加一个deentityify方法。它的任务是寻找字符串中的html字符实体并把它们替换为对应的字符。这就需要在一个对象中保存字符实体的名字和它们对应的字符。但我们该在哪里保存这个对象呢？我们可以把它放到一个全局变量中，但全局变量是魔鬼。我们可以把它定义在该函数的内部，但是那会带来运行时的损耗，因为每次执行该函数的时候该字面量都会被求值一次。理想的方式是把它放入一个闭包，而且也许还能提供一个增加更多字符实体的扩展方法：
String.method(‘deentityify’, function ( ){
／／字符实体表。它映射字符实体的名字到对应的字符。
var entity = {
quot:’ ‘’ ‘,
lt: ‘<‘,
gt: ‘>’
};
返回deentityify方法。
return function( ){
／／这才是deentityify方法。它调用字符串的replace方法，
／／查找’&’开头和’;’结束的子字符串。如果这些字符可以在字符实体表中找到，
／／那么就将该字符实体替换为映射表中的值。它用到了一个正则表达式。
return this.replace(/&([^&;]+);/g,
function (a,b){
var r = entity[b];
return typeof r === ‘string’ ? r : a;
}
);
}; }( ));
请注意最后一行。我们用( )运算法立即调用我们刚刚构造出来的函数。这个调用所创建并返回的函数才是deentityify方法。
document.writeln(
‘&lt;quot;&gt;’.deentityify(   ));   // <“>
模块模式利用了函数作用域和闭包来创建被绑定对象与私有对象的关联，在这个例子中，只有deentityify方法有权访问字符实体表这个数据对象。
模块模式的一般形式是：一个定义了私有变量和函数的函数；利用闭包创建可以访问私有变量和函数的特权函数；最后返回这个特权函数，或者把它们保存到一个可访问到的地方。
使用模块模式就可以摒弃全局变量的使用。它促进了信息隐藏和其他优秀的设计实践。对于应用程序的封装，或者构造其他单例对象，模块模式非常有效。
模块模式也可以用来产生安全的对象。假定我们想要构造一个用来产生序列号的对象：
var serial_maker = function ( ) {
 ／／返回一个用来产生唯一字符串的对象。
／／唯一字符串由两部分组成：前缀＋序列号。
／／该对象包含一个设置前缀的方法，一个设置序列号的方法
／／和一个产生唯一字符串的gensym方法。
var prefix = ‘ ‘;
var seq = 0;
return {
set_prefix: function(p){
prefix = String(p);
},
set_seq:function(s){
seq = s;
},
gensym:function ( ){
var result = prefix +seq;
seq += 1;
return result;
}
};
};
var seqer = serial_maker( );
seqer.set_prefix(‘Q’);
seqer.set_seq(1000);
var unique = seqer.gensym( );   ／／unique是’Q1000’
seqer包含的方法都没有用到this或that，因此没有办法损害seqer。除非调用对应的方法，否则没法改变prefix或seq的值。seqer对象是可变的，所以它的方法可能会被替换掉，但替换后的方法依然不能访问私有成员。seqer就是一组函数的集合，而且那些函数被授予特权，拥有使用或修改私有状态的能力。
如果我们把seqer.gensym作为一个值传递给第三方函数，那个函数能用它产生唯一字符串，但却不能通过它来改变prefix或seq的值。
级联
有一些方法没有返回值。例如，一些设置或修改对象的某个状态却不返回任何值的方法就是典型的例子。如果我们让这些方法返回this而不是undefined，就可以启用级联。在一个级联中，我们可以在单独一条语句中依次调用同一个对象的很多方法。一个启用级联的Ajax类库可能允许我们以这样的形式去编码：
getElement(‘myBoxDiv’)
.move(350,150)
.width(100)
.height(100)
.color(‘red’)
.border(‘10px outset’)
.padding(‘4px’)
.appendText(‘Please stand by’)
.on(‘mousedown’,function(m){
this.startDrag(m,this.getNinth(m));
})
.on(‘mousemove’,’drag’)
.on(‘mouseup’,’stopDrag’)
.later(2000,function( ){
this
.color(‘yellow’)
.setHTML(‘What hath God wraught?’)
.slide(400,40,200,200);
})
.tip(‘This box is resizeable’);
在这个例子中，getElement函数产生一个对应于id=‘myBoxDiv’的DOM元素且给其注入了其他功能的对象。该方法允许我们移动元素，修改它的尺寸和样式，并添加行为。这些方法每一个都返回该对象，所以每次调用返回的结果可以被下一次调用所用。
级联技术可以产生出极富表现力的接口。它也能给那波构造“全能”借口的热潮降降温，一个接口没必要一次做太多事情。
柯里化
函数也是值，从而我们可以用有趣的方式去操作函数值。柯里化允许我们吧函数与传递给它的参数相结合，产生出一个新的函数。
var add1 = add.curry(1);
document.writeln(add1(6));   //7
add1是把1传递给add函数的curry方法后创建的一个函数。add1函数把传递给它的参数值加1。并没有curry方法，但我们可以给Function.prototype扩展此功能：
Function.method(‘curry’,function( ){
var args = arguments, that = this;
return function( ){
return that.apply(null, args.concat(arguments));
};
}); ／／有些事好像看起来不太对头。。。
curry方法通过创建一个保存着原始函数和要被套用的参数的闭包来工作。它返回另一个函数，该函数被调用时，会返回原始函数的结果，并传递调用curry时的参数加上当前调用的参数。它使用Array的concat方法连接两个参数数组。
糟糕的事，就像我们先前看到的那样，arguments数组并非一个真正的数组，所以它并没有concat方法。要避开这个问题，我们必须在两个arguments数组上都应用数组的slice方法。这样产生出拥有concat方法的常规数组。
Function.method(‘curry’,function( ){
var slice = Array.prototype.slice,
args = slice.apply(arguments),
that = this;
return function( ){
return that.apply(null,args.concat(slice.apply(arguments)));
};
});
记忆
函数可以将先前操作的结果记录在某个对象里，从而避免无谓地重复计算。这种优化被称为记忆。JavaScript的对象和数组要实现这种优化是非常方便的。
比如说，我们想要一个递归函数来计算Fibonacci数列。一个Fibonacci数字是之前两个斐波那契数字之和。最前面的两个数字是0和1.
var fibonacci = function( n ){
return n<2?n:fibonacci(n-1) + fibonacci(n-2);
};
for (var i = 0;i <=10;i += 1){
document.writeln(‘// ‘ + i + ‘: ‘ +fibonacci ( i ));
}
//0:0
//1:1
//2:1
//3:2
//4:3
//5:5
//6:8
//7:13
//8:21
//9:34
//10:55
这样是可以工作的，但它做了很多无谓的工作。斐波那契函数被调用了453次。我们调用了11次，而它自身调用了442次去计算可能已被刚计算过的值。如果我们让函数具备记忆功能，就可以显著地减少运算量。
我们在一个名为memo的数组里保存我们的储存结果，存储结果可以隐藏在闭包中。当函数被调用时，这个函数首先检查结果是否已存在，如果已存在，就立即返回这个结果。
var fibonacci = function ( ){
var memo = [0,1];
var fib = function ( n ){
var result = memo[n];
if (typeof result !== ‘number’){
result = fibo(n-1) + fib(n-2);
memo[n] = result;
}
return result;
};
return fib;
} ( );
这个函数返回同样的结果，但它只被调用了29次。我们调用了它11次，它调用了自己18次去取得之前存储的结果。
我们可以把这种技术推而广之，编写一个函数来帮助我们构造带记忆功能的函数。memoizer函数取得一个厨师的memo数组合formula函数。它返回一个管理meno存储和在需要时调用formula函数的recur函数。我们把这个recur函数和它的参数传递给formula函数：
var memoizer = function (memo,formula){
var recur = function (n){
var result = memo[n];
if(typeof result !==‘number’){
result = formula (recur,n);
memo[n] = result;
}
return result;
};return recur;
};
现在，我们可以使用memoize函数来定义斐波那契函数，提供其初始的memo数组合formula函数：
var fibonacci = memoizer([0,1],function(recur,n){
return recur (n-1) + recur(n-2);
});
通过设计这种产生另一个函数的函数，极大地减少了我们的工作量。例如，要产生一个可记忆的阶乘函数，我们只需提供基本的阶乘公式即可：
var factorial = memoizer([1,1],function(recur,n){
return n * recur(n-1);
});

第五章 继承
在大多数编程语言中，继承都是一个重要的主题。
在那些基于类的语言中，继承提供了两个有用的服务。首先，它是代码重用的一种形式。如果一个新的类与一个已存在的类大部分相似，那么你只需具体说明其不同点即可。代码重用的模式极为重要，因为它们可以显著地减少软件开发的成本。类继承的另一个好处是引入了一套类型系统的规范。由于程序员无需编写显示类型转换的代码，他们的工作量将大大减轻，这是一件很好的事情，因为类型转换会丧失类型系统在安全上的优势。
JavaScript是一门弱类型的语言，从不需要类型转换。对象继承关系变的无关紧要。对于一个对象来说重要的是它能做什么，而不是它从哪里来。
JavaScript提供了一套更为丰富的代码重用模式。它可以模拟那些基于类的模式，同时它也可以支持其他更具表现力的模式。在JavaScript中可能的继承模式有很多。在本章中，我们将研究几种最为直接的模式。当然还有很多更为复杂的构造模式，但保持简单通常是最好的。
在基于类的语言中，对象是类的实例，并且类可以从另一个类继承。JavaScript是一门基于原型的语言，这意味着对象直接从其他对象继承。
伪类
JavaScript的原型存在着诸多矛盾。它的某些复杂的语法看起来就像那些基于类的语言，这些语法问题掩盖了它的原型机制。它不直接让对象从其他对象继承，反而插入了一个多余的简洁层：通过构造器函数产生对象。
当一个函数对象被创建时，Function构造器产生的函数对象会运行类似这样的一些代码：
this.prototype = { constructor: this };
新函数对象被赋予了一个prototype属性，它的值是一个包含constructor属性且属性值为该新函数的对象。这个prototype对象是存放继承特征的地方。因为JavaScript语言没有提供一种方法去确定那个函数是打算用来做构造器的，所以每个函数都会得到一个prototype对象。constructor属性没什么用，重要的是prototye对象。
当采用构造器调用模式，即用new前缀去调用一个函数时，函数执行的方式会被修改。如果new运算符是一个方法而不是一个运算符，它可能会像这样执行：
Function.method(‘new’, function( ) {
／／创建一个新对象，它继承自构造器函数的原型对象。
var that = Object.create(this.prototype);
／／调用构造器函数，绑定this到新对象上。
var other = this.apply(that, arguments);
／／如果它的返回值不是一个对象，就返回该新对象。
return (typeof other === ‘object’ && other || that;
});
我们可以定义一个构造器并扩充它的原型：
var Mammal = function (name) {
this.name = name;
};
Mammal.prototype.get_name = function ( ) {
return this.name;
};
Mammal.prototype.says = function ( ){
return this.saying || ‘ ‘;
};
现在我们可以构造一个实例：
var myMammal = new Mammal(‘Herb the Mammal’);
var name = myMammal.get_name( ); ／／’Herb the Mammal’
我们可以构造一个伪类来继承Mammal，这时通过定义它的constructor函数并替换它的prototype为另一个Mammal的实例来实现的：
var Cat = function ( name ) {
this.name = name;
this.saying = ‘meow’;
};
／／替换Cat.prototype为一个新的Mammal实例。
Cat.prototype = new Mammal ( );
／／扩充新原型对象，增加purr和get_name方法。
Cat.prototype.purr = function ( n ) {
var i, s = ‘ ‘;
for(i = ;i < n;i +=1) {
if (s ){
s += ‘-‘;
}
s += ‘r’;
}
return s;
};
Cat.prototype.get_name = function ( ){
return this.says( ) + ‘ ‘ + this.name + ‘ ‘+ this.says( );
};
var myCat = new Cat(‘Henrietta’);
var says = myCat.says( ); //‘meow’
var purr = myCat.purr(5); //‘r-r-r-r-r’
var name = myCat.get_name( ); //‘meow Henrietta meow’
伪类模式的本意是想向面向对象靠拢，但它看起来格格不入。我们可以隐藏一些丑陋的细节，通过使用method方法来定义一个inherits方法实现：
Function.method(‘inherits’,function(Parent){
this.prototype = new Parent( );
return this;
});
我们的inherits和method方法都返回this，这样允许我们可以采用级联的形式编程。现在可以只用一行语句构造我们的Cat对象。
var Cat = function(name ){
this.name = name;
this.saying = ‘meow’;
}
.inherits(Mammal)
.method(‘purr’, function ( n ){
var i, s = ‘ ‘;
for( i = 0; i < n ; i += 1){
if ( s ){
s += ‘-‘;
}
return s;
})
.method(‘get_name’, function( ){
return this.says( ) + ‘ ‘+ this.name + ‘ ‘+ this.says( 0;
});
通过隐藏那些无谓的prototype操作细节，现在它看起来没那么怪异了。但是否真的有所改善呢？我们现在有了行为像’类’的构造函数，但仔细看它们，你会惊讶的发现：没有私有环境，所有的属性都是公开的。无法访问super父类的方法。
更糟糕的事，使用构造器函数存在一个严重的危害。如果你在调用构造器函数时忘记了在前面加上new前缀，那么this将不会被绑定到一个新对象上。悲剧的事，this将被绑定到全局对象上，所以你不但没有扩充新对象，反而破坏了全局变量环境。那真是糟透了。发生那样的情况时，既没有编译时警告，也没有运行时警告。
这是一个严重的语言设计错误。为了降低这个问题带来的风险，所有构造器函数都约定明明成首字母大写的形式，并且不以首字母大写的形式拼写任何其他的东西。这样我们至少可以通过目视检查去发现是否缺少了new前缀。一个更好的备选方案就是根本不使用new。
伪类形式可以给不熟悉JavaScript的程序员提供便利，但它也隐藏了该语言的真实的本质。借鉴类的表示法可能误导程序员去边协过于深入与复杂的层次结构。许多复杂的类层次结构产生的原因时静态类型检查的约束。JavaScript完全摆脱了那些约束。在基于类的语言中，类继承是代码重用的唯一方式。而JavaScript有着更多且更好的选择。
对象说明符
有时候，构造器要接受一大串参数。这可能令人烦恼，因为要记住参数的顺序非常困难。在这种情况下，如果我们编写构造器时让它接受一个简单的对象说明符，可能会更加友好。那个对象包含了将要构建的对象规格说明。所以，与其这样写：
var myObject = maker( f , l ,m , c , s);
不如这么写：
var myObject = maker ( {
firtst: f,
middle: m,
last: l,
state: s,
city:c
});
现在多个参数可以按照任何顺序排列，如果构造器会聪明地使用默认值，一些参数可以忽略掉，并且代码也更容易阅读。
当与JSON一起工作时，这种形式还可以有一个间接的好处。JSON文本只能描述数据，但有时数据表示的是一个对象，把该数据与它的方法关联起来是有用的。如果构造器取得一个对象说明符，就能让它轻松实现，因为我们可以简单地把JSON对象传递给构造器，而它将返回一个构造完全的对象。
原型
在一个纯粹的原型模式中，我们会摒弃类，转而专注于对象。基于原型的继承相比基于类的继承在概念上更为简单：一个新对象可以继承一个旧对象的属性。也许你对此感到陌生，但它真的很容易理解。你通过构造一个有用的对象开始，接着可以构造更多和那个对象类似的对象。这就可以完全避免把一个应用拆解成一系列嵌套抽象类的分类过程。
让我们先用对象字面量去构造一个有用的对象：
var myMammal = {
name: ‘Herb the Mammal’,
get_name: function ( ){
return this.name;
},
says: function( ){
return this.saying || ‘ ‘;
}
};
一旦有了一个想要的对象，我们就可以利用第三章中介绍过的Object.create方法构造出更多的实例来。接下来我们可以定制新的实例：
var myCat = Object.create(myMamml);
myCat.name = ‘Henrietta’;
myCat.saying = ‘meow’;
myCat.purr = function( n ){
var i ,s = ‘ ‘;
for (i = 0;i < n;i +=1 ){
if ( s ){
s+= ‘-‘;
}
s +=‘ r’;
}
return s;
};
myCat.get_name = function ( ){
return this.says + ‘ ‘ + this.name + ‘ ‘+ this.says;
};
这是一种差异化继承。通过定制一个新的对象，我们指明它所基于的基本对象的区别。
有时候它对某些数据结构继承于其他数据结构的情形非常有用。这里就有一个例子：假定我们要解析一门类似JavaScript或TEX那样用一对花括号指示作用域的语言。定义在某个作用域定义的条目在该作用域之外是不可见的。但在某种意义上，一个内部作用域会继承它的外部作用域。JavaScript在表示这样的关系上做得非常好。当遇到一个左花括号时block函数被调用。parse函数将从scope中寻找符号，并且当它定义了新的符号时扩充scope：
var block = function ( ){
／／记住当前的作用域。构造一个包含了当前作用域中所有对象的新作用域。
var oldScope = scope;
scope = Object.create( scope );
scope = Object.create(scope);
／／传递左花括号作为参数调用 advance。
advance(‘ { ‘);
／／使用新的作用域进行解析。
parse( scope );
／／传递右花括号作为参数调用advance并且抛弃新作用域，恢复原来老的作用域。
advance(‘ } ‘);
scope = oldScope;
};
函数化
迄今为止，我们所看到的继承模式的一个弱点就是没法保护隐私。对象的所有属性都是可见的。我们无法得到私有变量和私有函数。有时候这样没关系，但有时候却是大麻烦。遇到这些麻烦的时候，一些无知的程序员接受了一种伪装私有的模式。如果想构造一个私有属性，他们就给它起一个怪模怪样的名字，并且希望其他使用代码的用户假装看不到这些奇怪的成员。幸运的事，我们有一个更好的选择，那就是应用模块模式。
我们从构造一个生成对象的函数开始。我们以小写字母开头来命名它，因为它并不需要使用new前缀。该函数包括四个步骤。
1，创建一个新对象。有很多方式去构造一个对象。它可以构造一个对象字面量，或者它可以和new前缀连用去调用一个构造器函数，或者它可以使用Object.create方法去构造一个已经存在的对象的新实例，或者它可以调用任意一个会返回一个对象的函数。
2，有选择地定义私有实例变量和方法。这些就是函数中通过var语句定义的普通变量。
3，给这个新对象扩充方法。这些方法拥有特权去访问参数，以及在第二步中通过var语句定义的变量。
4，返回那个新对象。
这里是一个函数化构造器的伪代码模版：
var constructor = function (spec , my){
var that,其他私有的实例变量;
my = my || { };
把共享的变量和函数添加到my中
that = 一个新对象
添加给that的特权方法
return that;
};
spec对象包含构造器需要构造一个新实例的所有信息。spec的内容可能会被复制到私有变量中，或者被其他函数改变，或者方法可以在需要的时候访问spec的信息。（一个简化的方法是替换spec为一个单一的值。当构造对象过程中并不需要整个spec对象的时候，这是有用的。）
my对象是一个为继承链中的构造器提供秘密共享的容器。my对象可以选择性地使用。如果没有传入一个my对象，那么会创建一个my对象。
接下来，声明该对象私有的实例变量和方法。通过简单地声明变量就可以做到。构造器的变量和内部函数变成了该实例的私有成员。内部函数可以访问spec，my，that以及其他私有变量。接下来，给my对象添加共享的秘密成员。这是通过赋值语句来实现的：
my.member = value;
现在，我们构造了一个新对象并把它赋值给that。有很多方式可以构造一个新对象。我们可以使用对象字面量，可以用new运算符调用一个伪类构造器，可以在一个原型对象上使用Object.value方法，或者可以调用另一个函数化的构造器，传给它一个spec对象（可能就是传递给当前构造器的同一个spec对象）和my对象。my对象允许其他的构造器分享我们放到my中的资料。其他构造器可能也会把自己可分享的秘密成员放进my对象里，以便我们的构造器可以利用它。
接下来，我们扩充that，加入组成该对象接口的特权方法。我们可以分配一个新函数成为that的成员方法。或者，更安全地，我们可以先把函数定义为私有方法，然后再把他们分配给that：
var method = function( ){
…
};
that.methodical = methodical;
分两步去定义methodical的好处是，如果其他方法想要调用methodical，它们可以直接调用methodical（）而不是that.methodical。如果该实例被破坏或篡改，甚至是that.methodical被替换掉了，调用methodical的方法同样会继续工作，因为他们私有的methodical不受该实例被修改的影响。
最后，我们返回that。
让我们把这个模式应用到mammal例子里。此处不需要my，所以我们先抛开它，但会使用一个spec对象。
name和saying属性现在是完全私有的。只有通过get_name和says两个特权方法才可以访问它们。
var mammal = function ( spec ){
var that = { };
that.get_name = function( ){
return spec.name;
};
that.says = function ( ){
return spec.saying || ‘ ‘;
};
return that;
};
var myMammal = mammal({nameL’Herb’});
在伪类模式里，构造器函数Cat不得不重复构造器Mammal已经完成的工作。在函数化模式中那不再需要了，因为构造器Cat将会调用构造器Mammal，让Mammal去做对象创建中的大部分工作，所以Cat只需关注自身的差异即可。
var cat = function( spec ){
spec.saying =spec.saying || ‘meow’;
var that = mammal ( spec);
that.purr = function(n){
var i, s = ‘ ‘;
for( i = 0; i<n ;i+=1){
if( s ){
s+= ‘-‘;
}
s+= ‘r’;
}return s;
};
that.get_name = function( ){
return that.says( ) + ‘ ‘ + spec.name +’ ‘ +that.says( );
};
return that;
};
var myCat =cat( {name: ‘Henrietta’});
函数化模式还给我们提供了一个处理父类方法的方法。我们会构造一个superior方法，它取得一个方法名并返回调用那个方法的函数。该函数会调用原来的方法，尽管属性已经变化了。
Object.method(‘superior’,function(name){
var that = this,
method = that[name];
return function ( ){
return method.apply(that,arguments);
};
});
让我们在coolcat上试验一下，coolcat就像cat一样，除了它有一个更酷的调用父类方法的get_name方法。它只需要一点点的准备工作。我们会声明一个super_get_name变量，并且把调用superior方法所返回的结果赋值给它。
var coolcat = function( spec ){
var that = cat(spec),
super_get_name = that.superior(‘get_name’);
that.get_name = function(n){
return ‘like’ + super_get_name( ) + ‘baby’;
};
return that;
};
var myCoolCat = coolcat({name: ‘Bix’ });
var name = myCoolCat.get_name( );
／／’like moew Bix meow baby’
函数化模式有很大的灵活性。它相比伪类模式不仅带来的工作更少，还让我们得到的更好的封装和信息隐藏，以及访问父类方法的能力。
如果对象的所有状态都是私有的，那么该对象就成为一个’防伪’对象。该对象的属性可以被替换或删除，但该对象的完整性不会受到损害。如果我们用函数化的样式创建一个对象，并且该对象的所有方法都不使用this或that，那么该对象就是持久性的。一个持久性对象就是一个简单功能函数的集合。
一个持久性的对象不会被入侵。访问一个持久性的对象时，除非有方法授权，否则攻击者不能访问对象的内部状态。
部件
我们可以从一套部件中把对象组装出来。例如，我们可以构造一个给任何对象添加简单时间处理特性的函数。他会给对象添加一个on方法，一个fire方法和一个私有的时间注册表对象：
var eventuality = function( that ){
var registry = { };
that.fire = function ( event ){
／／在一个对象上触发一个事件。该事件可以是一个包含事件名称的字符串，
／／或者是一个拥有包含事件名称的type属性的对象。
通过on方法注册的事件处理程序中匹配事件名称的函数将被调用。
var array,
func,
handler,
i,
type = typeof event ===‘string’ ? event : event.type;
／／如果这个事件存在一组事件处理程序，那么就遍历它们并按顺序依次执行。
if ( registry.hasOwnProperty( type )){
array = registry[type];
for( i = 0; i< array.length ; i+=1){
handler = array[i];
／／每个处理程序包含一个方法和一组可选的参数。
／／如果该方法是一个字符串形式的名字，那么寻找到该函数。
func = handler.method;
if( typeof = func ===‘string’){
func = this[func];
／／调用一个处理程序。如果该条目包含参数，那么传递它们过去。否则，传递该事件对象。
func.apply(this,
handler.parameters || [event]);
}} 
return this;
};
that.on = function(type,method,parameters){
／／注册一个事件。构造一条处理程序条目。将它插入到处理程序数组中，
／／如果这种类型的事件还不存在，就构造一个。
var handler = {
method: method,
parameters: parameters
};
if ( registry.hasOwnProperty(type) {
registry[type].push(handler);
} else {
registry[type] = [handler];
}
return this;
}
return that;
};
我们可以在任何单独的对象上调用eventuality，授予它事件处理方法。我们也可以赶在that被返回前在一个构造器函数中调用它。
eventuality(that);
用这种方式，一个构造器函数可以从一套部件中把对象组装出来。JavaScript的弱类型在此处是一个巨大的优势，因为我们无需花费精力去了解对象在类型系统中的继承关系。相反，我们只需专注于它们的个性特征。
如果我们想要eventuality访问该对象的私有状态，可以把私有成员my传递给它。

数组
数组是一段线性分配的内存，它通过整数计算偏移并访问其中的元素。数组是一种性能出色的数据结构。不幸的是，JavaScript没有像此类数组一样的数据结构。
作为替代，JavaScript提供了一种拥有一些类数组特性的对象。它把数组的下标转变成字符串，用其作为属性。它明显比一个真正的数组慢，但它使用起来更方便。它的属性的检索和更新的方式与对象一模一样，只不过多一个可以用整数作为属性名的特性。数组有自己的字面量格式。数组也有一套非常有用的内置方法。
数组字面量
数组字面量提供了一种非常方便地创建新数组的表示法。一个数组字面量是在一对方括号中包围零个或多个用逗号分隔的值的表达式。数组字面量允许出现在任何表达式可以出现的地方。数组的第一个值将获得属性名’0’，第二个值将获得属性名’1’，以此类推：
var empty = [ ];
var numbers = [
‘zero’,’one’,’two’,three’,’four’,
‘five’,’six’,’seven’,’eight’,’nine’
];
empty[1]  //undefined
numbers[1]  //‘one’
empty.length   // 0
numbers.length // 10
对象字面量：
var numbers_object = {
‘0’: ‘zero’,’1’: ‘one’,’2’: ‘two’,
…
‘9’: ‘nine’
};
两者产生的结果相似。numbers和number_object都是包含10个属性的对象，并且那些属性刚好有相同的名字和值。但是他们也有一些显著的不同。numbers继承自Array.prototype，而numbers_object继承自Object.prototype，所以numbers继承了大量有用的方法。同时，numbers也有一个诡异的length属性，而numbers_object则没有。
在大多数语言中，一个数组的所有元素都要求是相同的类型。JavaScript允许数组包含任意混合类型的值：
var misc = [
‘string’, 98.6 ,true ,false , null ,undefined,
[‘nested’,’array’],{object: true},NaN,
Infinity
};
misc.length  // 10
长度
每个数组都有一个length属性。和大多数其他语言不同，JavaScript数组的length是没有上界的。如果你用大于或等于当前length的数字作为下标来存储一个元素，那么length值会被增大以容纳新元素，不会发生数组越界错误。
length属性的值是这个数组的最大整数属性名加上1.它不一定等于数组里的属性的个数：
var myArray = [ ];
myArray.length    // 0
myArray[1000000] = true;
myArray.length // 1000001
//myArray 只包含一个属性。
［］后置下标运算符把它所含的表达式转换成一个字符串，如果该表达式有toString方法，就使用该方法的值。这个字符串将被用作属性名。如果这个字符串看起来像一个大于等于这个数组当前length且小于4294967295的正整数，那么这个数组的length就会被重新设置为新的下标加1.
你可以直接设置length的值。设置更大的length不会给数组分配更多的空间。而把length设小将导致所有下标大于等于新length的属性被删除：
numbers.length = 3;
//numbers是[‘zero’,’one’,’two’]
通过把下标指定为一个数组的当前length，可以附加一个新元素到该数组的尾部：
numbers[numbers.length] = ‘shi’;
//numbers是 [‘zero’,’one’,’two’,’shi’]
有时用push方法可以更方便地完成同样的事情：
numbers.push(‘go’);
//numbers是[‘zero’,’one’,’two’,’shi’,’go’]
删除
由于JavaScirpt的数组其实就是对象，所以delete运算符可以用来从数组中移除对象：
delete numbers[2];
／／numbers是[‘zero’,’one’,’undefined’,’shi’,’go’]
不幸的是，那样会在数组中留下一个空洞。这是因为排在被删除元素之后的元素保留着他们最初的属性。而你通常想要的是递减后面每个元素的属性。
幸运的是，JavaScirpt数组又一个splice方法。它可以对数组做个手术，删除一些元素并将它们替换为其他元素。第一个参数是数组中的一个序号，第二个参数是要删除的元素个数。任何额外的参数会在序号那个点的位置被插入到数组中：
numbers.splice(2,1);
／／numbers是[‘zero’,’one’,’shi’,’go’]
值为’shi'的属性的键值从 3 变到 2。因为被删除属性后面的每个属性必须被移除，并且以一个新的键值重新插入，这对于大型数组来说可能会效率不高。
枚举
因为JavaScirpt的数组其实就是对象，所以for in语句可以用来遍历一个数组的所有属性。遗憾的是，for in无法保证属性的顺序，而大多数要遍历数组的场合都期望按照阿拉伯数字顺序来产生元素。此外，可能从原型链中得到意外属性的问题依旧存在。
幸运的是，常规的for语句可以避免这些问题。JavaScirpt的for语句和大多数类c语言相似。他被第三个从句控制－第一个初始化循环，第二个执行条件检测，第三个执行增量计算。
var i;
for ( i = 0; i<myArray.length; i+=1){
document.writeln(myArray[i]);
}
容易混淆的地方
在JavaScript编程中，一个常见的错误是在必须使用数组时使用了对象，或者在必须使用对象时使用了数组。其实规则很简单：当属性名是小而连续的整数时，你应该使用数组。否则，使用对象。
JavaScript本身对于数组和对象的区别是混乱的。typeof运算符报告数组的类型是’object'这没有任何意义。
JavaScript没有一个好的机制来区别数组和对象。我们可以通过定义自己的is_array函数来弥补这个缺陷：
var is_array = function (value){
return value && 
typeof value === ‘object’ &&
value.constructor === Array;
};
遗憾的是，它在识别从不同的窗口或帧里构造的数组时会失败。有一个更好的方式去判断一个对象是否为数组：
var is_array = function (value) {
return Object.prototype.toString.apply(value) === ‘[object Array]’;
};
方法
JavaScript提供了一套数组可用的方法。这些方法是被储存在Array.prototype中的函数。
举例来说，假设我们想要给array增加一个方法，它允许我们对数组进行计算
Array.method(‘reduce’,function(f,value){
var i;
for(i = 0;i< this.length; i += 1){
value = f(this[i],value);
}
return value;
});
通过给Array.prototype扩充一个函数，每个数组都继承了这个方法。在这个例子里，我们定义了一个reduce方法，它接受一个函数和一个初始值作为参数。它遍历这个数组，以当前元素和该初始值为参数调用这个函数，并且计算出一个新值。当完成时，它返回这个值。如果我们传入一个把两个数字想家的函数。它会计算出相加之和。如果我们传入把两个数字相乘的函数，它会计算两者的乘积：
／／创建一个数字数组。
var data = [4,8,15,16,23,42];
／／定义两个简单的函数。一个是把两个数字相加，另一个是把两个数字相乘。
var add = function (a,b){
return a + b;
};
var mult = function( a,b){
return a * b;
};
调用data的reduce方法，传入add函数。
var sum = data.reduce(add,0);  //sum is 108
//再次调用reduce方法，这次传入mult函数。
var product = data.reduce(mult,1);
//product是 7419990。
因为数组其实就是对象，所以我们可以直接给一个单独的数组添加方法：
／／给 data数组添加一个total方法。
data.total = function( ){
return this.reduce(add,0);
};
total = data.total( ); // total is 108
因为字符串呢total不是整数，所以给数组增加一个total属性不会改变它的length。当属性名是整数时，数组才是最有用的，但它们依旧是对象，并且对象可以接受任何字符串作为属性名。
指定初始值
JavaScript的数组通常不会预置值。如果你用［］得到一个新数组，它将是空的。如果你访问一个不存在的元素，得到的值则是undefined。如果你知道这个问题，或者你在尝试获取每个元素之前都很有预见性地设置它的值，那就万事大吉了。但是，如果你实现的算法是假设每个元素都从一个已知的值开始 （例如0），那么你必须自己准备好这个数组。JavaScript应该提供一些类似Array.dim这样的方法来做这件事情，但我们可以很容易纠正这个疏忽：
Array.dim = function(dimension, initial){
var a = [ ], i;
for (i = 0;i<dimension;i += 1){
a[i] = initial;
}
return a;
};
／／创建一个包含10个0的数组。
var myArray = Array.dim(10,0);
JavaScript没有多维数组，但就像大多数类c语言一样它支持元素为数组的数组：
var matrix = [
[0,1,2],
[3,4,5],
[6,7,8]
];
matrix[2][1]  //7
为了创建一个二维数组或者说数组的数组，你必须自己去创建那个第二维的数组：
for ( i = 0;i<n; i += 1){
my_array[i] = [ ];
}
／／注意：Array.dim(n,[ ] )在这里不能工作。
／／如果使用它，每个元素都指向同一个数组的引用，那后果不堪设想。
一个空的矩阵的每个单元会拥有一个初始值undefined。如果你希望它们有不同的初始值，你必须明确地设置它们。同样地，JavaScript应该对矩阵提供更好的支持。好在我们也可以补上它：
Array.matrix = function(m,n,initial){
var a,i,j,mat = [ ];
for(i = 0;i<m;i +=1){
a = [ ];
for(j = 0;j<n; j+=1){
a[j] = initial;
}
mat[i] = a;
}
return mat;
}
／／构造一个用0填充的4*4矩阵。
var myMatrix = Array.matrix(4,4,0);
document.writeln(myMatrix[3][3]);   //0
／／用来构造一个单位矩阵的方法。
Array.identity = function (n){
var i ,mat = Array.matrix(n,n,0);
for (i = 0;i<n;i += 1){
mat[i][i] = 1;
}return mat;
};
myMatrix = Array.identity(4);
document.writeln(myMatrix[3][3]);   //1

正则表达式
JavaScript的许多特性都借鉴自其他语言。语法借鉴自Java，函数借鉴自Scheme，原型继承借鉴自Self。而JavaScript的正则表达式则借鉴自Perl。
正则表达式是一门简单语言的语法规范。它应用在一些方法中，对字符串中的信息实现查找，替换和提取操作。可处理正则表达式的方法有regexp.exec,regexp.test,string.match,string.replace,string.search和string.split。通常来说，在JavaScript中正则表达式相较于等效的字符串处理有着显著的性能优势。
正则表达式起源于对形式语言的数学研究。Ken Thompson基于Stephen Kleene对type-3语言的理论研究写出了一个切实可用的模式匹配器，它能够被嵌入到编程语言和像文本编辑器这样的工具中。
在JavaScript中，正则表达式的语法是对Perl版本的改进和发展，它非常接近于贝尔实验室最初提出的构想。正则表达式的书写规则出奇地复杂，在某些位置上的字符串可能解析为运算符，而仅在位置上稍微不同的相同字符串却可能被当作字面量。比不易书写更糟糕的是，这使得正则表达式不仅难以阅读，而且修改时充满危险。要想正确地阅读它们，就必须对正则表达式的整个复杂性有着相当透彻的理解。为了缓解这个问题，我对它的规则进行了些许简化。这里所展示的正则表达式可能稍微有些不够简洁，但使用它们的时候不会那么容易出错。这是值得的，因为维护和调试正则表达式可能非常困难。
现在的正则表达式的规则并不总是严格的，但它们非常有用。正则表达式趋向于极致的简洁，甚至不惜容忍含义的模糊。在最简单的形式下，它们是易于使用的，但可能很快就会变得让人费解。JavaScript的正则表达式难以分段阅读，因为他们不支持注释和空白。正则表达式的所有部分都被紧密排列在一起，使得它们几乎无法被辨认。当它们在安全应用中进行扫描和验证时，这点就需要特别地留意。如果你不能阅读和理解一个正则表达式，你如何能确保它对所有的输入都能正确地工作呢？然而，尽管有这些明显的缺点，但正则表示还是被广泛地应用着。
一个例子
这里有一个例子。它是用来匹配URL的正则表达式。书页的行宽有限，所以我把它拆开来写成两行。在JavaScript程序中，正则表达式必须写在一行中。空白需要特别注意：
var parse_url = /^(?:[A-Za-z]:)?(\/{0,3})([0-9.\-A-Za-z]+)(?::(\d+))?(?:\/([^?#]*))?(?:\?([^#*))?(?:#(.*))?$/;
var url = ‘http://www.ora.com:80/goodparts?q#fragment';
让我们调用parse_url的exec方法。如果能成功匹配我们传给它的字符串，它会返回一个数组，该数组包含了从这个url中提取出来的片段：
var url = “http://www.ora.com:80/goodparts?q#fragment”;
var result = parse_url.exec(url);
var names = [‘url’,’scheme’,’slash’,’host’,’port’,’path’,’query’,’hash’];
var blanks = ‘      ‘;
var i;
for (i = 0;i<names.length;i += 1){
document.writeln(names[i] + ‘:’ + blanks.substring(names[i].length),result[i]);
}
这段代码产生的结果如下：
url:http://www.ora.com:80/goodparts?q#fragment
scheme: http
slash: //
host: www.ora.com
port: 80
path: goodparts
query: q
hash: fragment
 让我们分解parse_url的各个部分，看看它是如何工作的：
^
^字符表示此字符串的开始。它是一个锚，指引exec不要跳过那些不像url的前缀，只匹配那些从开头就像URL一样的字符串：
(?:([A-Za-z]+):)?
这个因子匹配一个协议名，但仅当它后面跟随一个：冒号的时候才匹配。(?:…)表示一个非捕获型分组。后缀？表示这个分组是可选的。它表示重复0次或1次。（。。。）表示一个捕获型分组。一个捕获型分组会复制它所匹配的文本，并把其放到result数组里。每个捕获型分组都会被指定一个编号。第一个捕获型分组的编号是1，所以该分组所匹配的文本副本会出现在result[1]中。［。。。］表示一个字符类。A-Za-z这个字符类包含26个大写字母和26个小写字母。连字符（－）表示范围从A-Z。后缀＋表示这个字符类会被匹配一次或多次。这个组后面跟着字符：，它会按字面进行匹配：
(\/{0,3})
下一个因子是捕获型分组2。\/表示应该匹配／斜杠。它用\反斜杠来进行转义，这样它就不会被错误地解释为这个正则表达式的结束符。后缀｛0，3｝表示／会被匹配0次，或者1-3次：
([0-9.\-A-Za-z]+)
下一个因子是捕获型分组3。它会匹配一个主机名，由一个或多个数字，字母以及.或－字符组成－会被转义为\-以防止与表示范围的连字符相混淆：
(?::(\d+))?
下一个可选的因子匹配端口号，它是由一个前置：加上一个或多个数字而组成的序列。\d表示一个数字字符。一个或多个数字组成的数字串会被捕获型分组4捕获：
(?:\/([^?#]*))?
接下来是另一个可选的分组。该分组以一个／开始。之后的字符类[^?#]以一个^开始，它表示这个类包含除？和#之外的所有字符。*表示这个字符类会被匹配0次或多次。
注意我在这里的处理是不严谨的。这个类匹配除？和#之外的所有字符，其中包括了行结束符，控制字符，以及其他大量不应在此被匹配的字符。大多数情况下，它会按照我们的预期去做，但某些恶意文本可能会有渗漏进来的风险。不严谨的正则表达式是一个常见的安全漏洞发源地。写不严谨的正则表达式比写严谨的正则表达式要容易得多。
(?:\?([^#]*))?
接下来，我们还有一个以一个？开始的可选分组。它包含捕获型分组6，这个分组包含0个或多个非#字符。
(?:#(.*))?
我们最后一个可选分组是以#开始的。.会匹配除行结束符以外的所有字符。
$
$表示这个字符串的结束。它保证在这个URL的尾部没有其他更多的内容了。
以上便是正则表达式parse_url的所有因子了。
parse_url的正则表达式还可以编写得更复杂，但我不建议这样做。短小精悍的正则表达式是最好的。唯有如此，我们才有信心让它们正确地工作并在需要时能顺利地修改它们。
JavaScript的语言处理程序之间兼容性非常高。这门语言中最没有移植性的部分就是对正则表达式的实现。结构复杂或令人费解的正则表达式很可能导致移植性问题。在执行某些匹配时，嵌套的正则表达式也能导致极恶劣的性能问题。因此简单是最好的策略。
让我们来看另一个例子：一个匹配数字的正则表达式。数字可能由一个整数部分加上一个可选的负号、一个可选的小数部分和一个可选的指数部分组成：
var parse_number = /^-?\d+(?:\.\d*)?(?:e[+\-]?\d+)?$/i;
var test = function( num ){
document.writeln(parse_number.test(num));
};
test(‘1’);   //true
test(‘number’)  //false
...
…
parse_number成功地检验出这些字符串中，那些符合我们的规范，哪些不符合，但对那些不符合的字符串，它并没有告诉我们测试失败的缘由和位置。
让我们来分解parse_number:
/^      $/i
我们又用^和$来框定这个正则表达式。它指引这个正则表达式对文本中的所有字符都进行匹配。如果我们省略了这些标识，那么只要一个字符串包含一个数字，这个正则表达式就会进行匹配。但有了这些标识，只有当一个字符串的内容仅为一个数字时，它才会告诉我们。如果我们仅包含^，它将匹配以一个数字开头的字符串。如果我们仅包含¥，则匹配以一个数字结尾的字符串。
i标识表示匹配字母时忽略大小写。在我们的模式中唯一可能出现的字母是e。我们希望既能匹配e，也能匹配E。我们可以把e因子写成[Ee]或(?:E|e),但不必这么麻烦，因为我们使用了标识符i。
-?
负号后面的？后缀表示这个负号是可选的。
\d+
\d的含义和[0-9]一样。它匹配一个数字。后缀＋指引它可以匹配一个或多个数字。
(?:\.\d*)?
(?:….)?表示一个可选的非捕获型分组。通常用非捕获型分组来替代少量不优美的捕获型分组是很好的方法，因为捕获会有性能上的损失。这个分组会匹配后面跟随的0个或多个数字的小数点：
(/.:e[+\-]?\d+)?
这是另外一个可选的捕获型分组。它会匹配一个e或E、一个可选的正负号及一个或多个数字。
结构

有两个方法来创建一个RegExp对象。在以前的例子中我们可以看到，优先考虑的方法是使用正则表达式字面量。
正则表达式字面量被包围在一对斜杠中。这有点令人难以捉摸，因为斜杠也被用作除法运算符和注释符。
RegExp能设置三个标识。他们分别由字母g，i和m来标示，我把它们列在表7-1中。这些标识能直接添加在RegExp字面量的末尾：
／／构造一个匹配JavaScript字符串的正则表达式
var my_regexp = /“(?:\\.|[^\\\”])*”/g;
g：全局的（匹配多次；不同的方法对g标识的处理各不相同
i：大小写不敏感
m：多行（^和$能匹配行结束符）
创建一个正则表达式的另一个方法是使用RegExp构造器。这个构造器接受一个字符串，并把它编译为一个RegExp对象。创建这个字符串时请多加小心，因为反斜杠在正则表达式和在字符串字面量中有一些不同的含义。通常需要双写反斜杠，以及对引号进行转义：
／／创建一个匹配JavaScript字符串的正则表达式。
var  my_regexp = new RegExp(“\”(?:\\\\.|[^\\\\\\\”])*\””,’g’);
第二个参数是一个指定标识的字符串。RegExp构造器适用于必须在运行时动态生成正则表达式的情形。
RegExp对象包含的属性：
global：如果标识g被使用，值为true
ignoreCase：如果标识i被使用，值为true
lastIndex：下一次exec匹配开始的索引。初始值为0
multiline：如果标识m被使用，值为true
source：正则表达式源码文本
用正则表达式字面量创建RegExp对象共享同一个单例：
function make_a_matcher( ){
return /a/gi;
}
var x = make_a_matcher( );
var y = make_a_matcher( );
／／当心：x和y是相同的对象！
x.lastIndex = 10;
document.writeln(y.lastIndex);   //10
元素
让我们进一步看看那些构成正则表达式的元素。
正则表达式分支
一个正则表达式分支包含一个或多个正则表达式序列。这些序列被|（竖线）字符分隔。如果这些序列中的任何一项符合匹配条件，那么这个选择就被匹配。它尝试按顺序依次匹配这些序列项。所以：
“into”.match(/in|int/)
会在into中匹配in。但它不会匹配int，因为in已经被匹配成功了。
正则表达式序列
一个正则表达式包含一个或多个正则表达式因子。每个因子能选择是否跟随一个量词，这个量词决定着这个因子被允许出现的次数。如果没有指定这个量词，那么该因子只会被匹配一次。
正则表达式因子
一个正则表达式可以是一个字符，一个由圆括号包围的组、一个字符类，或者是一个转义序列。除了控制字符和特殊字符以外，所有的字符都会被按照字面处理：
\  /  [  ] ( _ {  } ? + * | . ^ $
如果你希望上面列出的字符按字面去匹配，那么必须要用一个\前缀来进行转义。你如果拿不准的话，可以给任何特殊字符都添加一个\前缀来使其字面化。注意\前缀不能使字母或者数字字面化。
一个未被转义的. 会匹配除行结束符以外的任何字符。
当lastIndex属性值为0时，一个未被转义的^会匹配文本的开始。当指定了m标识时，它也能匹配行结束符。
一个未转义的$将匹配文本的结束。当指定了m标识时，它也能匹配行结束符。
正则表达式转义
反斜杠字符在正则表达式因子中与其在字符串中一样均表示转义，但是在正则表达式因子中，它稍有一点不同。
像在字符串一样，\f是换页符,\n是换行符，\r是回车符，\t是制表符，并且\u允许指定一个Unicode字符来表示一个十六进制的常量。但是在正则表达式因子中，\b不是退格符。
\d等同于[0-9]，它匹配一个数字。\D则表示与其相反的:[^0-9]。
\s等同于[\f\n\r\t\u000B\u0020\u00A0\u2028\u2029]。这是Unicode空白符的一个不完全子集。\s则表示与其相反的：[^\f\n\r\t\u000B\u0020\u00A0\u2028\u2029]。
\w等同于[0-9A-Z_a-z]。\W则表示与其相反的：[^0-9A-Z_a-z]。\W本意是希望表示出现在话语中的字符。遗憾的是，它所定义的类实际上对任何真正的语言来说都不起作用。
如果你需要匹配信件一类的文本，你必须指定自己的类。
一个简单的字母类是[A-Za-z\u00C0-\u1FFF\u2800-\uFFFD]。它包括所有的Unicode字母，但它也包括成千上万非字母的字符。Unicode是巨大而复杂的。构造一个基本多语言面的精确字母类是有可能的，但它将会变的庞大而低效。JavaScript的正则表达式对国际化的支持非常有限。
\b被指定为一个字边界标识，它方便用于对文本的字边界进行匹配。遗憾的是，它使用\w去寻找字边界，所以它对多语言应用来说是完全无用的。这并不是一个好的特性。
\1是指向分组1所捕获到的文本的一个引用，所以它能被再次匹配。例如，你能用下面的正则表达式来搜索文本中的重复的单词：
var doubled_words = 
/([A-Za-z\u00C0-\U1FFF\U2800-\UFFFD]+)\s+\1/gi;
double_words会寻找重复的单词（包括一个或多个字母的字符串），该单词的后面跟着一个或多个空白，然后再跟着与它相同的单词。
\2是指向分组2的引用，，\3是指向分组3的引用，依此类推。
正则表达式分组
分组共有四种
捕获型
一个捕获型分组是一个被包围在括号中的正则表达式分支。任何匹配这个分组的字符都会被捕获。没个捕获型分组都被指定了一个数字。在正则表达式中第一个捕获（的分组是1，第二个捕获（的分组是2.
非捕获型
非捕获型分组有一个（？：前缀。非捕获型分组仅做简单的匹配，并不会捕获所匹配的文本。这会带来微弱的性能优势。非捕获型分组不会干扰捕获型分组的编号。
向前正向匹配
向前正向匹配分组有一个（？＝前缀。它类似于非捕获型分组，但在这个组匹配后，文本回到回到他开始的地方，实际上并不匹配任何东西。这不是一个好的特性。
向前负向匹配
向前负向匹配分组有一个（？！前缀。它类似于向前正向匹配分组，但只有当它匹配失败时它才继续向前进行匹配。这不是一个好的特性。
正则表达式字符集
正则表达式字符集是一种指定一组字符的便利方式。例如，如果向匹配一个元音字母，我们可以写作（?:a|e|i|o|u),但它可以被更方便地写成一个类[aeiou].
类提供另外两个便利。第一个是能够指定字符范围。所以一组由32个ASCII的特殊字符组成的集合：
! “ # $ % & ‘( ) * + , -./:
;<=>?@[ \ ] ^ _ `{|}~
你可以写成这样：
稍微好看一些的写法是：
[!-\/:-@\[-`{-~]
它包括从！到／、从：到@、从［到｀和从［到~的字符。但它看起来依旧相当难以阅读。
另一个方便之处是类的求反。如果［后的第一个字符是^，那么这个类会排除这些特殊的字符。
所以[^!…]会匹配任何一个非ASCII特殊字符的字符。
正则表达式转义
字符类内部的转义规则和正则表达式因子的相比有些不同。此处的[\b]是退格符。下面是在字符类中需要要被转义的特殊字符：- / [ \ ] ^
正则表达式量词
正则表达式因子可以用一个正则表达式量词后缀来决定这个因子应该被匹配的次数。包围在一对花括号中的一个数字表示这个因子应该被匹配的次数。所以，/www/匹配的和/w{3}/一样，{3,6}会匹配3，4，5，或6次，{3}会匹配三次或更多次。
？等同于｛0，1｝，＊等同于｛0，｝，＋则等同于｛1，｝。
如果只有一个量词，表示趋向于进行贪婪性匹配，即匹配尽可能多的副本直至达到上限。如果这个量词附加一个后缀？，则表示趋向于进行非贪婪性匹配，即止匹配必要的副本就好。一般情况下最好坚持使用贪婪性匹配。

方法
JavaScript包含了一套小型的可用在标准类型上的标准方法集。
Array
