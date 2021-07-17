## JS学习

1、浏览器分为两部分：渲染引擎和JS引擎，其中渲染引擎用来解析HTML和CSS，俗称内核，比如chrome的blink；JS 引擎也叫JS 解释器，用来读取网页中的JS代码，对其处理后运行，比如chrome的V8

2、JS 由JS语法（ECMAScript）、页面文档对象模型（DOM）、浏览器对象模型（BOM）

ECMAScript规定了JS编程语法和基础核心知识。

DOM对页面中的各个元素进行操作

BOM对浏览器中的元素进行操作

3、JS有三种书写位置：行内、内嵌、外部。

一、JS三种书写位置
行内式JS
<input type=”button” value=”点我试试” onclick=”alert(‘hello world’)”/>
可以单行或者少行JS代码写在HTML标签的事件属性中（以on开头的属性）如onclick；
注意单双引号的使用：在HTML中我们推荐使用双引号，JS中推荐使用单引号；
可读性差，在HTML中编写大量JS代码时不方便阅读；
引号易错，引号的多层嵌套匹配时非常容易弄混；
特使情况下使用

内嵌式JS

<script>
alert (‘Hello world~’);
   </script>
   可以将多行JS代码写到<script>标签中；
   内嵌JS是学习时常用的方法
外部JS文件

<script src=”my.js”></script>
利于HTML页面代码结构化，把大段的代码独立于HTML页面之外，既美观，也方便文件级别的复用；
引用外部js文件的script标签中间不能够写代码；
适用于JS代码量较大的情况

4、JS两种注释方法
1、单行注释：//注释     快捷键：Ctrl+/
2、多行注释: /*注释*/    快捷键：shift+alt+a

5、JS输入输出语句
1、常用语句；
     prompt(‘info’)       这是浏览器弹出输入框，用户可以输入，归属浏览器
     alert(‘msg’)         这是浏览器弹出警示框，展示给用户的，归属浏览器
     console.log(‘msg’)    这是浏览器控制台打印输出信息，控制台输出，给程序员测试仪的，归属浏览器
注意语句前后有<script>

6、变量：变量用于存放数据，我们通过变量名获取数据，甚至可以修改，本质是程序在内存中申请的一块用来存访数据的空间。

变量使用分两步：声明标量、赋值。

var age;//声明一个名称为age的变量；age=10;//把age这个变量赋值为10；

变量的初始化就是声明并赋值：var age =10;//声明变量并赋值为10

7、声明变量的时候数值不加引号，其他一般加单引号。

8、HTML 中的脚本必须位于 <script> 与 </script> 标签之间。

脚本可被放置在 HTML 页面的 <body> 和 <head> 部分中。浏览器会解释并执行位于 <script> 和 </script>之间的 JavaScript 代码 
