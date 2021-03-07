1、关于堆内存和栈内存

> 堆内存：存储的都是引用数据类型， 对象数据类型：在堆内存中存储的是 属性名和属性值 函数数据类型：在堆内存中存储的是字符串
> 栈内存：为 JS 执行提供环境包含全局作用域 window 和私有作用域 1.提供了 JS 代码执行的环境 2.基本数据类型都是放在栈内存中
> 2、对象定义三阶段 1.在堆内存开辟空间地址 2.把对象属性和值存放在这个空间里 3.把空间地址赋值给对象名

3、函数 分为哪几种？分别是什么样的形式出现的？ 1.有名函数 2.匿名函数 1.函数表达式 function(){} 2.自执行函数 函数自己调用自己 (function(){})() || ~function(){})() (),~,+,-,! ; 1.!function(){}() 2.~function(){}() 3.+function(){}() 4.-function(){}() 5.(function(){})()
4、节点
| nodeType | nodeValue | nodeName |
|----------|----------|---------|
| 文本节点 |TEXT| 3 | #text |
| 文本内容注释节点| 8 |#comment|
| 元素节点 | 1 |大写的标签名 |
| document | 9 |#document|

5、节点关系 parentNode 父节点；结构上的父级；childNodes 兼容所有浏览器，拿到的当前元素下所有的子节点 children previousSibling 上一个哥哥节点 previousElementSibling 上一个哥哥元素节点，但是不兼容 nextSibling 下一个弟弟节点 nextElementSibling 下一个弟弟元素节点，但是，不兼容 firstChild 第一个子节点 lastChild 最后一个子节点

6、元素的动态插入 2 个 1.插入到一个容器的末尾 //把当前元素插入到父容器的末尾； parent.appendChild(curEle); 2.把新元素插入到指定元素的前面； parent.insertBefore(curEle，oldEle);

7、元素的删除和替换 删除：parent.removeChild(要移除的元素); 替换：parent.replaceChild(curEle,oldEle);

8、 attribute 系列： obj.getAttribute(属性名) 获取元素身上的某个属性 obj.setAttribute(属性名) 设置元素的自定义属性； obj.removeAttribute(属性名) 移除元素身上的某个属性；

9、 关于.和 attribute 的区别： "1）如果已经在标签上设置了自定义属性，通过"".""不能获取到；通过 getAttribute 可以获取到自定义属性 2）通过"".""设置的自定义属性；在标签上看不到；但是通过 setAttribute 设置的自定义属性，可以看到注意事项："".""和 attribute 不能混合操作；"

10、 操作元素属性的方法有 3 个： . [] attribute 系列

11、 封装 getChildren 思路： getChildren 功能：获取当前元素所有的子元素参数：当前元素 curEle;返回值：获取的所有元素 ary;核心思想： 1）先获取当前元素所有的子节点 2）判断每个节点.nodeType===1;如果符合这个条件，把这个元素放入 ary 数组中；function getChildren(curEle){ var ary=[]; var aLis=curEle.childNodes; for(var i=0; i&lt;aLis.length; i++){ var cur=aLis[i]; if(cur.nodeType===1){ ary.push(cur) } } return ary;}

12、 封装 prev 的思路（上一个哥哥元素） prev:功能 获取当前元素的上一个哥哥元素节点参数：当前元素 curEle;返回值：找到的上一个哥哥元素 || null；核心思路： 先判断浏览器对 previousElementSibling 的支持情况；支持的话，直接用，不支持，自己再做兼容处理； 1. 先获取上一个哥哥节点（元素节点，文本节点，注释节点，document 节点） 2.当上个哥哥节点存在，并且，上一个哥哥节点不是元素节点的时候；会依据哥哥节点继续往上找；我们不知道要找多少次才能找到哥哥元素节点，所以用 while 循环；function prev(curEle){ if(curEle.previousElementSibling){ return curEle.previousElementSibling; } var pre=curEle.previousSibling; while(pre &amp;&amp; pre.nodeType !== 1){ pre=pre.previousSibling; }return pre;}

13、JS 的输出方法 1）alert（）2）confirm() 他有两个返回值：确定按钮-true； 取消按钮-false;3）document.write() 注意：在 window.onload 里使用 document.write 会清空页面；4）innerHTML5)console.log()6)console.dir();//可以打印出对象的详细信息；7)console.table();

14、 属性和方法的区别： 属性没括号，方法有括号；()

15、 数据类型检测 "1.typeof 1.不能判断具体对象的信息 2.instanceof 1.只要在原型链上都是 true 不能细分该对象到底属于哪个类 2.不能检测 null, undefined 3.字面量方法创建基本数据类型 不能检测 3.constructor 1.在原型链继承的时候若没有设置 prototype 上的 constructor 指向所属类的话， 只能找到最近的类 并不一定找到自己所属的类 2.不能检测 null undefined 3.给 prototype 赋值一个对象的话 ，constructor 会出问题 4.Object.prototype.toString.call() 可以检测所有数据类型 1.把 toString 方法中的 this 这个实例所属类详细信息打印出来 ""[object Object]"" 1.object 一个对象 2.Object 具体属于的类 首字母大写"

16、JS 下面的类 String Number Array Object Date RegExp......

17、 isNaN() 是否为非有效数： 是非有效数字-true； 不是非有效数字-false；

18、 1）Number 基本数据类型的转换方式 2)转换规律： "严格转换:Number()非严格转换：parseInt(); parseFloat();2)转换规律： 1.true-&gt;1; false-&gt;0; 2.null-&gt;0; undefined-&gt;NaN; 3.[] 首先会通过 tostring 转为"""",然后通过 Number 转成 0；3）isNaN();是否为非有效数字"

19、1）什么是真？什么是假？ "规律：除了 0,"""",null,undefined,NaN 为假，其他都为真"

20、 其他数据类型转为布尔数据类型的方式 1.Boolean(); 2.! 3.!! 4.if(值) 5.if(表达式)
21、 数字常用的方法 toFixed(保留的小数的个数)
22、 关于循环 for 和 while 的区别和联系 1）相同点，都可以包含四部：定义，条件，语句，自增 2）不同点：用法不同 for 循环用于长度固定的循环；while 循环，用于长度不固定；即，当不知道要循环多少次的时候，用 while 循环；3）do...while 循环，无论条件是否成立，都会先执行一次，以后再根据条件判断，决定是否再执行 4）for ...in 关于对象的循环；
23、 数据类型的比较 1.对象==对象 比较的是地址；[]==[]; -&gt;false2.对象==字符串 转成字符串 ''==[];-&gt;true3.对象==数字 转成数字 []==0; -&gt;true4.对象==布尔值 转成数字 []==![] -&gt;true;5.字符串==数字 转成数字 ''==0 -&gt;true;6.字符串==布尔 转成数字 ''==![] -&gt;true;7.数字==布尔 转成数字 0==[] -&gt;true;8.null==undefined -&gt;truenull===undefined -&gt;false;9.NaN==NaN -&gt;false

24、Math 9 个 1.Math.round() 四舍五入 2.Math.floor() 向下取整 3.Math.ceil 向上取整 4.Math.abs() 取绝对值 5.Math.pow() 幂 6.Math.sqrt() 开平方 7.Math.max() 求最大值 8.Math.min() 求最小值 9.Math.random() 0-1 之间的随机小数 //求 n-m 之间的随机整数，包含 n 和 m; Math.round(Math.random()\_(m-n)+n); //备注，一定要写会 0-61 之间不重复的随机整数： for 循环， while 循环

25、 Array 方法 pop 删除数组最后一项 push 添加数组最后一项 unshift 添加数组第一项 shift 删除数组第一项 splice 有三种用法 splice(n,m) 删除： 从索引 n 开始，删除 m 个 返回值：被删除的内容以一个新数组的形式返回； splice(n,0,x) 添加： 从索引 n 开始，删除 0 个，把 x 的新内容添加到索引 n 的前面； 返回值：一个空数组 splice(n,m,x) 替换： 从索引 n 开始，删除 m 个，替换为 x 的新内容； 返回值：被删除的内容以一个新数组的形式返回；indexOf() :查找数组中的内容，如果找到，返回对应内容的索引；找不到，返回-1；

