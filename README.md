# Professional-JavaScript-for-Web-Developers 

## 一、JS简介
JavaScript是不同于Java的动态语言，创造之初是为了在浏览器中提供一些实现逻辑，当时网速较慢，如果一个表单输入提交后，等了几十秒才返回某个字段是必填的，则用户体验非常不佳，此时JS应运而生。

JS包含ES(ECMAScript)、DOM、BOM，ES是JS的标准规范，DOM则是一个页面中的不同标签，BOM则是页面外的一些浏览器信息，例如location中的URL信息，naviator中的浏览器信息，cookies的操作，XMLHttpRequest和MicroSoftXMLHttp等ajax对象，screen获取浏览器视窗信息等等。

## 二、在HTML中使用JS
在html中使用JS，可以在页面中使用script标签，可以直接在页面中静态写死，也可以在JS中异步插入。一般会把script标签放在页面底部，因为页面在解析过程中如果遇到script标签，会停止解析，然后去执行script标签中的JS，如果是引入外部文件，那么就会等到文件下载完成后才继续解析，如果script引入的文件过大或者内容过多，那么会造成浏览器长时间空白，用户体验不佳。

script标签有两个属性比较重要，分别是defer(延迟加载)和async(异步)，如果有defer属性，那么脚本会在HTML文档完全呈现之后才执行，而且会按照指定它们的顺序，并且先于DOMContentLoaded执行(规范要求，但实际不保证)。如果有async属性表示当前脚本不会阻塞HTML文档的呈现，也不必等待其他脚本，但是不能保证脚本会按照在页面出现的顺序执行。注意异步脚本不要在加载期间修改DOM，因为不保证在DOMContentLoaded事件触发之后执行，但能保证会在load事件触发之前执行。
一般会采取外部引入文件的形式加载脚本，这样的好处是可维护和可缓存。

## 三、基本概念

## 四、变量、作用域及内存问题
JS中的变量分为基本类型和引用类型，基本类型有undefined、null、number、string、boolen，ES6中的symbol，引用类型就是对象，而函数，数组，正则都是对象。
typeof操作符可以返回变量的类型，其中会将null返回object，所以一般判定类型都会使用Object.propotype.toString.call()，会返回"[object XXXX]"，XXX为对应类型的名称。
想要获得函数的参数情况，可以在内部使用arguments进行获取，它是一个类似数组的变量，可以使用[].slice.call()，将其中的值复制出来。函数传参的时候，如果参数是基本类型，那么会是值复制的形式处理，如果是对象，那么复制的值就是对象的地址，也就是指向堆中的指针，这两种方式都会在函数内部生成一个变量去储存，也即是局部对象。

JS有一个全局作用域，在浏览器中是window，它没有块级作用域(ES6中有)，但是有函数作用域。在函数作用域中的变量是局部变量，如果不用var声明，则视为全局变量。

可以想象成一个栈，栈底是全局作用域，函数被调用时则会产生自己的执行环境，将其压入栈执行结束后执行环境销毁(即出栈)，将控制权交出。JS在搜寻变量时就会沿着当前的执行环境向栈底(全局作用域)搜寻，直到匹配到吻合的命名，则能取到值，当在全局作用域中都未能找到时，则说明该变量未被创建，值为undefined。
JS的垃圾处理机制分为两种，引用计数和标记清除。引用计数的意思是，如果某个变量被引用了，则将其计数的token增加1，每间隔一段时间进行一次检测，将引用计数为0的变量所占内存进行释放，这种方法无法处理循环引用的问题。标记清除的意思是，变量被创建时都是可达的，每间隔一段时间进行一次检测，当某个变量时被标记为不可达时，那么就会将其所占的内存进行释放。

JS内存管理机制可以使得我们可以在很多时候不需要处理内存问题，但是对于全局变量，我们还是需要进行处理。

## 五、引用类型
数组对象中的length属性，它不是只读的，我们可以通过设置其值，来影响数组的大小，而且还可以使用XXX[Y](其中Y是number)，Y的值是多少，那么数组的长度则是Y+1。

ES5之后可以通过Array.isArray确定某个变量是否是数组，将数组排序的时候，可以调用sort方法，传入一个比较函数作为参数，如果希望顺序，则返回第二个数和第一个数的差，如果希望逆序，则返回第一个数和第二个数的差。

slice方法可以实现拷贝一个数组，并返回一个新数组。

splice方法可以实现删除、替换、插入，例如splice(2,6)意思是删除从索引2开始的6个元素，splice(4,0,XXX,YYY,AAA)意思是从索引为4开始，插入三个元素，splice(2,1，XXX,YYY)意思是从索引为2开始删除一个元素，然后插入2个元素，splice方法会返回删除的项。

every方法，所有元素都满足某个条件时返回true，否则返回false。

some方法，有某个元素满足条件时则返回true，否则返回false。

filter方法，筛选出满足某个条件的元素，返回由这些元素组成的数组。

map方法，对元素进行某个操作后，返回新数组。

forEach方法，循环迭代，直接对原数组进行操作，没返回值。

encodeURI不会对本身属于URI的特殊字符进行编码，而encodeURIComponent会对整个URI的所有特殊字符进行编码。

利用Math.max.apply(Math，某数组)，这样可以找出数组中的最大值

## 六、面向对象程序设计

## 七、函数表达式
函数定义的方式有两种，分别是函数声明，函数表达式，JS在解析的时候，首先会将所有的函数声明提升，所以函数声明可以在定义之前去使用，而函数表达式不会被提升，在定义之前去使用会报错。函数声明后不能跟圆括号，会报错，函数表达式则可以。

闭包可以认为是在A函数中定义了B函数，然后在外部使用B函数，那么就会形成闭包，闭包不会被JS垃圾回收。

作用域链(scope chain)是一个指针列表，包含着指向各个执行环境的指针。所以函数闭包会创建并维护自己的作用域链，而这个也就是导致闭包不能被回收的原因。

我们可以利用函数的执行环境的特点来模拟块级作用域，因为一般来说外部的变量无法访问函数内部的变量。

可以利用闭包在对象中创建私有变量，实现对内部方法的访问，进行一些逻辑的封装。

## 八、BOM