26、获取元素的方式 1）id2)tagName3)className4)name--主要用于表单元素的获取 5）document.documentElementdocument.body//可视区的宽 document.documentElement.clientWidth||document.body.clientWidth;document.documentElement.clientHeight||document.body.clientHeight;//以下两个主要用于移动端 6)querySelector 获取到的是一个元素 #div .div;7)querySelectorAll 获取的是一组元素

27、插入排序 1）先给左手存一张牌（此牌放在数组中）2）拿数组中的每张牌跟左手数组中的每张牌进行比较（从后往前的比较）： 1.如果比左手大，放在左手下张牌的前面 2.如果比左手小，继续往左比较，一直比较到左手的第一张，还小的话，直接插入 left 数组的最开始；

28、数组常用的方法 1）增加，删除和替换 5 个 1.ary.push() 功能：给数组末尾添加一项 参数:要添加的新内容 返回值：新数组的长度 原数组发生改变; 2.ary.pop() 功能：删除数组最后一项 参数：没有参数； 返回值：被删除的内容 原数组发生改变; 3.ary.unshift(); 功能：给数组开头增加一项； 参数：要添加的新内容； 返回值：新数组的长度 原数组发生改变; 4.ary.shift() 功能：删除数组第一项； 参数：没有参数； 返回值：被删除的内容 原数组发生改变; 5.splice splice(n,m)删除： 从索引 n 开始，删除 m 个； 返回值：被删除的内容以新数组的形式返回； 原数组发生改变; splice(n,0,x)添加 从索引 n 开始，删除 0；把新内容 x 放在索引 n 的前面； 返回值：[]; 原数组发生改变; splice(n,m,x)替换 从索引 n 开始，删除 m 个，替换为 x 的新内容； 返回值：被删除的内容以新数组的形式返回； 原数组发生改变;2）查找和克隆 2 个 slice(n,m) 查找 从索引 n 开始，查找到索引 m，但不包含 m； 返回值：找到的内容 原数组不改变； //需求：找到[n 项-m 项] slice(n-1,m) concat 数组拼接 返回值：拼接后的数组 原数组不改变； 数组克隆： ary.concat() 不传参数 slice(0)/slice();3）数组转字符串 2 个 toString()-》把数组转为字符串（把数组每一项以“,”拼接成的字符串） 不传参数 返回值：以“,”拼接成的字符串； 原数组不发生改变； join('拼接形式')-&gt;把数组以各种形式拼接起来；拼接形式，就是我们传的参数； 返回值：拼接好的字符串； 原数组不发生改变； eval(str):把字符串做为 JS 代码来执行；字符串中如果有+,-,\_,/他们就具有计算的功能； eval(ary.join('+'))4)数组的排序和排列 2 个 reverse() 数组翻转 没有参数 返回值：翻转后的数组 原数组发生改变； sort(function(a,b){ return a-b;//实现从小到大排； //return b-a;//实现从大到小排 }) 参数：是一个函数，并且，函数中也有两个参数； 返回值：排序后的数组 原数组发生改变；5）数组常用但不兼容的方法；3 个； indexOf() 查找数组中是否有某一项，找到：返回索引；找不到：-1； //item：数组中的每一项 index：索引 input：原数组 forEach(function(item,index,input){ }) forEach 功能：遍历数组； 返回值：没有返回值； 原数组没发生改变； map(function(item,index,input){ }) map 的功能，及参数和 forEach 一样； 但是，map 有返回值；

29、快速排序 1）先找到中间位置 2）通过中间位置，获取中间值 3）拿数组中的每一项跟中间值进行比较，比他大放右边数组，比他小，放左边数组 4）return quickSort(left).concat([numValue],quickSort(right));注意：一定要写上什么情况，停止拆分；当数组.length&lt;=1;直接返回数组

30、 冒泡排序 思路：1.进行 arr.length 论排序 2.每轮都是前一个和后一个进行比较，若是比后面的大就换位置，每轮进行的比较次数随着轮数改变，arr.length-1-i;因为每比一轮都会把最大值放在最后面，所以再下一轮比较时候就不需要比较这个最大的了。function bubbleSort(arr) { for (var i = 0; i &lt; arr.length; i++) { for (var j = 0; j &lt; arr.length - 1 - i; j++) { if (arr[j] &gt; arr[j + 1]) { var temp = arr[j + 1]; arr[j + 1] = arr[j]; arr[j] = temp; } } } return arr; }

31、 任意数求和 //任意数求和 function add() { var total = 0; for (var i = 0; i &lt; arguments.length; i++) { if (!isNaN(arguments[i])) {//判断是否是有效数字 console.log(arguments[i]); total += Number(arguments[i]);//避免字符串的拼接 } } return total; }

32、 根据索引找对应字符： 2 个 charAt(索引) 通过索引找对应字符 charCodeAt(索引) 通过索引找对应字符的 ASCII 值；

33、 根据字符找对应索引 2 个 indexOf(字符串) 从前往后找：通过字符找对应索引； 找不到返回-1; lastIndexOf(字符串) 从后往前找： 通过字符找对应索引； 找不到返回-1;

34、 查找字符串 3 个 substr(n,m) 从索引 n 开始，查找 m 个； substring(n,m) 从索引 n 开始，找到索引 m，但不包含 m； slice(n,m) 他的功能跟 substring 一样；但是他可以取负值；
35、 字符串转大小写 2 个 toUpperCase() 转大写 toLowerCase() 转小写
36、 可以跟正则配合的字符串方法 4 个 1.split(‘切割形式’)字符串转数组 2.replace('内容','') 字符串替换 3.match(‘’) 捕获的功能； 4.search() 匹配的功能：通过字符找对应内容的索引； 找不到返回-1;

37、日期对象 var oDate=new Date();//获取日期对象 var y=oDate.getFullYear();//获取年份 var m=oDate.getMonth()+1;//获取月份的时候，必须+1； var d=oDate.getDate();//获取日 var w=oDate.getDay();//获取星期 0123456 0：代表星期日； var h=oDate.getHours();//获取小时 var min=oDate.getMinutes();//获取分钟 var s=oDate.getSeconds();//获取秒

38、定时器 //setInterval 有两个参数：1）回调函数 2）毫秒数 //setInterval：每隔一段时间走一次；只要不关闭页面或关闭定时器，他会一直走下去； //手动关闭：clearInterval()//setTimeout：一段时间后只走一次； // clearTimeout(定时器的名字)

39、JS 引入方式： "1.行内引入：写在标签内部 安全性低，可以在浏览器中更改内容 2.内嵌式： 写到 script 标签里面 3.外链式：通过 script 标签 src 引入路径 在此 script 中不可以写 JS 代码 不会执行 4.导入式：document.write(""&lt;script src=""""&gt;&lt;script/&gt;"")"

40、 JS 组成 1.ECMA script(5) 规定了ＪＳ中最核心的 数据类型 变量 基本语法 操作语句 2.DOM 3.BOM
41、 JS 命名规范 1.区分大小写 2.遵循驼峰命名法 3.由数字字母\_ $ 组成 数字不可以开头 一般情况 $ 这个开头是 jquery 对象 不可以使用关键字和保留字

42、 变量： 存储值和代表值的
43、 数据类型 "1 基本数据类型 1.数字(number) Number("""")&gt;&gt;&gt;&gt; 0 Number(undefined) &gt;&gt;&gt;&gt;NaN Number(null)&gt;&gt;&gt;0 1.正数 2.负数 3.0 4.小数 5.NaN isNaN() 判断时候先把字符串转换成数字（Number()），在进行判断 若不是一个数字的话 就返回 NaN 强制转换 Number() 软转换 parseInt() parseFloat() 2.字符串 3.Boolean 1.true and false 2.! 取反 eg:!3 &gt;&gt;&gt;&gt;&gt;先给 3 转换成 boolean 值（Boolean()）然后再取反 !! 取反再取反 3.Boolean(); 1."""" 2.null 3.undefined 4. 0 5.NaN &gt;&gt;&gt;&gt;&gt;&gt;只有这 5 个是 false 4.null 5.undefined 2.引用数据类型 1. 对象数据类型 1）var obj={}; 字面量创建方式 2）var o=new Object();实例创建方式 1.数组 [] 2.正则// 3.对象{} 4.Date 5.Math 2.函数数据类型 1.var fn=function(){};"

44、 不同数据类型的比较 "1.对象==对象 》》》》false {}=={}&gt;&gt;&gt;&gt;false []==[] &gt;&gt;&gt;&gt;false 2.对象==字符串 先将对象转化成字符串 然后再比较 [].toString()&gt;&gt;&gt;&gt;"""" 3.对象==Boolean 对象转化成字符串再转化成数字 再比较 4.对象==数字 对象转成字符串再转成数字 再比较 5.Boolean==字符串 都转成数字在比较 6.Boolean==数字 都转成数字在比较 7.数字==字符串 都转成数字在比较 8.null==undefined &gt;&gt;&gt; true undefined==undefined》》true null==null &gt;&gt;&gt;true 9.null or undefined 和其他任何数据类型比较 永远不相等"

45、对象 类 实例 区别 1.万物皆对象 2.类是对象的具体的细分 3.类中具体实例

46、 基本数据类型和引用数据类型的区别： 1.基本数据类型操作的是值 2.引用数据类型操作的是引用

47、 闭包： 函数在执行的时候，会形成一个私有的作用域，这个私有的作用域不会被外界的代码所干扰。所以我们把函数执行的这种机制叫做闭包。闭包就是一种机制。

48、 事件流 1.冒泡事件 哪一个元素触发事件 然后其父元素也会触发 再往上面传递 （从低往上的） * 2.捕获型事件 IE 只支持冒泡事件 而支持标准 DOM 的 chrome 和 FF 是两者都支持的(从上到下的)
box-shadow 1.重叠性 例如：box-shadow:1px 1px 1px #ffffdd,0px 0px #ffffdd,2px 2px 2px #fdffdd *2.本质是就是自身的复制 我们可以创建 1px\*1px 的元素 然后去绘制任意图形（理论上，任意的图片，box-shadow 都可以呈现。）

49、/\*javascript 的方法分为三类： 1.类方法 2.对象方法 3.原型方法

50、函数接受参数的两种方式 1.参数确定； 用形参接收 2.参数不确定： 用 arguments 接收

51、instanceof 不能检测什么样的变量 基本数据类型字面量创建的变量 不能用 instanceof 去检测 实例创建的可以

52、删除数组最后一项： ary.pop() ary.length--; ary.length-=1; ary.length=ary.length-1; ary.splice(ary.length-1,1);

53、给数组末尾添加一项 ary.push(); ary.splice(ary.length,0,''); ary[ary.length]=''; 3)数组的克隆 slice()/slice(0) ary.concat() ary.splice(0)

54、如何配置 git "git config --global user.name ""github Name""git config --global user.email ""github email"""

55、把本地文件夹变成 git 仓库 1.建立一个新的文件夹，点击进入（建立本地仓库 ） 2.通过 gitBash 或者是按住 shift 点击鼠标右键打开命令行。或者先打开 cmd .cd 把文件拖拽到此 打开 3.通过 git init，把此文件夹初始化成一个 git 仓库。

56、检查 git 安装成功 git --version

57、git 工作流 "1.git add .或者-A 或者具体名称 保存到暂存区 2.git commit -m""注释"" 保存到历史区 3.git push origin master 把历史区的内容推送到远程仓库的 master 分支上"
创建远程仓库及建立和远程仓库的链接和删除链接 1.new repository 创建一个新的远程仓库 2.复制仓库地址 3.进入命令行 git remote add origin（名字） 地址 4.查看是否连接 git remote -v 5.删除远程仓库 git remote rm origin
如何获取以及更新别人的项目 "1.fork 别人的项目 2.clone 别人项目到本地 git clone “fork 到自己的 github 的项目的地址” 目的就是拷贝到本地 3.建立和别人仓库的远程链接 git remote add teacher ""别人的地址"""
当别人的仓库有更新时候 "建立和别人仓库的远程链接 git remote add teacher ""别人的地址"" 1.更新远程地址 git remote update ""teacher"" 2.把更新的内容拉到本地仓库 git pull ""teacher"" master"
推送本地仓库内容推送给项目（别人的仓库） "1.把自己的内容 push 到自己的远程仓库 建立和自己的远程的 fork 过来的仓库的的链接 git remote add origin ""地址"" 1.git add . 2.git commit -m"""" 3.git push origin master 2.登陆到自己的 github,点击对应从别人 fork 过来的的仓库 ，点击 pull request ,进行合并请求。"
.什么是预解释？ 在当前作用域下，在 JS 代码执行之前，浏览器会对带 var 和带 function 进行提前声明或定义；

58、作用域分为： 全局作用域 和 私有作用域
全局作用域 当浏览器打开 HTML 页面的时候，会形成一个供 JS 代码执行的全局作用域(全局环境)，在这个全局作用域下，所有的全局变量，都属于 window 的全局属性；所有的全局函数，都属于 window 的全局方法；

59、声明和定义 声明：告诉浏览器，有这么一个变量； 举例： var a;定义：给已经声明过的变量赋值； eg: var a=123;

60、关于带 var 和 带 function 在声明阶段是不同的； 带 var 的： 只声明，不定义；带 function 的： 声明+定义；

61、函数定义和执行阶段：
定义阶段：
1）开辟一个空间地址 2）把函数体中的所有 JS 代码做为字符串存在这个空间中 3）把空间地址赋值给函数名调用
执行阶段：
1）形成一个私有作用域 2）给形参赋值 3）预解释 4）代码从上到下的执行；
作用域链： 当函数执行的时候，会形成一个私有作用域；查看这个作用域中是否有私有变量 A：1）如果有，这个作用域中所有出现的 A 都属于私有变量，跟外界没有任何关系；2）如果没有： 1.获取阶段： 往上级作用域进行查找，找到直接弹出，找不到，继续往上级的上级找，。。。一直找到 window 还没有找到，报错； xx is not defined; 2.设置阶段；往上级作用域进行查找，找到进行重新赋值，找不到，继续往上级的上级找，。。。一直找到 window 还没有找到，属于 window 的全局属性；

62、私有变量有两个 1）形参 2）带 var 的；

63、内存： 栈内存，堆内存

64、内存释放： 全局作用域释放：只有我们关闭浏览器打开的 HTML 页面，才能释放；私有作用域释放：一般情况，当我们执行完函数的时候，他会自动释放；但特殊情况除外：1）如果函数里面的东西被外面占用，就无法释放；2)不立即释放：当函数执行完成的时候会返回一个函数，这个返回的函数还需要再执行一次；只有返回值执行完成后才能释放；

65、堆内存： 对象数据类型：存的是对象的属性名和属性值 函数数据类型：存的是代码字符串；

66、堆内存的释放 如果堆内存被变量占用，无法得到释放，只有把变量的指针指向一个空指针 null，才会被释放

67、垃圾回收机制； 当浏览器空闲的时候，会把指向空指针的变量自动收回；浏览器 的这种处理机制，叫做垃圾回收机制；

68、带 var 和不带 var 的区别： 带 var：1）会进行预解释 2）window 的全局属性（在全局环境下）不带 var：1）不会进行预解释 2）window 的全局属性

69、预解释无节操：5 1）只对等号左边带 var 的，进行只声明，不定义；2）自执行函数不进行预解释，只有执行到他的时候，声明+定义+执行同步完成 3）条件判断语句中，无论条件是否成立，都会进行预解释；注意：为了代码规范性，不要在条件判断语句中写函数定义阶段；因为预解释时各大浏览器不同；4）已经声明过的变量，不会进行重复声明 5）return 后面的返回值不会进行预解释，return 下面的语句虽然不执行，但会进行预解释；

70、关于 this 的用法总结（6ge） 1）当元素的事件被触发，执行一个函数，函数中的 this 指向当前这个元素 2）当函数被调用的时候，看前面是否有点，点前面是谁，this 就是谁；3) 自执行函数中的 this，永远都是 window；4）在构造函数的中的 this 指向的就是当前实例 5）在回调函数中的 this 一般是指的是 window6）在函数调用时使用 call bind apply ,他们的第一个参数是改变 this 指向的，所以以上规则不适用

71、什么是上级作用域？ 上级作用域跟在哪里调用无关，只跟他对应的堆内存在哪里开辟（定义）有关；

72、闭包的作用： 1.避免变量名冲突 : 1)在闭包中重新定义变量 2）给形参赋值； _ 2.在闭包中影响全局：1)在闭包中不定义跟全局变量一样的变量名 2）用自执行函数中的 this/直接用 window； _ 3.封装 1.对象由两部分构成： 属性 和 方法；

73、面向对象和面向过程的区别？ 面向对象，主要会使用已经封好的方法；面向过程，需要考虑整个封装的细节；
面向对象的特点： 1）封装：对于一样的功能，我们只需要封装一次，以后再使用，直接调用即可：复用；专业术语：低耦合，高内聚；2）继承：子类继承父类中的属性和方法；3）多态：包含重载和重写：重载：JS 中不存在严格意义上的重载；但有类似重载的功能，就是给同一个方法，传不同的参数，可以实现不同的功能；重写：子类可以重写父类的属性和方法；

74、单例模式以及单例模式的本质 单例模式：就是把描述同一事物的属性和方法，放在同一个命名空间下；这样就避免了变量名冲突的问题；单例模式的本质：普通对象；

75、单例模式的优缺点总结 1.避免全局变量名冲突的问题 2.可以进行模块化开发： 1）模块之间的相互调用：模块名.属性名 2）本模块内个方法的相互调用：this.属性名/方法名；缺点：当对象的属性名和属性值相同的时候，会造成大量冗余代码；

76、工厂模式； 为了避免相同的功能，返回的重写；我们可以进行相同功能代码的封装

77、工厂模式 3 步骤： 1) var obj={};2） obj.xxx=xxx;3） return obj;
工厂模式的本质 封装；
工厂模式和构造函数模式的区别： 1）在调用阶段: 1.工厂模式调用时首字母小写；但是构造函数模式，首字母大写 2.构造函数调用时有 new；而工厂模式没有 new; 注意： 1）构造函数 new 出来的都是实例；实例都是对象数据类型； 2）构造函数都是类，类都是函数数据类型；2）在定义阶段： 工厂模式定义阶段有 3 步骤：1）自己创建对象 2）加工对象 3）自己返回对象； 构造函数模式定义阶段只有 1 个步骤：加工对象； 因为系统会自动帮我们创建对象和返回已经加工好的对象；
关于构造函数的总结(6) 1）构造函数中存的都是私有的属性和方法 2）构造函数中的 this 指向当前 new 出来的实例；3）构造函数中不需要手动返回对象，如果自己写了返回值： 1：返回基本数据类型，我们的实例仍然具有给他绑定属性和方法，不会发生任何影响； 2：返回引用数据类型，会覆盖掉系统返回的对象；那我们创建的实例，就不具有他的属性和方法了；4）构造函数主要是类和实例打交道；5）在创建实例的时候，如果没有参数，小括号可以省略；6）构造函数中，实例只跟 this.xxx 有关，跟变量没有任何关系；

78、关于原型模式的基础知识：（3 句话）重中之重） 1）每个函数数据类型（构造函数，普通函数）上，都天生自带一个属性，叫做 prototype，prototype 是一个对象；2）prototype 这个对象上，天生自带一个属性，叫做 constructor，他指向当前这个类；3）每个对象数据类型（实例，prototype，普通对象），都自带一个属性叫做\_\_proto\_\_，他指向当前实例所属类的原型；

79、函数中存储什么方法和属性，原型中存储什么方法和属性 函数中存储的是私有属性和方法原型上面存储的是共有的属性和方法

80、如何判断属性名属于对象，如何判断属性是否属于对象的私有属性，如何判断属性是否属于对象的公有属性 in 来判断是否为对象的属性 hasOwnProperty(）来判断是否为对象的私有属性 function hasPublicProperty(obj,attr){ return (attr in obj)&amp;&amp;(!obj.hasOwnProperty(attr);}
关于 Object.prototype 上的一些公有方法： hasOwnProperty():判断属性是否为对象的私有属性 返回值：boolean；obj1.isPrototypeOf(obj2):判断 obj1 是否在 obj2 的原型链上；propertyIsEnumerable():判断是否为可枚举的属性

81、原型链：如果查找 obj.属性名， 1）先在自己的私有空间中进行查找，如果找到，说明这个属性是对象私有属性；2）如果找不到，通过**proto**，去它所属类的原型上找，找到的话，属于公有属性；3）如果找不到，继续通过**proto**一层层往上找，一直找到 Object.prototype 还没有的话是 undefined;注意：如果找的是方法的话，最终找不到，会报错；
一提到构造函数就该想到 2 点 1：构造函数中都是私有的属性和方法 2：构造函数就是 实例和类打交道
一提到构造函数原型模式想到 2 点 1.原型上放的都是公有的属性和方法 2.原型模式是： 实例，类，原型三个打交道；
一提到 **proto**， 就是指原型链；对象找他的属性和方法都是通过**proto**一级级查找的
一旦我们更改了类.prototype 的指向 直接给他赋值一个我们自己定义的对象，那么他的 constructor 就是指向了 Object 这个类；所以，只要见到 Fn.prototype={};一定要注意他的 constructor；
基类什么，通过什么能最终找到它 Object 是所有对象数据类型的基类：任何一个对象，通过**proto**最终都能找到这个基类 Object;

82、批量操作公有属性？有什么需要注意的？ 用{}的时候，一定要注意两点： 1.constructor 会有问题，我们一定要重写 constructor 的指向； 2.不能批量删除系统内置类的公有方法；（但可以一个个的删除）

83、关于 call 方法 call 是用来改变函数中的 this 指向的；call()中第一个参数：用来改变 this 指向 call()中从第二个参数开始，相当于给 call 点前面的函数，从左往右一个个的传参；

84、面向对象的继承：

    1. 原型链继承// 继承父类的私有+公有的属性和方法到自己公有的，通过**proto**建立子类和父类之间的联系，方法:子类的 prototype 指向父类的实例 修改子类的 prototype 中的 constructor 指向子类
    2. call 继承 ：继承父类私有的属性和方法继承到自己私有的，方法：在子类构造函数中用 call 调用父类构造函数,F.call(this) call() ：改变 this 指向 call() 第一个参数 指的是用来改变 this 指向的 call() 后面的参数就是函数参数
    3. 冒充继承: 把父类公有的和私有的都继承到子类私有的 方法：在子类的构造函数中把父类的实例克隆一份相同的给子类中的 this(子类实例)
    4. 混合继承 1 call 继承 +原型链继承 问题：父类私有的即在子类私有的也在子类公有的
    5. 混合继承 2 call 继承+ 拷贝继承(把父类公有的方法和属性复制到子类的 prototype 上) function extend(obj1, obj2) { for (var attr in obj2) { obj1[attr] = obj2[attr]; } return obj1; }
    6. 寄生式组合继承 call 继承+ Object.create 思想创建一个空函数来继承父类的公有属性和方法（利用了一个空函数做过度，空函数中没有私有的 空函数的 prototype 指向父类的 prototype,在把子类的 prototype 指向空函数的实例，然后再设置子类的 prototype.constructor=子类）

Object.prototype 上的公有方法： hasOwnProperty：判断是否为私有属性 obj.isPrototypeOf(obj2) obj 是否在 obj2 的原型链上；propertyIsEnumerable：是否可枚举，只能枚举实例上自定义的属性和方法；（配合 for in 循环）
重写 子类实例通过.**proto**.\*\*proto\*\*更改属性或者方法，导致父类的变化 ，这就是 JS 重写或者同 prototype 更改
隐式数据类型转换 - \_ / % ==
回调函数 就是把函数表达式作为一个值，传给另一个函数的参数；

85、封装 forEach 兼容低版本 //forEach 有几个参数：2 个参数 1）callback 2）用来改变 this 指向的；Array.prototype.myForEach=function(callback,context){ //this-&gt;就是实例； context=context||window;//如果第二个参数不穿，默认是 window； if('forEach' in Array.prototype){//标准浏览器兼容处理； this.forEach(callback,context); return;//阻断程序执行的作用； } //低级浏览器的兼容处理； for(var i=0; i&lt;this.length; i++){//看回调函数被调用多少次； callback.call(context,this[i],i,this);//回调函数传参和改变 this 指向； } };

86、封装 map 兼容低版本 //思路： /\*map 有两个参数：1.回调函数 2.用来改变 this 指向；map 有返回值，返回值是个数组； _ 1.回调函数被调用的次数-就是数组的长度 _ 2.回调函数有 3 个参数：1.数组的内容 2.索引 3.原数组 _ 3.回调函数中的 this-window；call 改变 this 指向 _ 4.回调函数的返回值，会被数组保存 \_ 回调函数被调用多少次，数组中的长度就是多少个；Array.prototype.myMap=function(callback,context){ context=context||window; //先处理浏览器兼容问题 if('map' in Array.prototype){ return this.map(callback,context);//直接把 map 的返回值返回出去即可； //1.返回值 2.阻断程序执行； } var ary=[];//建立一个数组保存每个回调函数的返回值； for(var i=0; i&lt;this.length; i++){ var val=callback.call(context,this[i],i,this); ary.push(val); } return ary;//因为 map 有返回值，所以，最后我们返回一个数组； };

87、函数的三个角色 1.普通函数：会形成一个私有作用域-形参赋值-预解释-代码从上到下的执行；栈内存的释放； 2.构造函数：实例，类，原型 prototype，constructor：当前所属的类； **proto** 原型链； 3.普通对象：会具有普通对象的特征：属性和方法； 堆内存的释放；

88、Function 和 Object 的关系 Function 是 Object 这个基类的爹；Object.prototype 是 Function.prototype 的爹；

89、每个类都是 Function 这个类的实例；所有的实例，最终都能通过**proto**找到 Object 这个基类的原型；

90、call,apply,bind 以及在严格模式下和非严格模式下的解析 1.call 1）修改函数中的 this（当函数中没有关键字 this 的话就不修改） 2).调用了.前面的函数 this() 3. 为函数传递参数 是从左至右一个一个传递 但是第一个参数修改 this 的 2.apply 1）修改函数中的 this（当函数中没有关键字 this 的话就不修改） 2).调用了.前面的函数 this() 3. 为函数传递参数 一共连个参数 第一个参数修改 this 的，第二个函数是个数组，把 function 中的参数以数组的形式传入 call 和 apply 区别只有在传参的时候 其他都是一样的 包括严格模式 和非严格模式
非严格模式下的 call 和 apply fn.call() this---windowfn.call(undefined) this---windowfn.call(null) this---windowapply 和 call 一样
严格模式下 call 和 apply fn.call() this---undefinedfn.call(undefined) this---undefinedfn.call(null) this---nullapply 和 call 一样

91、构造函数没有参数在 new 的时候，什么情况下后面的（）不能省略 new Foo().getName()；他是什么执行的 "如果后面还有.方法的话就不能省略""（）""；例如：new Foo.getName();这时候就是先执行 Foo.getName() 再 new 实例这时候是先执行 new Foo()再调用 getName()，代码从左向右执行；"

92、Function.prototype 是什么？ 又是怎么操作的？ Function.prototype 名字为 anonymous 或者 empty 是个特殊的函数，但是操作是按着 prototype 来操作,看成对象去操作

93、求数组的最大值和最小值（4 种方法） "//1.排序思路获取最大值和最小 arr.sort(function (a, b) { return a - b; }); console.log(""最小值"" + arr[0]); console.log(""最大值"" + arr[arr.length - 1]); //2.利用 Math.max Math.min 和 eval 配合拼接成字符串 来实现求最大值和最小值 var strMax = ""Math.max("" + arr.toString() + "")""; var strMin = ""Math.min("" + arr.toString() + "")""; var max = eval(strMax); var min = eval(strMin); console.log(max); console.log(min); //3.利用 Math.max Math.min 和 apply 配合实现 var max = Math.max.apply(null, arr); var min = Math.min.apply(null, arr); console.log(max); console.log(min) //4.假设法求最大值和最小值 var max = arr[0], min = arr[0]; for (var i = 1; i &lt; arr.length; i++) { arr[i] &gt; max ? max = arr[i] : null; arr[i] &lt; min ? min = arr[i] : null; } console.log(max); console.log(min);"

94、字面量创建基本数据类型 //基本数据类型（字符串，数字，布尔）通过字面量方式创建的时候，如果使用属性和方法，他会找到对应的包装类型(String,Number,Boolean)的原型去使用公有的属性和方法; /\_ _ 1.'123'.charAt(0) _ 2.对应的包装类型，会把自己的属性和方法给了字面量创建的变量,让他去使用 \_ 3.然后包装类型迅速消失；

95、call apply bind 区别 1.call,apply 在 this 被改变后，函数会立即执行；2.bind 属于预处理机制:bind（）会提前修改后函数中的 this 和参数，然后返回个修改后的函数；等我们需要的时候，手动调用；bind 的传参方式，跟 call 一样；3.只有 apply 的第二个参数是一个数组；其他的都是从第二个参数开始一个个的传参；

96、封装类数组转数组 \*\* _ makeArray:把类数组转成数组 _ @param arg：类数组 _ @returns {Array} _/ makeArray:function(arg){ var ary=[]; try{ ary=Array.prototype.slice.call(arg); }catch(e){//IE 6-8 中元素集合，节点集合不支持借用数组 slice 方式转数组 for(var i=0; i&lt;arg.length; i++){ ary.push(arg[i]); } } return ary; },

97、把 JSON 格式的字符串转成 JSON 格式的数据 /\*\* _ jsonParse:把 JSON 格式的字符串转成 JSON 格式的数据 _ @param jsonStr \_/ jsonParse:function(jsonStr){ return 'JSON' in window?JSON.parse(jsonStr):eval('('+jsonStr+')') }

98、数组 sort 深入研究 1）找到每一项的数字进行排序 2）找到每一项的汉字进行排序 a.localeCompare(b);

99、DOM 映射？DOM 回流？DOM 重绘 DOM 映射//核心：html 页面结构跟获取的元素集合存在映射关系 1.页面结构发生变化的时候，元素集合也会跟着改变 2.当我们操作元素集合的时候，页面结构也会跟着改变

100、DOM 回流 当页面中的 HTML 结构发生变化时候（增加，删除，位置改变），浏览器都需要重新计算一遍最新的 DOM 结构，重新对当前页面进行渲染

101、DOM 重绘 某一个元素的部分样式发生改变，浏览器只需要重新当前元素即可

102、JSON 及其方法 "JSON 的属性名都有“”且不能省略，也不能换成''JSON 用来解析字符串(数据)的 JSON.parse(str) 把字符串转成 JSON 对象 JSON.stringifg(json) 把 JSON 对象转成字符串 IE 6-7 中的不存在 JSON 属性，所以可以使用 eval(""(""+str+"")"") 把字符转 JSON 对象"

103、数组取最大值和最小值（4 种方法） "//1.排序思路获取最大值和最小 arr.sort(function (a, b) { return a - b; }); console.log(""最小值"" + arr[0]); console.log(""最大值"" + arr[arr.length - 1]); //2.利用 Math.max Math.min 和 eval 配合拼接成字符串 来实现求最大值和最小值 var strMax = ""Math.max("" + arr.toString() + "")""; var strMin = ""Math.min("" + arr.toString() + "")""; var max = eval(strMax); var min = eval(strMin); console.log(max); console.log(min); //3.利用 Math.max Math.min 和 apply 配合实现 var max = Math.max.apply(null, arr); var min = Math.min.apply(null, arr); console.log(max); console.log(min) //4.假设法求最大值和最小值 var max = arr[0], min = arr[0]; for (var i = 1; i &lt; arr.length; i++) { arr[i] &gt; max ? max = arr[i] : null; arr[i] &lt; min ? min = arr[i] : null; } console.log(max); console.log(min);"
求多个数的平均值（去掉最大值和最小值） " function average() { var arr = Array.prototype.slice.call(arguments); arr.sort(function (a, b) { return a - b; }); arr.shift(); arr.length--; return (eval(arr.join(""+"")) / arr.length).toFixed(2); }"

104、浏览器异常捕获 try{}catch(e){throw new Error(e); //手动抛出错误 阻断代码的执行}finally{}

105、绑定数据三种方式 \*\*\_1.直接 DOM 操作 _ 多次回流 _ 2.fragment(文档碎片模式：) _ 回流一次 _ 3.字符串拼接 最常用在工作中 _ 优点： 1.简单 _ 2.性能高：只对页面进行一次的 DOM 操作；不会引发太多的回流 \_ 缺点：相当于把页面中所有内容都拿出来，重新进行字符串拼接，拼接成新的字符串再放进页面，原来内容的事件就不存在了。

106、页面表排序三步骤 1.类数组转数组 2.数组排序 3.将排序后的对象插入页面

107、表格排序思路 排序时候默认是从小到排序 1.获取元素并且解析数据 2.绑定数据 3.给表格添加隔行变色 4.给表格排序 排序默认是从小到大的顺序

108、什么是正则 正则用来操作（匹配和捕获）字符串的一系列规则；
正则创建的两种方式 ？两种创建方式的区别：？ 1）实例创建时，特殊含义的字符需要转义（\）；2）实例创建可以进行变量的拼接，但是字面量方式创建，不能拼接变量；
正则由两部分组成 正则由两部分组成：元字符 和 修饰符
元字符包含：代表特殊意义的元字符 和 代表次数的量词元字符 代表特殊意义的元字符： \ 转义字符 | 或 () 分组 . 除了\n 以外的其他字符 \n 换行（一般用在控制台的换行） \b 开头结尾和空格 ^ $ \d 数字 \w 数字字母下划线 \s 空格 \D 非数字 \W 非数字字母下划线 \S 非空格 [abc] abc 三个中的任何一个 [^abc] 除了 abc 这三个的任何一个； [a-z] 字母中的任何一个 [^a-z] 非字母 代表次数的量词元字符： \_ 0 到多 + 1 到多 ？ 0 次或 1 次； {n} 正好几次 {n,} 至少 n 次 {n,m} n 次到 m 次
[]的用法： 1）特殊含义的字符（比如：+ .等）不再具有特殊含义，就是普通的字符；2）中括号不会出现两位数
小括号的用法总结：3 1）提高优先级 var reg=/^(18|19)$/2）分组 经常配合 exec；exec 拿到的数组中能捕获到小分组；3）只匹配不捕获 (?:)
捕获的方式： 1）exec 返回值是一个数组 有三项（如果正则中有分组的话返回的数组中从第二项开始就是分组的内容，所以数组就不只是三项了，这时候能拿到正则的详细信息（第一个符合规则的字符，索引，原始字符串 ）如果没有 返回 null2）match:可以一次性把符合我们规则的内容，放在一个新数组返回；3）replace（//，function(参数和 exec 返回的一样){}）
正则捕获的特点： 1）懒惰性：解决办法-用全局 g; eg:每次都是从索引 0 开始查找； 用了全局 g，lastIndex 每次查找都是从找到内容的下一个元素的索引开始查找；2)贪婪性：解决办法-用?
lastIndex:代表开始查找位置的索引；影响 lastIndex 的东西有哪些： 1.exec 2.test
关于?的用法总结： 1）？ 0||1；可有可无的意思 2）用来解决正则捕获的贪婪性 量词元字符+？3)（?:） 只匹配不捕获；
exec 和 match 的区别 exec 能拿到小分组的详细信息；match 只能拿到符合大正则的内容，不能拿到小分组的详细信息；
重复子项： \1：跟第一个小分组一模一样； 小分组都是带小括号的 \2:跟第二个小分组一模一样；
获取地址栏中的=两边的内容的正则（传的参） /([^?=&amp;]+)=([^?=&amp;]+)/g

109、css 盒子模型 1.设定的宽高+2.padding+3.border+4.margin

110、JS 盒子模型： js 通过属性和方法获取元素的样式（行间的样式表的）
处理浏览器的兼容性问题 1)属性判断 1.'getComputedStyle' in window; 2.window.getComputedStyle 3.typeof getComputedStyle ==='function'2)try...catch(e)....try...catch:因为他只有报错，才能走 IE 浏览器；所以，无论是否支持，都会走 try；所以，相对来说，try...catch 性能不是太好；3）navigator.userAgent 检测浏览器版本的详细信息 1. var reg=/MSIE (6|7|8)\.0/; reg.test(navigator.userAgent) 2.var reg=/MSIE (6|7|8)\.0/; if(navigator.userAgent.search(reg) !==-1){//说明找到了，是 IE 浏览器 }else{//标准浏览器 }
JS 盒子模型遇到的 4 个问题 1）浏览器盒子模型的兼容性问题 -- 封装一个 win 方法：获取和设置浏览器的盒子模型 2）浏览器提供的属性和方法只能拿到复合值，不能拿到宽、高之类单个的值； -- 封装一个 getCss 方法 （获取非行间样式的方法） 3）通过浏览器属性拿到的值，只能拿到四舍五入的整数，不能拿到小数 --没办法解决； 4）offsetLeft 只能求出当前元素的外边框距离定位父级内边框的距离，无法求出到 body 的距离； --offset 封装
client 系列 （不受内容溢出的影响）1.clientHeight 设定的高 +padding 2.clientWidth 设定的宽 +padding 3.clientTop 边框 4.clientLeft 边框
offset 系列 （不受内容溢出的影响）1.offsetWidth clientWidth+border 2.offsetHeight clientHeight+border 3.offsetTop 当前元素的外边框到父级（定位父级）的内边框 4.offsetLeft 当前元素的外边框到父级（定位父级）的内边框 5.offsetParent 定位父级
scroll 系列 （受内容溢出的影响）1.scrollWidth 2.scrollHeight 3.scrollLeft 卷去的内容 4.scrollTop 卷去的内容在没有内容溢出的时候和 client(clientWidth 和 clientHeight)一样在有内容溢出的时候:scrollHeight 约等于：真实内容+上 padding 值约等于？： 1.在不同浏览器下取到的值不同 2.在同一浏览器下，有无设置 overFlow hidden ，取到的值不同
获取样式（行内和样式表）属性值 getComputedStyle(元素，null)[属性名] 获取样式（行内和样式表）但是不兼容，在 IE6-8 不兼容，但可以用 元素.currentStyle[属性名]做兼容处理
同步和异步 同步：当前的任务没完成，会不开始下一项任务；异步：当前任务（定时器没到，里面的代码不能执行）没完成，不会等待，继续开始下面的任务；下面的任务如果没做完，永远不会回过头来执行前面已经准备好的代码；只有后面的任务都完成，才会回头执行前面已经准备好的代码；JS 中用的最多的是同步，所以 JS 代码是从上到 下执行的；JS 中的循环都是同步；
JS 中的异步：4 个 1）元素身上的事件 2）定时器：第二个参数代表毫秒数，各大浏览器对定时器的执行时间都设置了最小毫秒数，比如 5ms； 定时器并不是时间设置越小，就越好，反而，时间越小越不准确；3）回调函数 4）ajax
结构父级和定位父级 结构父级上最大的标签是 html 元素 结构父级上的祖师爷-》document;定位父级上最大的是 body；
404 (Not Found)： 代表文件没找到；

111、任务队列池 每添加一个异步事件，都会跟任务池中的所有异步任务时间进行比较，若是比他小，，就放在前面，否则就放后面

112、跑马灯效果 1.先把原来的 ul 内的内容复制一遍，添加到 ul 中 ul.innerHTML+=ul.innerHTML2.然后动态向左移动 ul 的 left,等到 ul 整个元素的一半的时候，回到 0 就实现了跑马灯效果
多张图片的懒加载技术 "1.然包含图片的 div 设置背景图片 2.绑定 window.onscroll 事件，判断里面所有的 li（for 循环）位置来加载图片，也就是 win(""scrollTop"")+win(""clientHeight""）&gt;=li.offsetTop+li.offsetHeight 加载图片 3.加载图片需要做校验 1.新建一个 var temp= new Image; 2.temp.src=aImg[i].realSrc; 3.temp.onload=function(){ aImg[i].src=this.src; temp=null; L......................... } 4.temp.onerror=function(){ temp=null; .......... }"

113、回到顶部 1.为元素绑定点击事件，采用 定时器的方式动态的减少 win(scrollTop)的值，直到为小于或等于 0 的时候停止定时器;2. 在页面没有滑动过一屏幕时候隐藏按钮，滑过一屏幕，再显示，3.新要求：在回到顶部的过程中 鼠标滑动停止回顶,设置一个 bOk 为 false 表示定时器执行, 在定时器中设置为 false，在 window.onscroll 中 设置为 true,当人为的干预的时候就停止定时器（原理就是人为的滑动滚轮会更快速的触发 window.onscroll，所以在定时器没有执行下一次的时候，我们已经手动操作多次了，然后 bOk=true 停止定时器）注意：我们通常设置定时器的间隔大于 30 毫秒，因为各个浏览器都有设置最小的默认值

114、瀑布流 就是像瀑布一样，一直向下花鼠标一直有内容被加载进来 1.我们可以先手动的创建 50 个，然后判断滑轮是否快要滑倒 body 内容的总高度的时候就再加载 50 个来实现瀑布流。2，在创建 50 内容的时候我们会一个一个的创建，添加到内容最少的 ul 中，已达到错落有致的感觉 1.类数组转数组 2.排序 3.插入到最小的那个 ul 中

115、关于定时器的优化小技巧： 1）开启一个定时器前，先清除没有的定时器 2）我们最好把定时器放在元素的自定义属性上，避免全局变量的冲突；3）当匿名函数中的函数调用需要传参的时候，参数会把匿名函数当作跳板去上级作用域查找；这样，就会形成无数个不销毁的匿名函数；解决措施：使用\_move;4)定时器的边界值判断；

116、 链接： 1）如果 href 中不写或者写#,都是调到页面顶部 2）如果 href 中如果写了真正的链接地址，会打开对应的页面；3)如果 href 中写 ID，可以跳到对应的模块 4）如果不想让其跳转，可以直接写 javascript:(可以写代码，只是我们不写而已);javascript:; 或 javascript:void(0);两个都可以

117、原生转 jquery？ jquery 转原生？ 原生转 jquery： $(原生的元素)jquery转原生：$(ele).get(索引)； $(ele)[索引]

118、给 jquery 扩充插件有两种方法 1）给原型上扩充 $.fn.extend相当于 $.prototype.extend;我们就是给原型上扩充公有方法，能调用这些公有方法的就是实例；$('').tab();
给类上直接添加方法 $.extend({tab:funtion(){}})

119、jquery 页面加载的功能，他跟 window.onload 是有区别的： 1）window.onload 是等页面所有的内容（dom,视频，音频，图片等等）都加载完成，才开始执行 JS 代码；2）$(function(){代码}) 代表只加载完 DOM 结构就开始执行 JS 代码；
jQuery 取值赋值合体 同一个方法，既可以获取值，也可以设置值
jquery 没有 DOM 映射，当页面结构变化的时候，我们提前获取到的元素集合不会跟着发生变化；
jQuery 原型上的 each 方法?类上的 each 方法? //原型上的 each 方法，只能遍历 jquery 元素 //类上的 each 方法，不仅可以遍历 jquery 元素，也可以遍历数组，对象，类数组

120、关于 onmouseover 和 onmouseout 的问题(持续触发)：两种解决办法 utah 1）懒办法 ： onmouseenter; onmouseleave2) 让关联元素不执行代码； var oTo= e.fromElement||relatedTarget;//里面的关联元素 如是 onmouseout 的话用 var oTo= e.toElement||relatedTarget; if(this.contains(oTo)) return;

121、事件对象的兼容处理 e=e||window.event 在 iE6-8 中用 window.event
事件对象：描述事件类型的详细信息（7） 常用的 事件对象的兼容处理：e=e||window.event;1）在标准浏览器下，用的是形参 e;2)在 IE 浏览器下，跟是否传形参无关，用 window.event 获取事件对象；3.事件的详细信息；1)clientX/Y:当前鼠标落脚点，距离可视区左上角的坐标；--兼容 2)pageX/Y:当前鼠标落脚点，距离第一屏左上角的坐标；当浏览器被卷去的内容越多，pageY 就越大--他不兼容； 兼容处理： e.pageX=(document.documentElement.scrollLeft||document.body.scrollLeft)+ e.clientX; e.pageY=(document.documentElement.scrollTop||document.body.scrollTop)+ e.clientY;3)e.type:当前所触发的行为类型；--兼容 4)e.target:事件源--不兼容 兼容处理： e.target= e.target|| e.srcElement;5)e.keyCode6）阻止默认事件 e.preventDefault();--不兼容 兼容处理： e.preventDefault? e.preventDefault(): e.returnValue=false;7）阻止冒泡 e.stopPropagation? e.stopPropagation(): e.cancelBubble=true;

122、事件流：1）捕获阶段 --从外向里捕获 2）事件源 -- e.target 当前放生事件的这个元素 3）冒泡阶段 -- 从里向外的去触发元素身上相同的事件，当元素身上有绑定的方法的时候，被绑定的方法就会执行； 注意：只要元素的事件被触发，他所有父级的相同事件都被触发了，只是看他是否有绑定方法而已，如果过绑定方法，才会执行，没有，就不会执行了；

123、事件分为 DOM0 级事件和 DOM2 级事件区别 DOM0 级事件：1）DOM0 级事件，是元素的私有属性 DOM0 级事件绑定只能给当前元素的某一个事件绑定一次方法”2)只能发生在事件流的冒泡阶段 DOM2 级事件：也可以绑定元素的事件，只是不加 on;1)DOM2 级事件，在元素所属的 eventTarget 这个类的原型上；所以，它是公有属性；2)DOM2 级事件可以通过第三个参数，控制事件流在捕获阶段 还是 冒泡阶段；3）DOM2 级事件中，可以绑定 DOM0 级没有的行为：（自定义的行为，DOM2 级专有，DOM0 级没有的系统行为）;4）原理: 只要使用的是 DOM2 事件绑定,不管是标准浏览器还是 IE6~8,浏览器都会给当前操作的元素默认开辟一个事件池(一个存放方法的容器),紧接着浏览器会把绑定的所有方法依次存储到事件池中 5）DOM2 事件绑定可以给当前元素的某一个事件绑定多个不同的方法，当事件触发，浏览器会到默认创建的事件池中把之前存放的所有方法按照顺序依次的执行”

124、DOM2 级事件绑定在标准和非标准浏览器的 区别: 1.&gt;事件在 IE6~8 下需要在前面加 on -&gt;标准浏览器中通过控制最后一个参数是 false 还是 true,可以控制绑定的方法在冒泡还是捕获阶段执行(一般都用 false,代表在冒泡阶段执行)；在 IE6~8 下只能在冒泡阶段执行；2.&gt;THIS 问题: 标准浏览器中使用 DOM2 绑定的方法,在事件触发方法执行的时候,方法中的 THIS 都是当前的元素;但是在 IE6~8 下方法中的 THIS 是 window;3.重复问题: 标准浏览器在往事件池中存储方法的时候，天生自带去重的机制，也就是不能给同一个元素的某一个事件绑定多个相同的方法，但是 IE6~8 下没有这个去重的机制，是可以给同一个元素的某一个事件绑定多个相同方法的;4.&gt;执行的顺序问题: 标准浏览器绑定的时候，往事件池中存储的顺序和绑定的先后顺序一致，执行的时候也是按照绑定的顺序依次执行的；但是 IE6~8 下执行的时候顺序是混乱的，和绑定的顺序没啥关系

125、jQuery 中的 ready 方法的实现原理(采用的是 DOM2 事件绑定 &amp;&amp; 使用的是 DOMContentLoaded 事件) function domReady(fn) { if (document.addEventListener) { document.addEventListener('DOMContentLoaded', function () { fn &amp;&amp; fn(); }, false); } else { document.attachEvent('onreadystatechange', function () { if (this.readyState === 'complete') { fn &amp;&amp; fn(); } }) } 1.我把当前的 JS 写在 HEAD 中了,我还想获取到 BODY 中的元素进行操作,可以怎么做?2.JQ 中的 READY 和 WINDOW.ONLOAD 的区别? 1.使用 JQ 中的$(document).ready() 2.使用 window.onload 3.把 JS 放在外部文件中,通过 SCRIPT 引入,引入的时候设置属性：async、defer &lt;script src='xxx.js' async defer... JQ 中的 READY 和 WINDOW.ONLOAD 的区别? 1. WINDOW.ONLOAD 是只有等到页面中的 HTML 结构、图片、文字等所有资源都加载完成才会触发事件执行 2.JQ 中的 READY 是等页面中 DOM 结构加载完成之后就可以了，还可以在同一个页面中使用多次；WINDOW.ONLOAD 在同一个页面中只能使用一次(想使用多次的话用 DOM2 绑定) 所有的事件绑定都是异步编程,READY 也是一个 DOM2 的事件绑定,所以它也是异步编程的
jQuery 选择器类型 "(1)基本#id $('#div1')element $('div').class $('.bg')_ $('*')selector1,selector2,selectorN $(""div,.bg,#div1"")(2)层次选择器：ancestor descendant $(""#div1 a"") 后代查找 $('#div1').find('a')parent &gt; child    $(""#div1&gt;a"") 子代查找 $('#div1').children(""a"")                 同级筛选 $('div').filter('.bg') 首先获取所有的DIV,然后在集合中进行二次过滤,把拥有BG样式类名的过滤出来prev + next     $(""#div1+a"") 下一个弟弟Aprev ~ nexts     $(""#div1~a"") 所有弟弟中的A(3)基本过滤器选择器(二次筛选:在原来集合的基础上在进行过滤的):first:last:not:even:odd:eq:gt 大于某个索引:lt 小于某个索引:header:animated$('div:not(.bg):gt(2):lt(6)') -&gt;首先获取所有的 DIV,在所有的 DIV 中进行二次筛选获取没有 BG 样式的,在目前最新的集合基础上把索引大于 2 的获取到,然后再在现在最新的集合基础上把索引小于 6 的获取到(4)内容过滤器选择器:contains $(""a:contains('珠峰')"") 在所有的a中筛选出内容包含珠峰的a:empty:has:parent(5)可见性过滤器选择器:hidden:visible(6)属性过滤器选择器[attribute]  $(""a[id]"") 所有有ID属相的A[attribute=value][attribute!=value][attribute^=value][attribute$=value][attribute\*=value][attrsel1][attrSel2][attrseln](7)子元素过滤器选择器:nth-child $(""a:eq(0)"") $(""a:nth-child(1)""):first-child:last-child:only-child(8)表单选择器:input $(""input:text""):text:password:radio:checkbox:submit:image:reset:button:file:hidden(9)表单过滤器选择器:enabled:disabled:checked:selected"

126、事件绑定 on: 1)浏览器的兼容问题：标准-addEventListener2)IE 浏览器： 1.顺序问题-把所有的方法都保存在自己事件池中； 1）没有自己事件池创建一个 []; 2)有了自己事件池，先看是否重复； 3）没有重复才添加 2.把 run 方法绑定到系统事件池：存在两个问题 1）run 中的 this 问题--通过 call 解决； 2）run 的重复绑定问题；--把 ele.attachEvent()放在第一次创建自己事件池那里；//以上解决了 attachEvent 的三个问题：3.run 方法；--run 方法只会在 IE 浏览器下执行；1）处理 IE 浏览器 event 详细信息的兼容处理 2）把自己事件池中所有方法顺序调用；--核心
.off 方法 1）标准浏览器下，直接用 removeEventListener2)判断自己事件池中是否有你要解除的 fn 方法，如果有，让其=null;

127、1.H5 拖拽 2.事件的执行顺序 draggable:true 设置此属性之后才能拖拽拖拽元素事件：dragstart :拖拽触发之前 drag 拖拽前和拖拽之间 连续的触发 dragend 拖拽结束触发拖拽目标元素事件 dragenter 进入目标元素触发 dragover 进去目标离开目标之间连续触发 ：注意：可以在此事件中设置阻止默认事件 e.preventDefault(); 这时候就可以把拖拽元素放入目标元素中；设置这个之后就不会触发 dragleave 事件 ，会触发 drop 事件；dragleave 离开目标元素触发：drop 在目标元素上释放鼠标时候触发 drop 不触发的时候，触发 dragleave 事件 drop 触发的时候（dragover 中设置了阻止默认事件），就不触发 dragleave 事件
dataTransfer 对象 用来存放拖拽时候携带的数据 setData() getData(); effectAllowed:设置光标的样式;(none copy copyLink copyMove link linkMove move all uninitialized ) setDragImage:三个参数 1.指定的元素 2.X 坐标 3.Y 坐标

128、File API FileReader;读取文件信息；将文件读入内存，并且读取文件中的数据 readAsBinaryString 二进制字符串 readAsText 文本数据 readAsDataURL 数据读取为 DataURL readAsArrayBuffer 读取为 ArrayBuffer 对象（存储固定长度的二进制数据的缓存区）
File API 系列完整的事件模型 "onabort 中断  onerror 出错 <span class=""Apple-tab-span"" style=""white-space:pre""> </span>onloadstart 开始时触发 <span class=""Apple-tab-span"" style=""white-space:pre""> </span>onprogress 数据读取中 <span class=""Apple-tab-span"" style=""white-space:pre""> </span>onload 成功完成时触发 ，数据保存在 this.result 中 <span class=""Apple-tab-span"" style=""white-space:pre""> </span>onloadend 完成时触发，不管成功或失败"

129、6.base 64 base64 是一种使用 64 个可打印字符来表示二进制数据的一种编码方法 btoa() 二进制转化成 base64 atob() 将 base64 转化成二进制数

130、在移动端中, 定义了三种目前为止受到所有移动设备支持的事件：（ios 和 android 都是 webkit 内核） touchstart：手指按下时候触发 touchmove： 拖动页面元素时候触发 touchend：手指松开时候触发
触摸事件 每一个事件对象都拥有如下所示的一些属性： • touches:由所有用户手指在屏幕上的触碰点所构成的集合。 • targetTouches:在本次事件中目标绑定的触碰点的集合  • changedTouches:在本次事件中发生变动的触碰点的集合  注: 移开屏幕(touchend)的那个触摸点，只会包含在 changedTouches 列表中，而不会包含在 touches 和 targetTouches 列表中。
每一个触碰点都拥有如下所示的一些属性 • identifier:属性值为一个整数值,用于标识屏幕上的每一个触碰点。 • target:属性值为该触碰点所在元素。 • pageX 与 pageY:属性值为一个整数,分别表示触碰点在页面上的水平方向与垂直方向上的坐标点位置。 • screenX 与 screenY:属性值为一个整数,分别表示触碰点在屏幕上的水平方向与垂直方向上的坐标点位置。 • clientX 与 clientY:属性值为一个整数,分别表示触碰点在视口上的水平方向与垂直方向上的坐标点位置  • radiusX 与 radiusY:属性值为一个整数,分别表示一个接近于用户手指形状的椭圆在水平方向上的半径值与垂直方向上的半径值。
在移动端中,注意事项： "防止用户缩放 &lt;meta name=""viewport"" content=""width=device-width, initial-scale=1.0, user-scalable=no""&gt; 防止页面滚动 event.preventDefault(); 关于 touchend 事件 移开屏幕的那个触摸点，只会包含在 changedTouches 列表中，而不会包含在 touches 和 targetTouches 列表中。"
