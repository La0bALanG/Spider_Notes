# **<font face="楷体" size=6 color='blue'>Python爬虫笔记4:JavaScript逆向分析</font>**

<font face="楷体" color='blue'>作者：**Barranzi_**</font>
<font face="楷体" color='blue'>个人github主页：**[github]**(https://github.com/La0bALanG)</font>
<font face="楷体" color='blue'>个人邮箱：awc19930818@outlook.com</font>

<font face="楷体" color='blue'>**新时代的铁饭碗：一辈子不管走到哪里都有饭吃(还能吃上热乎的)。——佚名**</font>

<font face="楷体" size=5 color='red'>**免责声明**：</font>

<font face='楷体' color='red'>	**本系列笔记撰写初衷就是为了分享个人知识以及个人学习历程中的感悟及思考，所涉及到的内容<font size=5>`仅供学习与交流`</font>，请勿用作<font size=5>`非法或商业用途`</font>！由此引发的任何法律纠纷<font size=5>`后果自负`</font>，与作者本人无关！**</font>

<font face="楷体" size=5 color='red'>**版权声明**：</font>

<font face='楷体' color='red' size=5>	**未经作者本人授权，禁止转载！请尊重原创！**</font>

![timg](C:\Users\安伟超\Desktop\桌面文件\timg.jpg)

**<font face="楷体" color='blue'>注：本文所有代码、案例测试环境：1.Linux -- 系统版本：Ubuntu20.04 LTS   2.windows -- 系统版本：WIN10 64位家庭版</font>**

------

[TOC]

# 高级反爬机制——JavaScript逆向分析

## JavaScript反爬虫原理及原因

当前文我们所见过的绝大部分反爬机制都无效的时候，js反爬或许可能成为最后一根救命稻草。

前文我们说到，爬虫与网站安全，一个是矛，一个是盾。你网站安全与否，第一看安全措施是否到位，第二，还得看数据价值是否会勾引到“爬虫”的注意。也就是说，除非没有爬虫盯上你的数据，否则反爬措施你必须步步到位！哈哈。

那问题来了，如果常见的反爬我们都已经做了，发现服务器还是受到大量爬虫请求的压力，该怎么办呢？此时，JavaScript反爬虫，可能会是效果最好的一个。为什么呢？

​	你headers反爬？对不起我可以伪造User-Agent啊，我创建自己的User-Agent池，随机更换，你拿我有招么？这些信息都是你网站response里带好的哟，我祖传CV大法(复制粘贴)就能解决；

​	你想通过cookie来限制我请求？对不起我有cookie池，一样解决你；

​	你想通过封IP来限制我请求？对不起有个东西叫代理IP，几十块钱就能一天换几万个IP，我爬死你；

​	你搞各种花里胡哨的验证码防我？对不起分分钟破解你各种图形、操作验证码；

​	你动态页面加载来限制我请求？对不起我分析你XHR数据包，我找规律，我总能发现你破绽......

​	看上去好绝望是么，但，如果：

​		我尽量在动态页面加载技术中使用js来处理数据呢？

​		我把数据加密呢？比如请求中的关键参数进行加密？比如response的页面数据、json数据加密呢？

​		我不仅加密，我还给你采用更复杂的加密手段，什么常见MD5加密都是渣渣，我AES加密？我RSA加密？甚至我tm自己写加密算法行不？

​		啥你还想破解我加密？来来再提高难度！我给你js代码混淆！一堆看似简单实则混乱懵逼的变量函数名，来你有本事你给我读代码你破解！

​		于是乎往往存在以下两种结果：

​		破解不了吧，混淆的代码读的累吧，行了别费劲了洗洗睡吧...

​		wc我自定义加密算法你都能破解？小伙子有点东西啊！来我们厂上班吧....

​	哈哈开个玩笑。以上段子已经大致说明JavaScript反爬机制出现的原因了，即：JavaScript反爬目的是大幅提升爬虫破解数据的难度，进而实现对数据及网站服务器的保护。

​	而JavaScript反爬的原理其实说不简单吧也简单：使尽浑身解数就是让你难受！如何让你难受？

​		1.数据通过js加载。你不是想要我数据呢？来，分析我js代码吧！

​		2.数据再加密。啥你分析我代码还挺牛逼啊？那来接着分析分析加密算法吧！

​		3.js代码混淆。增加点难度嘿嘿，别想代码读的那么顺溜！

​	由此可见，JavaScript反爬原理可谓是思路清晰招招致命。但，青出于蓝而胜于蓝，你有你的反爬，我就有我的反反爬，总之一句话，矛的作用永远是攻破你的盾！

## Python调用JavaScript执行代码

### PyExecJS

> 这个库主要是将 JS 代码运行在本地的 JS 环境中，优点是我们有多种 JS 环境的选择，官方推荐了 PyV8、Node.js、PhantomJS、Nashorn 四种，当然缺点是必须安装一种环境导致不是很轻量，而且调用时有一个启动环境过程，还是有明显缓慢的。

- 安装

  先安装好本地的js环境。推荐安装node.js，安装简单，执行效率也很不错。

  再安装库：

  ```python
  pip install PyExecJS
  ```

- 举个例子

  ```python
  >>> import execjs
  >>> execjs.get().name  # 查看调用的环境
  'Node.js (V8)'
  >>> ctx = execjs.compile(
  """  # 执行 JS 语句
       function add(x, y) {
           return x + y;
       }
  """
  )
  >>> ctx.call("add", 1, 2)#调用函数，传递参数
  3
  >>> with open('./test.js') as f:  # 执行 JS 文件
  ...     ctx = execjs.compile(f.read())
  ...     ctx.call('add', 1, 2)
  ```

### PyV8

> 这是 Google 官方将 Chrome V8 引擎用 Python 封装的库，和 `PyExecJS` 相比，这个库很轻量，不需要额外装 JS 环境，因为 V8 本身就是环境，同时也因为不需要启动外部环境，执行速度很快。

- 安装

  在这里下载对应系统的二进制文件：[emmetio/pyv8-binaries](http://link.zhihu.com/?target=https%3A//github.com/emmetio/pyv8-binaries)

  然后解压后将 PyV8.py 与 _PyV8.so (如so不是这个名字需要改成这样) 两文件复制到 Python 的 site-packages 目录下，如 `/usr/local/lib/python3.6/site-packages`。

- 举个例子

  ```python
  >>> import PyV8  # 注意大小写
  >>> with PyV8.JSContext() as ctx:
  ...     ctx.eval("""
  ...         function add(x, y) {
  ...             return x + y;
  ...         }
  ...     """)
  ...     ctx.locals.add(1, 2)
  ```

### Js2Py

> 将 JS 代码直接转译成 Python 代码，这种方式可以摆脱调用 JS 环境的瓶颈，但遗憾的是如果用于很长的混淆 JS 代码，转译过来的大概率会报错… 所以只建议先尝试一下，如果报错及时更换上面的库。

- 安装

  ```python
  pip install js2py
  ```

- 举个例子

  ```python
  >>> import js2py
  >>> add = js2py.eval_js("""
  ...     function add(x, y) {
  ...         return x + y;
  ...     }
  ... """)
  >>> add  # 可以看到大括号里已被转译
  'function add(x, y) { [python code] }'
  >>> add(1, 2)
  3
  >>> # 使用下边这个方法可以输出转译后的代码
  >>> # 可以保存到文件里，下次不需要再次转译
  >>> print(js2py.translate_js('var x = 1'))
  from js2py.pyjs import *
  # setting scope
  var = Scope( JS_BUILTINS )
  set_global_object(var)
   
  # Code follows:
  var.registers(['x'])
  var.put('x', Js(1.0))
  ```

## 浏览器控制台：开发者工具使用技巧介绍

在这里我们以Chrome浏览器为例。

浏览器内通过F12 or 右键-- 检查 打开控制台，打开后界面如下：

![image-20200923130318905](C:\Users\安伟超\AppData\Roaming\Typora\typora-user-images\image-20200923130318905.png)

> 图中红框内容介绍如下：
>
> 1：抓手工具，反正我习惯这样叫。该图标的作用是直接在渲染出来的网页中抓取你想检索的任何元素。
>
> 2：控制台选项卡：控制台的核心功能区域。
>
> 3：elements：该选项内展示当前页面的所有元素及结构。注意，是渲染之后的最终页面结构，言外之意：很可能一次页面请求的response并不是如此完整。

控制台选项卡其余功能介绍：

> console：控制台区域，此处展示前端页面请求、加载、渲染等过程中可能出现的任何运行信息、错误信息等。同时这里还可以临时进行js代码调试。

![image-20200923130757695](C:\Users\安伟超\AppData\Roaming\Typora\typora-user-images\image-20200923130757695.png)

> network：网络请求区域，这部分是爬虫进行页面分析的核心部分。按照下图红框所列出的重点项：
>
> ALL XHR JS CSS:对一次页面请求的数据包类型进行筛选。ALL：查看全部；XHR：查看异步请求数据包；JS：查看请求的js文件；CSS：查看请求的样式表。
>
> name，status，type...:一个数据包的详细信息，name：请求的数据包名称；status：请求状态码（200表示请求成功。详细参见前文：请求状态码详解）；type:请求类型；initiator：请求的资源；size：数据大小；time：请求用时

![image-20200923131032945](C:\Users\安伟超\AppData\Roaming\Typora\typora-user-images\image-20200923131032945.png)

> source：网页的主机资源，包含详细的地址，详细的包及资源信息。

![image-20200923131418990](C:\Users\安伟超\AppData\Roaming\Typora\typora-user-images\image-20200923131418990.png)

控制台network选项卡详细介绍：

> 切换到network选项卡，点击某一个数据包，即可在右侧查看其具体详细信息，如下图；
>
> headers:包含基本的信息如请求的URL，请求方式，状态码，主机地址等相关信息；包含该数据包的请求内容及响应内容信息，关键的信息如User-agent、cookie等。
>
> preview：对响应数据的预览；
>
> response：具体的响应内容查看；

![image-20200923131637888](C:\Users\安伟超\AppData\Roaming\Typora\typora-user-images\image-20200923131637888.png)

## JavaScript逆向分析中常见的工具

### Charles——抓包

> Charles其实是一款代理服务器，通过成为电脑或者浏览器的代理，然后截取请求和请求结果达到分析抓包的目的。
>
> Charles主要功能
>
> - 支持SSL代理。可以截取分析SSL的请求。
> - 支持流量控制。可以模拟慢速网络以及等待时间（latency）较长的请求。
> - 支持AJAX调试。可以自动将json或xml数据格式化，方便查看。
> - 支持AMF调试。可以将Flash Remoting 或 Flex Remoting信息格式化，方便查看。
> - 支持重发网络请求，方便后端调试。
> - 支持修改网络请求参数。
> - 支持网络请求的截获并动态修改。
> - 检查HTML，CSS和RSS内容是否符合W3C标准。

### EditThisCookie

> EditThisCookie这款Chrome插件是一款可以管理Chrome浏览器cookies的插件，用户可以利用它添加、删除、编辑、搜索、锁定和屏蔽Chrome cookies。EditThisCookie插件是一款为谷歌浏览器定制的非常强大的一款cookies管理插件。

### Toggle Javascript

> 为切换JavaScript提供的一个简单易用的浏览器按钮，可以全局启用或禁用JavaScript。

## chrome浏览器控制台debugger

Chrome控制台的debugger主要针对的是前端js代码，其通用调试思路及步骤如下：

- 1.定位到相应js文件

- 2.格式化js代码便于阅读。点击下图红框所示图标可以一键格式化js代码：

  ![image-20200923132246416](C:\Users\安伟超\AppData\Roaming\Typora\typora-user-images\image-20200923132246416.png)

- 3.在左侧行号上左键点击打下断点，右侧开始图标启动debug：

  ![image-20200923132433141](C:\Users\安伟超\AppData\Roaming\Typora\typora-user-images\image-20200923132433141.png)

  右侧图标从左向右依次的含义为：

  > 启动debug，运行到断点处，等待单步调试；
  >
  > 单步调试，一次回车 or 点击该图标 or F10执行一行代码；
  >
  > 进入下一个函数体；
  >
  > 退出当前函数体；

  右侧的watch区域可以查看某参数值；

  右侧的scope区域可以查看函数内变量、参数跟随debug过程的值变化；

## 处理js代码混淆

在日常的爬虫分析页面的过程中，我们常常需要对异步加载的数据进行分析，而现今大部分异步加载的数据都是通过js进行加载的，所以也避免不了分析js代码。可是在分析js代码的过程中我们经常发现一个现象：一段代码中变量名用特简单的单个字母表示，如abcde等，同时，你还会发现出现了很多同名的变量名称，比如变量a，函数a，对象a等。如此js代码自然就增加了分析的难度。这就是js代码混淆。

js代码混淆存在的意义就是为了保护数据和代码，在反爬虫方面的意义则很明显：反制爬虫程序，提升爬虫程序破解js代码的难度，进而起到保护数据及服务器站点等目的。

在了解如何处理js代码混淆之前，我们先了解js代码到底如何混淆的。

### 为什么要进行js代码混淆

> 在web应用越来越丰富的今天，伴随着浏览器性能和网速的提高，js承载了更多的工作，不少后端逻辑都在向前端转移，与此同时也让更多的不法分子有机可乘。在web模型中，js往往是不法分子的第一个突破口。知晓了前端逻辑，不法分子可以模拟成一个正常的用户来实施自己的恶意行为。所以，在很多登录、注册、支付、交易等等页面中，关键业务和风控系统依赖的js都不希望被人轻易的破解，js混淆应运而生。

- js代码混淆不是纸老虎——“专门吓唬人的实则并没有什么卵用”

  实际上，代码混淆早就不是一个新鲜的名词，在桌面软件时代，大多数的软件都会进行代码混淆、加壳等手段来保护自己的代码。Java和.NET都有对应的混淆器。黑客们对这个当然也不陌生，许多病毒程序为了反查杀，也会进行高度的混淆。只不过由于js是动态脚本语言，在http中传输的就是源代码，逆向起来要比打包编译后的软件简单很多，很多人因此觉得混淆是多此一举。

### 如何进行js代码混淆

js代码混淆主要依靠混淆器。

混淆器大致两种：

- 通过正则替换实现的混淆器
- 通过语法树替换实现的混淆器

第一种实现成本低，但是效果也一般，适合对混淆要求不高的场景。第二种实现成本较高，但是更灵活，而且更安全，更适合对抗场景

当然，也有通过以下几种方式进行js代码混淆的：

- 可怕的eval()函数：js中有个函数叫eval，贼tm臭名昭著的eval，效率又低，可读性又差...但，针对爬虫的话这个就牛皮了，一般新手小白第一次碰到直接懵逼....
- 符号混淆：将代码混淆成各种各样的代码，视觉上直观“吓死你”，让你一看就想“抱歉，打扰了”。但实则此类混淆非常好破解。

除此之外，也有个别真心损的大厂，将js代码混淆成英语之外的语言，例如阿拉伯语......阿拉伯语有的时候从左向右书写，也能从右向左书写，还能从上到下书写......所以除非你懂阿拉伯语，或者你身边有阿拉伯人，或者你是老板你雇个阿拉伯籍的程序员，否则就GG.....

不过，虽然js代码混淆的目的是保护数据代码及服务器站点，但毕竟我们还讲究个所谓的边际效应。这是经济学的概念，大致意思就是说当付出的成本高到一定程度的时候，收益相对就不是很多了。爬虫无非就是个攻防游戏，RMB玩家才是牛逼所在。无条件死磕，不划算，两败俱伤。或者换句话说：送人玫瑰，手留余香。真要是混淆成别的语言，这就过分了。我适当混淆防你，我到此为止，你要是非得爬那就爬吧，做人做事不能太绝对，给爬虫程序员一条活路，没准哪天自己也去干爬虫了，那就叫“天道好轮回，苍天饶过谁”~

### 混淆器对js代码性能的影响

由于增加了废代码，改变了原有的AST，混淆对性能肯定会造成一定的影响，但是我们可以通过规则来控制影响的大小。

> · 减少循环混淆，循环太多会直接影响代码执行效率
>
> · 避免过多的字符串拼接，因为字符串拼接在低版本IE下面会有性能问题
>
> · 控制代码体积，在插入废代码时应该控制插入比例，文件过大会给网络请求和代码执行都带来压力

我们通过一定的规则完全可以把性能影响控制在一个合理的范围内，实际上，有一些混淆规则反而会加快代码的执行，比如变量名和属性名的压缩混淆，会减小文件体积，比如对全局变量的复制，会减少作用域的查找等等。

### 混淆的安全性

混淆的目的是保护代码，但是如果因为混淆影响了正常功能就舍本逐末了。

由于混淆后的AST已经和原AST完全不同了，但是混淆后的文件和原文件执行结果必须一样，如何保证既兼顾了混淆强度，又不破坏代码执行呢？高覆盖的测试必不可少：

> · 对自己的混淆器写详尽的单元测试
>
> · 对混淆的目标代码做高覆盖的功能测试，保证混淆前后代码执行结果完全一样
>
> · 多样本测试，可以混淆单元测试已经完备了的类库，比如混淆 Jquery 、AngularJS 等，然后拿混淆后的代码去跑它们的单元测试，保证和混淆前执行结果完全一样

### 如何处理js代码混淆

两种情形：

- 产品向浏览器提供了反混淆算法，方便用户运行 -- 比较少见

  如果能通过技术手段比如常见的爬虫请求模块请求到该反混淆算法，这真是极(xiang)好(pi)的(chi....噗哈哈哈)；

- 没有工具，没有反混淆算法——自己动手丰衣足食吧。

#### 常见js代码混淆的处理

- “haha”哈哈大法：针对eval函数混淆的方式，如果目标js代码经过eval()函数混淆，只需在控制台输入：

  ```javascript
  var haha = (...)//括号中的内容为eval()中的字符串参数
  console.log(haha)
  ```

- 颜文字组成的混淆代码：如下

  ![image-20200923144414204](C:\Users\安伟超\AppData\Roaming\Typora\typora-user-images\image-20200923144414204.png)

  解决办法：复制代码到控制台，删除最后表情（·-·）和‘；’，加上.toString()，运行后就会出现混淆前的js

- 符号组成的混淆代码：如下

  ![image-20200923144508171](C:\Users\安伟超\AppData\Roaming\Typora\typora-user-images\image-20200923144508171.png)

  解决办法：复制代码到控制台，删除最后“（）；”，加上.toString()，运行后就会出现混淆前的js

- 都不是以上的混淆算法，而是我们见到最多的abc混淆：

  - 借助Python执行js代码工具模块直接运行；
  - 控制台内通过打断点进行debugger分析js代码参数变化

## 定位加密数据

面对js代码混淆和加密，我们在进行js逆向分析中，需要能够定位到所需数据存在的js文件中的具体位置。大致思路流程如下：

- 控制台中，通过ctrl + shift +F先进行全局搜索目标关键字；
- 在众多搜索结果中一一检索目标关键字所在的js文件路径，一般在source资源中检索；
- 检索到目标关键字所在的js文件后，格式化查看该js代码；
- js文件内ctrl + F检索到关键字位置，分析其上下文代码；
- 如果引用到其他的参数或函数，则继续搜索对应关键字；
- 直至找到目标数据的加密算法——通常对应某一个函数或某一个函数的内的某一部分功能实现。

## 数据的编码与加密

### ASCII编码

> ASCII ((American Standard Code for Information Interchange): 美国信息交换标准代码）是基于[拉丁字母](https://baike.baidu.com/item/拉丁字母/1936851)的一套电脑[编码](https://baike.baidu.com/item/编码/80092)系统，主要用于显示现代[英语](https://baike.baidu.com/item/英语/109997)和其他[西欧](https://baike.baidu.com/item/西欧/3028649)语言。它是最通用的信息交换标准，并等同于[国际](https://baike.baidu.com/item/国际)标准ISO/IEC 646。ASCII第一次以规范标准的类型发表是在1967年，最后一次更新则是在1986年，到目前为止共定义了128个字符

详细的ASCII编码表参见百度百科——词条：ASCII

### base64编码

> Base64是网络上最常见的用于传输8Bit[字节码](https://baike.baidu.com/item/字节码/9953683)的编码方式之一，Base64就是一种基于64个可打印字符来表示[二进制](https://baike.baidu.com/item/二进制/361457)数据的方法。可查看RFC2045～RFC2049，上面有MIME的详细规范。
>
> Base64编码是从二进制到字符的过程，可用于在[HTTP](https://baike.baidu.com/item/HTTP)环境下传递较长的标识信息。采用Base64编码具有不可读性，需要解码后才能阅读。
>
> Base64由于以上优点被广泛应用于计算机的各个领域，然而由于输出内容中包括两个以上“符号类”字符（+, /, =)，不同的应用场景又分别研制了Base64的各种“变种”。为统一和规范化Base64的输出，Base62x被视为无符号化的改进版本。

#### 用Python实现base64编解码

- 编码

  ```python
  import base64
  a = 'HC'.decode() #将‘HC’转为二进制
  b = base64.b64encode(a) #将a转为base64编码
  b.decode() #从二进制转回
  
  base64.b64encode('HC'.encode()).decode() #简写'SEM=
  ```

- 解码

  ```python
  base64.b64decode('SEM=').decode()
  'HC'
  ```

### MD5加密算法

> **MD5信息摘要算法**（英语：MD5 Message-Digest Algorithm），一种被广泛使用的[密码散列函数](https://baike.baidu.com/item/密码散列函数/14937715)，可以产生出一个128位（16[字节](https://baike.baidu.com/item/字节/1096318)）的散列值（hash value），用于确保信息传输完整一致。MD5由美国密码学家[罗纳德·李维斯特](https://baike.baidu.com/item/罗纳德·李维斯特/700199)（Ronald Linn Rivest）设计，于1992年公开，用以取代[MD4](https://baike.baidu.com/item/MD4/8090275)算法。这套算法的程序在 RFC 1321 标准中被加以规范。1996年后该算法被证实存在弱点，可以被加以破解，对于需要高度安全性的数据，专家一般建议改用其他算法，如[SHA-2](https://baike.baidu.com/item/SHA-2/22718180)。2004年，证实MD5算法无法防止碰撞（collision），因此不适用于安全性认证，如[SSL](https://baike.baidu.com/item/SSL/320778)公开密钥认证或是[数字签名](https://baike.baidu.com/item/数字签名/212550)等用途。

#### Python处理MD5加密

```python
# 由于MD5模块在python3中被移除
# 在python3中使用hashlib模块进行md5操作

import hashlib

# 待加密信息
str = 'this is a md5 test.'

# 创建md5对象
m = hashlib.md5()

# Tips
# 此处必须encode
# 若写法为m.update(str)  报错为： Unicode-objects must be encoded before hashing
# 因为python3里默认的str是unicode
# 或者 b = bytes(str, encoding='utf-8')，作用相同，都是encode为bytes
b = str.encode(encoding='utf-8')
m.update(b)
str_md5 = m.hexdigest()

print('MD5加密前为 ：' + str)
print('MD5加密后为 ：' + str_md5)

# 另一种写法：b‘’前缀代表的就是bytes
str_md5 = hashlib.md5(b'this is a md5 test.').hexdigest()
print('MD5加密后为 ：' + str_md5)
```

### 对称加密算法

> 对称加密算法是应用较早的加密算法，技术成熟。在对称加密算法中，数据发信方将明文（原始数据）和加密密钥（mi yao）一起经过特殊加密算法处理后，使其变成复杂的加密密文发送出去。收信方收到密文后，若想解读原文，则需要使用加密用过的密钥及相同算法的逆算法对密文进行解密，才能使其恢复成可读明文。在对称加密算法中，使用的密钥只有一个，发收信双方都使用这个密钥对数据进行加密和解密，这就要求解密方事先必须知道加密密钥。

### 非对称加密算法

> 非[对称加密算法](https://baike.baidu.com/item/对称加密算法)是一种密钥的保密方法。
>
> 非对称加密算法需要两个密钥：[公开密钥](https://baike.baidu.com/item/公开密钥/7453570)（publickey:简称公钥）和私有密钥（privatekey:简称私钥）。公钥与私钥是一对，如果用公钥对数据进行加密，只有用对应的私钥才能解密。因为加密和解密使用的是两个不同的密钥，所以这种算法叫作非对称加密算法。 非对称加密算法实现机密信息交换的基本过程是：甲方生成一对[密钥](https://baike.baidu.com/item/密钥/101144)并将公钥公开，需要向甲方发送信息的其他角色(乙方)使用该密钥(甲方的公钥)对机密信息进行加密后再发送给甲方；甲方再用自己私钥对加密后的信息进行解密。甲方想要回复乙方时正好相反，使用乙方的公钥对数据进行加密，同理，乙方使用自己的私钥来进行解密。
>
> 另一方面，甲方可以使用自己的私钥对机密信息进行签名后再发送给乙方；乙方再用甲方的公钥对甲方发送回来的数据进行验签。
>
> 甲方只能用其私钥解密由其公钥加密后的任何信息。 非[对称加密算法](https://baike.baidu.com/item/对称加密算法)的保密性比较好，它消除了最终用户交换密钥的需要。
>
> 非对称[密码体制](https://baike.baidu.com/item/密码体制)的特点：算法强度复杂、安全性依赖于算法与密钥但是由于其算法复杂，而使得加密解密速度没有对称加密解密的速度快。对称密码体制中只有一种密钥，并且是非公开的，如果要解密就得让对方知道密钥。所以保证其安全性就是保证密钥的安全，而非对称密钥体制有两种密钥，其中一个是公开的，这样就可以不需要像对称密码那样传输对方的密钥了。这样安全性就大了很多。

### AES加密

> 密码学中的高级加密标准（Advanced Encryption Standard，AES），又称Rijndael[加密法](https://baike.baidu.com/item/加密法)，是美国联邦政府采用的一种区块加密标准。

严格地说，AES和Rijndael[加密法](https://baike.baidu.com/item/加密法)并不完全一样（虽然在实际应用中二者可以互换），因为Rijndael加密法可以支持更大范围的[区块](https://baike.baidu.com/item/区块)和[密钥长度](https://baike.baidu.com/item/密钥长度)：AES的区块长度固定为128位，密钥长度则可以是128，192或256位；而Rijndael使用的密钥和区块长度可以是32位的整数倍，以128位为下限，256位为上限。加密过程中使用的密钥是由[Rijndael密钥生成方案](https://baike.baidu.com/item/Rijndael密钥生成方案)产生。

大多数AES计算是在一个特别的[有限域](https://baike.baidu.com/item/有限域)完成的。

AES加密过程是在一个4×4的[字节](https://baike.baidu.com/item/字节)矩阵上运作，这个矩阵又称为“体（state）”，其初值就是一个明文区块（矩阵中一个元素大小就是明文区块中的一个Byte）。（Rijndael[加密法](https://baike.baidu.com/item/加密法)因支持更大的区块，其矩阵行数可视情况增加）加密时，各轮AES加密循环（除最后一轮外）均包含4个步骤：

AddRoundKey

[![将每个状态中的字节与该回合金钥做异或](https://bkimg.cdn.bcebos.com/pic/6609c93d70cf3bc7a6c87f8bd100baa1cc112a88?x-bce-process=image/resize,m_lfit,w_220,limit_1)](https://baike.baidu.com/pic/高级加密标准/468774/0/d35a10f422202a39dcc474e9?fr=lemma&ct=single)将每个状态中的字节与该回合金钥做异或

—矩阵中的每一个[字节](https://baike.baidu.com/item/字节)都与该次回合金钥（round key）做XOR运算；每个子密钥由密钥生成方案产生。

AddRoundKey步骤，回合密钥将会与原矩阵合并。在每次的加密循环中，都会由主密钥产生一把回合密钥（通过Rijndael密钥生成方案产生），这把密钥大小会跟原矩阵一样，以与原矩阵中每个对应的字节作异或（⊕）加法。

SubBytes

—通过一个非线性的替换函数，用[查找表](https://baike.baidu.com/item/查找表)的方式把每个[字节](https://baike.baidu.com/item/字节)替换成对应的字节。

在SubBytes步骤中，矩阵中的各字节通过一个8位的S-box进行转换。这个步骤提供了加密法非线性的变换能力。 S-box与GF（2）上的乘法反元素有关，已知具有良好的非线性特性。为了避免简单代数性质的攻击，S-box结合了乘法反元素及一个可逆的仿射变换矩阵建构而成。此外在建构S-box时，刻意避开了固定点与反固定点，即以S-box替换字节的结果会相当于错排的结果。

ShiftRows

—将矩阵中的每个横列进行循环式移位。

ShiftRows描述矩阵的行操作。在此步骤中，每一行都向左循环位移某个[偏移量](https://baike.baidu.com/item/偏移量/9180391)。在AES中（区块大小128位），第一行维持不变，第二行里的每个字节都向左循环移动一格。同理，第三行及第四行向左循环位移的偏移量就分别是2和3。128位和192比特的区块在此步骤的循环位移的模式相同。经过ShiftRows之后，矩阵中每一竖列，都是由输入矩阵中的每个不同列中的元素组成。Rijndael算法的版本中，偏移量和AES有少许不同；对于长度256比特的区块，第一行仍然维持不变，第二行、第三行、第四行的偏移量分别是1字节、3字节、4位组。除此之外，ShiftRows操作步骤在Rijndael和AES中完全相同 [3] 。

MixColumns

—为了充分[混合矩阵](https://baike.baidu.com/item/混合矩阵)中各个直行的操作。这个步骤使用线性转换来混合每内联的四个[字节](https://baike.baidu.com/item/字节)。最后一个加密循环中省略MixColumns步骤，而以另一个AddRoundKey取代。

AES只是个基本算法，实现AES有几种模式，主要有ECB、CBC、CFB和OFB这几种（其实还有个CTR）：

**1.ECB模式（电子密码本模式：Electronic codebook）**

ECB是最简单的块密码加密模式，加密前根据加密块大小（如AES为128位）分成若干块，之后将每块使用相同的密钥单独加密，解密同理。

**2.CBC模式（密码分组链接：Cipher-block chaining）**

CBC模式对于每个待加密的密码块在加密前会先与前一个密码块的密文异或然后再用加密器加密。第一个明文块与一个叫初始化向量的数据块异或。

**3.CFB模式（密文反馈：Cipher feedback）**

与ECB和CBC模式只能够加密块数据不同，CFB能够将块密文（Block Cipher）转换为流密文（Stream Cipher）。

**4.OFB模式（输出反馈：Output feedback）**

OFB是先用块加密器生成密钥流（Keystream），然后再将密钥流与明文流异或得到密文流，解密是先用块加密器生成密钥流，再将密钥流与密文流异或得到明文，由于异或操作的对称性所以加密和解密的流程是完全一样的。

### RSA加密

> RSA是1977年由[罗纳德·李维斯特](https://baike.baidu.com/item/罗纳德·李维斯特/700199)（Ron Rivest）、[阿迪·萨莫尔](https://baike.baidu.com/item/阿迪·萨莫尔)（Adi Shamir）和[伦纳德·阿德曼](https://baike.baidu.com/item/伦纳德·阿德曼/12575612)（Leonard Adleman）一起提出的。当时他们三人都在[麻省理工学院](https://baike.baidu.com/item/麻省理工学院/117999)工作。RSA就是他们三人姓氏开头字母拼在一起组成的。

RSA公开密钥密码体制是一种使用不同的加密密钥与解密密钥，“由已知加密密钥推导出解密密钥在计算上是不可行的”密码体制 [2] 。

在公开密钥密码体制中，加密密钥（即公开密钥）PK是公开信息，而解密密钥（即秘密密钥）SK是需要保密的。加密算法E和解密算法D也都是公开的。虽然解密密钥SK是由公开密钥PK决定的，但却不能根据PK计算出SK [2] 。

正是基于这种理论，1978年出现了著名的RSA算法，它通常是先生成一对RSA密钥，其中之一是保密密钥，由用户保存；另一个为公开密钥，可对外公开，甚至可在网络服务器中注册。为提高保密强度，RSA密钥至少为500位长，一般推荐使用1024位。这就使加密的计算量很大。为减少计算量，在传送信息时，常采用传统加密方法与公开密钥加密方法相结合的方式，即信息采用改进的DES或IDEA对话密钥加密，然后使用RSA密钥加密对话密钥和信息摘要。对方收到信息后，用不同的密钥解密并可核对信息摘要 [2] 。

RSA是被研究得最广泛的公钥算法，从提出到现在已近三十年，经历了各种攻击的考验，逐渐为人们接受，普遍认为是目前最优秀的公钥方案之一。1983年麻省理工学院在美国为RSA算法申请了专利。

RSA算法的具体描述如下： [5] 

（1）任意选取两个不同的大素数p和q计算乘积

![img](https://bkimg.cdn.bcebos.com/formula/f0dac18152076624d87832b62709895c.svg)

 [5] ；

（2）任意选取一个大整数e，满足

![img](https://bkimg.cdn.bcebos.com/formula/c33d8c66364a636b051d82f0ee202a36.svg)

 ，整数e用做加密钥（注意：e的选取是很容易的，例如，所有大于p和q的素数都可用） [5] ；

（3）确定的解密钥d，满足

![img](https://bkimg.cdn.bcebos.com/formula/da8649c0078a0a842779394d64011776.svg)

 ，即

![img](https://bkimg.cdn.bcebos.com/formula/4dee3f4df52a81983db0e3c619f96058.svg)

 是一个任意的整数；所以，若知道e和

![img](https://bkimg.cdn.bcebos.com/formula/679e809a0d964785d0aa4cfcb4218742.svg)

，则很容易计算出d [5] ；

（4）公开整数n和e，秘密保存d [5] ；

（5）将明文m（m<n是一个整数）加密成密文c，加密算法为 [5] 

![img](https://bkimg.cdn.bcebos.com/formula/5947116555169dc6fe9e3f5cdf347706.svg)

（6）将密文c解密为明文m，解密算法为 [5] 

![img](https://bkimg.cdn.bcebos.com/formula/1a8b337167e4d4b2c23855d88ec4c67f.svg)

然而只根据n和e（注意：不是p和q）要计算出d是不可能的。因此，任何人都可对明文进行加密，但只有授权用户（知道d）才可对密文解密 [5] 。

### Python处理AES加密及RSA加密的标准库——[PyCryptodome](https://www.pycryptodome.org/en/latest/)

PyCryptodome是python一个强大的加密算法库，可以实现常见的单向加密、对称加密、非对称加密和流加密算法。直接pip安装即可：

```python
pip install pycryptodome
```

#### 对称加密算法实现（以AES算法CBC模式为例）

加密代码如下：

```python
from Crypto.Cipher import AES
from Crypto.Util.Padding import pad
from Crypto.Random import get_random_bytes

# 要加密的内容
data = b"123456"
# 随机生成16字节（即128位）的加密密钥
key = get_random_bytes(16)
# 实例化加密套件，使用CBC模式
cipher = AES.new(key, AES.MODE_CBC)
# 对内容进行加密，pad函数用于分组和填充
encrypted_data = cipher.encrypt(pad(data, AES.block_size))

# 将加密内容写入文件
file_out = open("encrypted.bin", "wb")
# 在文件中依次写入key、iv和密文encrypted_data
[file_out.write(x) for x in (key, cipher.iv,  encrypted_data)]
```

对应解密代码如下：

```python
from Crypto.Cipher import AES
from Crypto.Util.Padding import unpad

# 从前边文件中读取出加密的内容
file_in = open("encrypted.bin", "rb")
# 依次读取key、iv和密文encrypted_data，16等是各变量长度，最后的-1则表示读取到文件末尾
key, iv, encrypted_data = [file_in.read(x) for x in (16, AES.block_size, -1)]

# 实例化加密套件
cipher = AES.new(key, AES.MODE_CBC, iv)
# 解密，如无意外data值为最先加密的b"123456"
data = unpad(cipher.decrypt(encrypted_data), AES.block_size)
```

#### 非对称加密算法实现（以RSA为例）

生成密钥对代码如下：

```python
from Crypto.PublicKey import RSA# 生成密钥对
key = RSA.generate(2048)

# 提取私钥并存入文件
private_key = key.export_key()
file_out = open("private_key.pem", "wb")
file_out.write(private_key)

# 提取公钥存入文件
public_key = key.publickey().export_key()
file_out = open("public_key.pem", "wb")
file_out.write(public_key)
```

加密代码如下：

```python
from Crypto.PublicKey import RSA
from Crypto.Cipher import PKCS1_OAEP

# 要加密的内容
data = b"123456"
# 从文件中读取公钥
public_key = RSA.import_key(open("public_key.pem").read())
# 实例化加密套件
cipher = PKCS1_OAEP.new(public_key)
# 加密
encrypted_data = cipher.encrypt(data)

# 将加密后的内容写入到文件
file_out = open("encrypted_data.bin", "wb")
file_out.write(encrypted_data)
```

解密代码如下：

```python
from Crypto.PublicKey import RSA
from Crypto.Cipher import PKCS1_OAEP

# 从私钥文件中读取私钥
private_key = RSA.import_key(open("private_key.pem", "rb").read())
# 实例化加密套件
cipher = PKCS1_OAEP.new(private_key)
# 从文件中读取加密内容
encrypted_data = open("encrypted_data.bin", "rb").read()
# 解密，如无意外data值为最先加密的b"123456"
data = cipher.decrypt(encrypted_data)
```

# <font color='red'>案例：破解js加密爬取网易云音乐任意vip付费歌曲</font>

<font color='red' size=4>*参见代码：[Spider_Codes/demo19_Music163_Vip_download_OOP.py](https://github.com/La0bALanG/Spider_Codes)*</font>

- 目标

  - 输入任意歌手名称或歌曲名称，列出所有的查询结果
  - 自行选择其中某一条想要的歌曲，将其下载至本地

- 请求URL分析

  打开网易云，随机选择一首歌曲，进入其播放页面，点击播放后，F12打开控制台，

  控制台选择network -- XHR选项，查看左侧列出的一次请求的XHR数据包，

  多次刷新播放，并查看XHR数据包发现：

  "v1?csrf_token=..."数据包为歌曲信息相关的内容；

  先选择preview(预览)查看下当前歌曲的URL：

  

  ![image-20200916153913192](C:\Users\安伟超\AppData\Roaming\Typora\typora-user-images\image-20200916153913192.png)

  ​	

  看到该URL后，确定该XHR数据包确实为歌曲的相关信息；

  接下来回到headers内查看下该数据包的请求URL：

  ![image-20200916154110915](C:\Users\安伟超\AppData\Roaming\Typora\typora-user-images\image-20200916154110915.png)

  由此可知当前XHR数据包的请求URL为:

  ```python
  https://music.163.com/weapi/song/enhance/player/url/v1?csrf_token=
  ```

  其请求方式为POST;

  既然为POST请求方式，那么一定会携带请求体。在headers选项内继续下拉查看下form_data:

  ![image-20200916154934522](C:\Users\安伟超\AppData\Roaming\Typora\typora-user-images\image-20200916154934522.png)

  在这里我们看到了，POST提交了两个参数：parmas和encSecKey;

  从这两个参数的具体值上我们能够明显的看出，这两个参数是经过加密处理的。

  现在我们多进行几次提交刷新(播放不同的歌曲)，我们发现，这两个参数值不是固定的，而是时刻改变的，由此我们能确定，该参数在加密时应该是存在随机操作的，但是两参数其各自长度值始终保持不变，即参数parmas长度为152，参数encSecKey长度为256.

  进行到此步，正式请求的XHR接口的URL及其对应所需参数均已找到，下一步我们就需要确定两个参数是如何进行加密的。

- 参数加密分析

  上一步，我们确定了两个参数：parmas以及encSecKey，接下来我们要确定其具体的加密方式，则需要先在相应的js文件中定位到该参数的加密方法(说白了就是找到参数的加密函数)。

  第一步，我们先在全局搜索下参数encSecKey，发现定位到了两个文件：

  ![image-20200916160109628](C:\Users\安伟超\AppData\Roaming\Typora\typora-user-images\image-20200916160109628.png)

  我们将该js文件进行格式化查看，并检索到参数encSecKey的关键位置：

  ![image-20200916160405238](C:\Users\安伟超\AppData\Roaming\Typora\typora-user-images\image-20200916160405238.png)

  当然到这我们只能猜测这就是加密函数，毕竟我们还没有dubgger具体的代码及数据；

  我们先把这段代码摘出来：

  ```javascript
  var bVZ7S = window.asrsea(JSON.stringify(i9b), bqN9E(["流泪", "强"]), bqN9E(Wx4B.md), bqN9E(["爱心", "女孩", "惊恐", "大笑"]));
  e9f.data = j9a.cs0x({
      params: bVZ7S.encText,
      encSecKey: bVZ7S.encSecKey
  })
  ```

  先不debug，我们先简单分析：

  首先，这个window.asrsea()应该是个加密函数，其需要传递四个参数，该函数接收这四个参数之后调用，获得返回值赋值给变量bVZ7S；

  那么这个变量就应该有两个属性：bVZ7S.encText 和 bVZ7S.encSecKey，那么这两个属性也就赋值给了我们想要的参数params 和encSecKey。

  简单分析完代码思路后，我们现在开始debug一下，确认我们的分析是否正确：

  首先，在13133行设置断点，执行debug，刷新页面，执行到断点处后打开console，我们先看一下这四个参数，其次在右侧的watch中我们查看下变量bVZ7S的值：

  ![image-20200916161419523](C:\Users\安伟超\AppData\Roaming\Typora\typora-user-images\image-20200916161419523.png)

  从右侧watch区域查看的变量bVZ7S的值来看，证实了window.asrsea()就是加密函数.接下来我们将该函数所需的四个参数及参数值打印出来看一下：

  ```javascript
  JSON.stringify(i9b)
  "{"csrf_token":""}"
  bqN9E(["流泪", "强"])
  "010001"
  bqN9E(Wx4B.md)
  "00e0b509f6259df8642dbc35662901477df22677ec152b5ff68ace615bb7b725152b3ab17a876aea8a5aa76d2e417629ec4ee341f56135fccf695280104e0312ecbda92557c93870114af6c9d05c4f7f0c3685b7a46bee255932575cce10b424d813cfe4875d3e82047b97ddef52741d546b8e289dc6935b3ece0462db0a22b8e7"
  bqN9E(["爱心", "女孩", "惊恐", "大笑"])
  
  "0CoJUm6Qyw8W8jud"
  ```

  即window.asrsea()加密函数所需的四个参数值已经确定，均为字符串，分别是：

  ```javascript
  "{"csrf_token":""}"
  
  "010001"
  
  "00e0b509f6259df8642dbc35662901477df22677ec152b5ff68ace615bb7b725152b3ab17a876aea8a5aa76d2e417629ec4ee341f56135fccf695280104e0312ecbda92557c93870114af6c9d05c4f7f0c3685b7a46bee255932575cce10b424d813cfe4875d3e82047b97ddef52741d546b8e289dc6935b3ece0462db0a22b8e7"
  
  "0CoJUm6Qyw8W8jud"
  ```

  其中，第三个参数为十六进制编码。同时，我们在当前页面下多次刷新，发现这几个值不变。

  至此，一个XHR数据包的请求URL所需的参数我们分析完了，接下来就是解决这两个参数到底是如何加密的，搞清楚加密算法之后我们采用python进行同等模拟即可。

- 加密分析

  上一步，我们确定了window.asrsea()为加密函数，所以我们先看看这个函数是不是JavaScript的原生加密函数。很简单，百度直接搜索该函数，发现并没有任何匹配结果，所以，该加密函数并不是原生JavaScript函数，而是开发者自定义的。这就有点小小困难了，因为我们真的要分析其加密算法了...

  现在开始正式分析。第一步，我们先继续在当前js文件内部搜索函数名asrsea，定位其位置：

  ![image-20200916162523318](C:\Users\安伟超\AppData\Roaming\Typora\typora-user-images\image-20200916162523318.png)

  找到该算法后我们看到了，asrsea函数其实就是d函数，这个d函数就是我们要找到的加密函数，其接收的d,e,f,g四个参数对应的就是window.asrsea()函数的四个参数，即：

  ```javascript
  d = "{"csrf_token":""}"
  
  e = "010001"
  
  f = "00e0b509f6259df8642dbc35662901477df22677ec152b5ff68ace615bb7b725152b3ab17a876aea8a5aa76d2e417629ec4ee341f56135fccf695280104e0312ecbda92557c93870114af6c9d05c4f7f0c3685b7a46bee255932575cce10b424d813cfe4875d3e82047b97ddef52741d546b8e289dc6935b3ece0462db0a22b8e7"
  
  g = "0CoJUm6Qyw8W8jud"
  ```

  到这其实应该发现了一个困惑已久的问题，为啥看了那么多被我爬过的页面的js代码，怎么他们变量命名这么简单？无论是函数名还是变量名甚至参数都直接来一个字母？而且甚至还出现了相同的？没错，这其实就是一种比较常见的反爬虫手段——JS代码混淆。

  继续。我们把这几个参数的加密函数直接摘出来分析一下：

  ```javascript
  !function() {
      function a(a) {
          var d, e, b = "abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789", c = "";
          for (d = 0; a > d; d += 1)
              e = Math.random() * b.length,
              e = Math.floor(e),
              c += b.charAt(e);
          return c
      }
      /*
      
      函数a的作用是：从字符串"abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789"中随机生成长度为a的字符串
      
      */
      function b(a, b) {
          var c = CryptoJS.enc.Utf8.parse(b)
            , d = CryptoJS.enc.Utf8.parse("0102030405060708")
            , e = CryptoJS.enc.Utf8.parse(a)
            , f = CryptoJS.AES.encrypt(e, c, {
              iv: d,
              mode: CryptoJS.mode.CBC
          });
          return f.toString()
      }
      /*
      
      函数b的作用是对数据a进行AES加密，加密模式为CBC，最后在通过toString()方法将结果转化为字符串
      
      */
      function c(a, b, c) {
          var d, e;
          return setMaxDigits(131),
          d = new RSAKeyPair(b,"",c),
          e = encryptedString(d, a)
      }
      /*
      
      函数c的作用是对数据a进行RSA加密，返回的结果是十六进制形式的字符串
      
      */
      function d(d, e, f, g) {
          var h = {}
            , i = a(16);
          return h.encText = b(d, g),
          h.encText = b(h.encText, i),
          h.encSecKey = c(i, e, f),
          h
      }
      /*
      
      函数d的作用是对数据d进行加密，得到两个加密结果encText和encSecKey，而其具体的加密方法是：使用函数a随机生成长度为16的字符串，将其结果通过函数b进行第一次AES加密，然后在通过函数b对第一次的加密结果再进行一次AES加密，得到结果encText，该结果即对应我们的parmas；最后通过函数c进行一次RSA加密，得到结果encSecKey
      
      */
      function e(a, b, d, e) {
          var f = {};
          return f.encText = c(a + e, b, d),
          f
      }
      window.asrsea = d,
      window.ecnonasr = e
  }();
  ```

  至此，加密算法我们挨个分析完了，接下来我们就开始使用python比对js加密算法模拟出python的加密算法。

- 模拟加密

  > 这里我们使用一个非常强大的加密算法库——[PyCryptodome](https://www.pycryptodome.org/en/latest/)

  第一步，我们先在函数d中打上断点，分析一下a,b,c三个函数执行完毕后返回的结果，方便我们下一步比对模拟加密算法：

  ![image-20200916165244289](C:\Users\安伟超\AppData\Roaming\Typora\typora-user-images\image-20200916165244289.png)

  程序执行到函数a处，在最右边变量作用域区scope可以看到各个变量的值及函数a返回的的结果i: "onh267xxLCtlpPb1"。

  由此，我们先模拟函数a的加密算法。

  定义一个加密算法模拟类EncryptText，用于模拟JavaScript的加密过程：

  ```python
  class EncryptText:
      def __init__(self):
        self.character = 'abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789'
          self.iv = '0102030405060708'
        self.public_key = '010001'
          self.modulus = '00e0b509f6259df8642dbc35662901477df22677ec152b' \
                       '5ff68ace615bb7b725152b3ab17a876aea8a5aa76d2e417' \
                         '629ec4ee341f56135fccf695280104e0312ecbda92557c93' \
                         '870114af6c9d05c4f7f0c3685b7a46bee255932575cce10b' \
                         '424d813cfe4875d3e82047b97ddef52741d546b8e289dc69' \
                         '35b3ece0462db0a22b8e7'
          self.nonce = '0CoJUm6Qyw8W8jud'
  
  ```

  接下来我们模拟函数a的加密过程。首先我们先使用官方提供的API：Crypto.Random.get_random_bytes(N)，该方法执行完毕后返回一个长度为N的随机字符串：

  ```python
      def create16RandomBytes(self):
          """
          # 产生16位随机字符, 对应函数a
          :return:
          """
          generated_string = get_random_bytes(16)
          return generated_string
  
  ```

  得到返回结果后我们需要通过decode()方法将其转换成字符串，但是该方法随机产生的字节串是这样的：

  ```python
  (venv) F:\老安课程串讲资料\文档、代码杂七八\BarranziLessonSource\PythonSpider\Spider_Code>python test_demo.py
  b'\xa5\xc7\xe7\x90\xa4@\xeb\xefU7\x99\xf0\xa7\xbag\xf5'
  ```

  此字节串在转换字符串时就会产生UnicodeDecodeError，所以在这里我们不采用官方API实现，采用自定义加密算法：

  ```python
      def create16RandomBytes(self):
          """
          # 产生16位随机字符, 对应函数a
          :return:
          """
          generate_string = random.sample(self.character, 16)
          generated_string = ''.join(generate_string)
          return generated_string
  
  ```

  

  此时该方法产生的结果就是16位随机的字符串：

  ```python
  (venv) F:\老安课程串讲资料\文档、代码杂七八\BarranziLessonSource\PythonSpider\Spider_Code>python test_demo.py
  UBoAfHIcWTbSEMKt
  ```

  继续。依据之前debug结果，当程序执行到函数b处，传入的参数d和g的值我们已经知晓，看一下加密后的结果：

  ![image-20200917094718642](C:\Users\安伟超\AppData\Roaming\Typora\typora-user-images\image-20200917094718642.png)

  加密后的结果为：encText: "eHhjXckqrtZkqcwCalCMx0QuU6Lj9L7Wxouw1iMCnB4="

  接下来使用官方API模拟AES加密过程：

  ```python
      def AESEncrypt(self, clear_text, key):
          """
                  AES加密, 对应函数b
                  :param clear_text: 需要加密的数据
                  :return:
                  """
          # 数据填充
          clear_text = pad(data_to_pad=clear_text.encode(), block_size=AES.block_size)
          key = key.encode()
          iv = self.iv.encode()
          aes = AES.new(key=key, mode=AES.MODE_CBC, iv=iv)
          cipher_text = aes.encrypt(plaintext=clear_text)
          # 字节串转为字符串
          cipher_texts = base64.b64encode(cipher_text).decode()
          return cipher_texts
  
  ```

  接下来将需要加密的数据"{"csrf_token":""}"传入函数内执行以下看一下结果：

  ```python
      def resultEncrypt(self, input_text):
          """
          对应函数d
          :param input_text:
          :return:
          """
          i = self.create16RandomBytes()
          encText = self.AESEncrypt(input_text, self.nonce)
          print(encText)
  
  
  res = EncryptText().resultEncrypt('{"csrf_token":""}')
  print(res)
  
  
  (venv) F:\老安课程串讲资料\文档、代码杂七八\BarranziLessonSource\PythonSpider\Spider_Code>python test_demo.py
  eHhjXckqrtZkqcwCalCMx0QuU6Lj9L7Wxouw1iMCnB4=
  
  ```

  ok,经测试，第一次AES加密的结果一致。现在需要再进行一次AES加密，因为第二次加密用到了函数a产生的16位随机字符，为了结果一致，这里也使用相同的随机字符进行模拟。先看一下原始的结果：

  ![image-20200917095030124](C:\Users\安伟超\AppData\Roaming\Typora\typora-user-images\image-20200917095030124.png)

  ```python
  原始结果中，函数a生成的16位随机字符为："PUhuBzfd3SqIAm3E";
  对应得到的二次AES加密结果为："Pwwk1G7XhSncBmQ/zLfmvamgwsqk2JuBffIKCIANqsPx8DauU2ZLGKVOHteSUIjb"
  
  将该随机字符传给我们自己的加密方法，进行二次加密后得到的结果：
  
          encText = self.AESEncrypt(input_text, self.nonce)
          encText = self.AESEncrypt(encText, "PUhuBzfd3SqIAm3E")
          
          print(encText)
  
  
  res = EncryptText().resultEncrypt('{"csrf_token":""}')
  print(res)
  
  (venv) F:\老安课程串讲资料\文档、代码杂七八\BarranziLessonSource\PythonSpider\Spider_Code>python test_demo.py
  Pwwk1G7XhSncBmQ/zLfmvamgwsqk2JuBffIKCIANqsPx8DauU2ZLGKVOHteSUIjb
  
  ```

  结果比对：一致。

  接下来模拟RSA加密。先看原始函数c返回的结果：

  ![image-20200917095717396](C:\Users\安伟超\AppData\Roaming\Typora\typora-user-images\image-20200917095717396.png)

  比较长的一串加密字符，长度为256：

  ```python
  "0431d4e75cb6184434486e7857404419d9def54b838cc843f0916d100acc7cfbca08e7e3985741642fa18b2711709ece133f44e543de0a57b7ec912931b55671f24c650aac50cd58e5bff70be14a1feac2eb1dcc792b05ead1d93216b0a0434ff85d242ab484099a0df6000a960380b0d292a390750cdc2e7c304cf7d210fcd2"
  ```

  模拟RSA加密算法：

  ```python
      def RSAEncrypt(self, i, e, n):
          """
          RSA加密, 对应函数c
          :param i:
          :return:
          """
          # num = pow(x, y) % z
          # 加密C=M^e mod n
          num = pow(int(i[::-1].encode().hex(), 16), int(e, 16), int(n, 16))
          result = format(num, 'x')
          return result
  
  ```

  调用执行：

  ```python
      def resultEncrypt(self, input_text):
          """
          对应函数d
          :param input_text:
          :return:
          """
          # i = self.create16RandomBytes()
          encText = self.AESEncrypt(input_text, self.nonce)
          encText = self.AESEncrypt(encText, "PUhuBzfd3SqIAm3E")
          encSecKey = self.RSAEncrypt("PUhuBzfd3SqIAm3E", self.public_key, self.modulus)
          # from_data = {
          #     'params': encText,
          #     'encSecKey': encSecKey
          # }
          # return from_data
          print(len(encSecKey))
          print(encSecKey)
          # print(encText)
  
  
  res = EncryptText().resultEncrypt('{"csrf_token":""}')
  
  对应的返回结果：
  (venv) F:\老安课程串讲资料\文档、代码杂七八\BarranziLessonSource\PythonSpider\Spider_Code>python test_demo.py
  256
  0431d4e75cb6184434486e7857404419d9def54b838cc843f0916d100acc7cfbca08e7e3985741642fa18b2711709ece133f44e543de0a57b7ec912931b55671f24c650aac50cd58e5bff70be14a1feac
  2eb1dcc792b05ead1d93216b0a0434ff85d242ab484099a0df6000a960380b0d292a390750cdc2e7c304cf7d210fcd2
  
  结果比对：一致。
  
  至此，完整的加密流程我们模拟完了，各步骤测试结果基本正确。但是，问题在于，我们模拟出来的encText，也就是对应的parmas参数长度不够。
  
  经过上述步骤测试，能够证明加密算法是没有错的，因为已经完全比对模拟正确，而所需的四个d,e,f,g参数后面三个值又是固定的，那么问题基本就能确定出在了参数d上。
  
  我们继续debug，即继续单步调试，每执行一行语句，注意观察右侧local区域参数d的值得变化：
  ```

  ![image-20200917101120790](C:\Users\安伟超\AppData\Roaming\Typora\typora-user-images\image-20200917101120790.png)

  ```python
  将其进行两次AES加密：
      def resultEncrypt(self, input_text):
          """
          对应函数d
          :param input_text:
          :return:
          """
          # i = self.create16RandomBytes()
          encText = self.AESEncrypt(input_text, self.nonce)
          encText = self.AESEncrypt(encText, "PUhuBzfd3SqIAm3E")
          # encSecKey = self.RSAEncrypt("PUhuBzfd3SqIAm3E", self.public_key, self.modulus)
          # from_data = {
          #     'params': encText,
          #     'encSecKey': encSecKey
          # }
          # return from_data
          # print(len(encSecKey))
          # print(encSecKey)
          print(encText)
          print(len(encText))
  
  
  res = EncryptText().resultEncrypt('{"platform":"web","product":"cloudmusic","csrf_token":""}')
  
  返回的结果：
  (venv) F:\老安课程串讲资料\文档、代码杂七八\BarranziLessonSource\PythonSpider\Spider_Code>python test_demo.py
  M/r2wqVd21JsrSfoIv6GOHydw/KrCYdhQuax5/AjbI+217Ha9yaPxmbZf5qHBc5SitEk+RQigCad34CiU785Ufo/KvwW7E53HNnOOeviEpdQrdXFlgyJftgMnCUb4Gsk
  128
  
  长度为128，还是不够。
  继续debug，继续观察参数d的值：
  ```

  ![2020091416160816](C:\Users\安伟超\Desktop\桌面文件\2020091416160816.png)

  ```python
  此时d参数的值又发生了变化：
  d: "{"ids":"[1456238192]","level":"standard","encodeType":"aac","csrf_token":""}"
      
  我们将其再次传入上文二次AES加密测试：
  (venv) F:\老安课程串讲资料\文档、代码杂七八\BarranziLessonSource\PythonSpider\Spider_Code>python test_demo.py
  gFlGGE+7IPN1JYVMCKxXY2glNqlWGe6UnlW7nIX+9/RVczETQDFEch3izlQoRx34pALS8dlxkx60ZASaWNveTqmwOS72E5pgxctEW75uJV5reSDS4ZgnTMb4DBPXfIxUri0hxUxbt5DH78Alll3kDQ==
  152
  
  长度终于达到152了...看来这个就是d的真正值了。
  
  至此，模拟加密完成，我们将加密算法封装在单独的一个功能类内部，使用时只需要传入所需加密的字符串，即可返回我们所需的两个参数。
  
  虽然加密算法模拟完成了，但是注意观察最终d参数的值。d为字典，第一个值为ids，此id值即为某一首歌的id值。但每首歌都单独对应一个id值，如何获取这些id值成为我们需要解决的在请求最终数据之前的最后一个问题。
  ```

- 获取歌曲id

  ```python
  上文我们分析完parmas参数的加密算法，并采用Python模拟实现了加密算法，且算法经测试是正确的。
  
  接下来我们获取歌曲id。
  
  进入网易云官网，搜索框随便搜索歌曲或歌手名称：
  ```

  ![image-20200917112944961](C:\Users\安伟超\AppData\Roaming\Typora\typora-user-images\image-20200917112944961.png)

  ```python
  很明显，仍然是通过AJAX异步加载的数据包，找到该数据包，预览其响应数据，其中就包含我们所需的每一首歌的id。
  但该数据是没办法直接请求页面去获取的，所以还是老套路，分析该XHR数据包的URL及其请求方式，发现仍然为POST请求，则继续下拉查看form_data:
  ```

  ![image-20200917113321628](C:\Users\安伟超\AppData\Roaming\Typora\typora-user-images\image-20200917113321628.png)

  ```python
  oh shit,又是加密算法...
  
  先确定URL：https://music.163.com/weapi/cloudsearch/get/web?csrf_token=
  请求方式:POST
  
  查看下parmas参数值：zdFAiMHzLTcMN52lR1y47FK1nPSMXTCCq0T5zJr37+a2oRr2dCvxODhDkqALLsL8bLH4/SPYr/UE7xp+fFgqXtAvrw0iSspbEz2nVNBGpRrWsoL1drsVCyTyiLzn4SzyXMD2FTh1QjyhjEo450qELcCKbGG9I/XC/ZjZt2HXAZ+EFQCM8gg4uno8mgXDsNL8VVGJmcxxrpoFXjUQCXzEzsSMgWOeXASyMBQ9axA6l46nAvee7Jiq3n+y/zgbSLHTuJEmlxXFgVGDmjJqH7CSHw==
  
  其长度：280
  
  而encSecKey参数:
  30b011bbb1a9d55da964bae8c27840c4ab3d5d82163e544f2f0be9f6fe09536fe5bef35209f55c37b9e1da225ecf06b270753f17a5c3bf8f36b709f4ddfe7c24043a45e548f0a628001e3bf2cd0d13eaada1aa67c680abea53bc080201d47d934f335fa3161cb708967864aa450af53e2f7c271e81e7af844e03568cd326be60
  长度值仍然为256，不变。
  
  所以，又是这个d参数变了...
  继续老套路，定位到该参数，找到其加密算法，打断点，单步调试，观察右侧local数据变化，确定最终的d参数值：
  
  ```

  ![image-20200917115157563](C:\Users\安伟超\AppData\Roaming\Typora\typora-user-images\image-20200917115157563.png)

  ```python
  确定的最终d参数：
  d:{"hlpretag":"<span class=\"s-fc7\">","hlposttag":"</span>","s":"赵雷","type":"1","offset":"0","total":"true","limit":"30","csrf_token":""}
     
  使用加密算法加密后查看结果：
  
  F:/老安课程串讲资料/文档、代码杂七八/BarranziLessonSource/PythonSpider/Spider_Code/demo15_Music163_vip_download_OOP.py
  sZegqf/ji6goy5hJmlxWR25R2V4EmJr5zNOLf07Sq8i0hsFxhii8txE6DIMmGsh5OK/RcDubgb4WM6zeiJMmQW+NM+cWMSUulxVV1wWdcvh6cSmlCNXEXd+UlFxRwQaTOyDAIwM7dTkkOtnyC9MoSWxVWOeWGIhQq6F18ikECDUUI33BE7Gvm24FelMr/oj4rFsoNWJjyyji2GJwpCNlTbIXXgKrlbNONu9Nn5xlcjqu/Cyz4DAlXkfJkVzNZAmfYkwT4Xjp1Q05fL3F9atA/w==
  280
  6df91b702830d4b567a64491c66eed04e5d128f73e37be4eedfad9c81fde8f48150b134ecc53e3039384abbd4a8fcacdc57634e302e8c3bcbfa1c3565447a17ad57edb4bfbad79f00d48a8be1d5d7ca94ca6c49e9c97c0157c3341f65faec9c2155a658114fae09dfdfc750005e244b23afb3c21453c993674aea67f0e1183c8
  256
  
  Process finished with exit code 0
  
  对于参数d中各参数解读：
  s:你要搜索的内容。也就是说，你需要搜索的内容只需要自己定义就好，也就是代码层面可以使用input()来输入
  type:表示搜索的类型。经过测试，网易云对多种搜索内容进行了分类：
  ```

  | type | 含义     |
  | ---- | -------- |
  | 1    | 单曲     |
  | 100  | 歌手     |
  | 10   | 专辑     |
  | 1014 | 视频     |
  | 1006 | 歌词     |
  | 1000 | 歌单     |
  | 1009 | 主播电台 |
  | 1002 | 用户     |

  ```python
  处理完参数加密，我们就可以请求该URL获得响应，响应的内容为json格式数据，其中就包含所需的歌曲id。
  
  至此，有关的所有编码前的分析已到位，接下来是编码。
  ```

  ```python
  编码实现：
  
  
  
  # -*- coding:utf-8 _*-
  """
  @version:
  author:安伟超
  @time: 2020/09/16
  @file: demo15_Music163_vip_download_OOP.py.py
  @environment:virtualenv
  @email:awc19930818@outlook.com
  @github:https://github.com/La0bALanG
  @requirement:抓取网易云音乐任意付费音乐，下载到本地保存
  """
  
  import requests
  import random
  import base64
  import json
  import os
  from Crypto.Cipher import AES, PKCS1_OAEP
  from Crypto.Util.Padding import pad
  from Crypto.PublicKey import RSA
  from Crypto.Random import get_random_bytes
  from fake_useragent import UserAgent
  
  
  
  """
  
  实现思路
  
  1.目标：
      1.输入任意歌手或歌曲名称，列出所有查询结果；
      2.自行选择其中想要的结果下载至本地
      3.搜索结果包含可能的vip付费歌曲，也要实现下载功能
  
  2.需求实现所需突破的难点：
      1.网易云歌曲播放的XHR异步加载数据包其URL请求参数form_data的加密破解；
      2.具体每一首歌曲的歌曲id(网易云每一首歌都有一个单独的歌曲id，获取该id，用于构造上述加密破解)
      
  3.请求、参数及其加密分析
      1.歌曲文件请求
          请求接口(URL):https://music.163.com/weapi/song/enhance/player/url/v1?csrf_token=
          请求方式：POST
          请求参数：parmas和encSecKey
          参数加密：AES及RSA加密算法
          具体实现：详见加密算法实现及其注解
      2.歌曲id请求：
          请求接口：https://music.163.com/weapi/cloudsearch/get/web?csrf_token=
          请求方式:POST
          请求参数：parmas和encSecKey
          参数加密：AES及RSA加密算法
          具体实现：详见加密算法实现及其注解
  
  附经过js逆向分析后的js加密算法代码：
  
  var bVZ7S = window.asrsea(JSON.stringify(i9b), bqN9E(["流泪", "强"]), bqN9E(Wx4B.md), bqN9E(["爱心", "女孩", "惊恐", "大笑"]));
              e9f.data = j9a.cs0x({
                  params: bVZ7S.encText,
                  encSecKey: bVZ7S.encSecKey
              })
  
  
  
  !function() {
      function a(a) {
          var d, e, b = "abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789", c = "";
          for (d = 0; a > d; d += 1)
              e = Math.random() * b.length,
              e = Math.floor(e),
              c += b.charAt(e);
          return c
      }
      function b(a, b) {
          var c = CryptoJS.enc.Utf8.parse(b)
            , d = CryptoJS.enc.Utf8.parse("0102030405060708")
            , e = CryptoJS.enc.Utf8.parse(a)
            , f = CryptoJS.AES.encrypt(e, c, {
              iv: d,
              mode: CryptoJS.mode.CBC
          });
          return f.toString()
      }
      function c(a, b, c) {
          var d, e;
          return setMaxDigits(131),
          d = new RSAKeyPair(b,"",c),
          e = encryptedString(d, a)
      }
      function d(d, e, f, g) {
          var h = {}
            , i = a(16);
          return h.encText = b(d, g),
          h.encText = b(h.encText, i),
          h.encSecKey = c(i, e, f),
          h
      }
      function e(a, b, d, e) {
          var f = {};
          return f.encText = c(a + e, b, d),
          f
      }
      window.asrsea = d,
      window.ecnonasr = e
  }();
  
  4.实现步骤：
      1.调用加密算法类模拟js加密过程将parmas及encSecKey完成加密并放入form_data格式返回。其中留下接口：参数d，用于请求歌曲id和请求歌曲文件时的不同传参。
      2.请求歌曲id
      3.请求歌曲文件
      4.下载保存至本地
  
  
  测试数据：一次XHR接口请求的response:
  
  {
    "data": [
      {
        "id": 1356499052,
        "url": "http://m10.music.126.net/20200917152750/c6a5d97c3aa529eeb5f08237fae3f412/ymusic/030f/0659/0652/4eeba3ec67139de17412186b850c3a70.mp3",
        "br": 128000,
        "size": 3971074,
        "md5": "4eeba3ec67139de17412186b850c3a70",
        "code": 200,
        "expi": 1200,
        "type": "mp3",
        "gain": 0.0,
        "fee": 8,
        "uf": null,
        "payed": 0,
        "flag": 64,
        "canExtend": false,
        "freeTrialInfo": null,
        "level": "standard",
        "encodeType": "mp3"
      }
    ],
    "code": 200
  }
  
  
  
  
  """
  
  
  
  class EncryptAlgorithm(object):
      """
      加密算法类:处理form_data所需的parmas及encSecKey参数的加密
      :return:form_data
  
      """
  
      def __init__(self):
  
          #固定字符库，用于从中随机抽取字符完成加密
          self.__init_str = 'abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789'
          self.__init_num = '0102030405060708'
  
          #模拟参数d所需的三个固定参数
          #模拟参数e
          self.__e = '010001'
  
          #模拟参数f
          self.__f = '00e0b509f6259df8642dbc35662901477df22677ec152b' \
                         '5ff68ace615bb7b725152b3ab17a876aea8a5aa76d2e417' \
                         '629ec4ee341f56135fccf695280104e0312ecbda92557c93' \
                         '870114af6c9d05c4f7f0c3685b7a46bee255932575cce10b' \
                         '424d813cfe4875d3e82047b97ddef52741d546b8e289dc69' \
                         '35b3ece0462db0a22b8e7'
  
          #模拟参数g
          self.__g = '0CoJUm6Qyw8W8jud'
  
      def __make16randomstr(self):
          """
          # 产生16位随机字符, 对应函数a
          :return:
          """
          # generated_string = get_random_bytes(16)
          # return generated_string
  
          generate_string = random.sample(self.__init_str, 16)
          generated_string = ''.join(generate_string)
          return generated_string
  
      def __AES_encrypt_alogorithm(self, clear_text, key):
          """
                  AES加密, 对应函数b
                  :param clear_text: 需要加密的数据
                  :return:
                  """
          # 数据填充:传入的所需加密数据进行填充处理并重写clear_text变量
  
          clear_text = pad(data_to_pad=clear_text.encode(), block_size=AES.block_size)
          key = key.encode()
          iv = self.__init_num.encode()
          aes = AES.new(key=key, mode=AES.MODE_CBC, iv=iv)
          cipher_text = aes.encrypt(plaintext=clear_text)
          # 字节串转为字符串
          cipher_texts = base64.b64encode(cipher_text).decode()
          return cipher_texts
  
      def __RSA_encrypt_alogorithm(self, i, e, n):
          """
          RSA加密, 对应函数c
          :param i:
          :return:
          """
          # num = pow(x, y) % z
          # 加密C=M^e mod n
          num = pow(int(i[::-1].encode().hex(), 16), int(e, 16), int(n, 16))
          result = format(num, 'x')
          return result
  
      def __get_encrypt_result(self, input_text):
          """
          对应函数d
          :param input_text:
          :return:
          """
          i = self.__make16randomstr()
          # print(i) #输出一个生成的16位随机字符串
  
          encText = self.__AES_encrypt_alogorithm(input_text, self.__g)
          encText = self.__AES_encrypt_alogorithm(encText, i)
          encSecKey = self.__RSA_encrypt_alogorithm(i, self.__e, self.__f)
          from_data = {
              'params': encText,
              'encSecKey': '0' + encSecKey
          }
          # print(encText) #输出encText加密结果
          # print(len(encText)) #返回其长度，验证是否正确
          # print(encSecKey) #输出encSecKey加密结果
          # print(len(encSecKey)) #验证其长度是否正确
          return from_data
  
      def return_form_data(self,input_text):
          return self.__get_encrypt_result(input_text)
  
  
  # res = EncryptAlgorithm().display('{"ids":"[1456238192]","level":"standard","encodeType":"aac","csrf_token":""}')
  # print(res)
  #
  
  
  class CrackMusic163VipMusicSpider(object):
      '''
      爬虫请求类：负责请求所需数据
      :return:response
  
      '''
  
      def __init__(self):
  
          self.__headers = {
              'User-Agent':UserAgent().random
          }
  
      #请求数据(响应内容)
      def get_html(self,url,method = 'GET',form_data = None):
          try:
              if method == 'GET':
                  response = requests.get(url=url,headers = self.__headers)
              else:
                  response = requests.post(url=url,data=form_data,headers=self.__headers)
              response.raise_for_status()
              response.encoding = 'utf-8'
              return response.text
          except Exception as err:
              print(err)
              return '请求异常'
  
      def parse_text(self,text):
          #1.将得到response(json格式数据)转为Python字典
          ids_list = json.loads(text)['result']['songs']
          info_list = []
          for id_info in ids_list:
              song_name = id_info['name']
              id = id_info['id']
              singer = id_info['ar'][0]['name']
              info_list.append([id,song_name,singer])
          return info_list
  
      def save_music(self,music_url,id_info):
          dir = 'D:\musicSpider'
          if not os.path.exists(dir):
              os.mkdir(dir)
          filename = id_info[1] + '-' + id_info[2]
          response = requests.get(music_url,headers=self.__headers)
          with open(os.path.join(dir,filename) + '.mp3','wb') as f:
              f.write(response.content)
              print('下载完毕！')
  
  
  
  
  
  def test():
      #创建加密工厂
      ea = EncryptAlgorithm()
      #创建爬虫工厂
      crack_spider = CrackMusic163VipMusicSpider()
  
      #接口URL
      song_url = 'https://music.163.com/weapi/song/enhance/player/url/v1?csrf_token='
      id_url = 'https://music.163.com/weapi/cloudsearch/get/web?csrf_token='
  
      #获取歌曲id的加密模拟所需的d参数
      id_d = {
          "hlpretag": "<span class=\"s-fc7\">",
          "hlposttag": "</span>",
          "s": input("请输入歌名或歌手: "),
          "type": "1",
          "offset": "0",
          "total": "true",
          "limit": "30",
          "csrf_token": ""
      }
      #根据id的d参数构造加密后的form_data
      id_form_data = ea.return_form_data(json.dumps(id_d))
      #发请求获取歌曲id响应
      id_text = crack_spider.get_html(id_url,method='POST',form_data=id_form_data)
  
      #解析相应内容，摘出歌曲id，歌名，歌手名
      id_infos = crack_spider.parse_text(id_text)
      music_info = []
  
      #多条记录，for循环遍历依次取出歌曲id
      for id_info in id_infos:
          #请求歌曲的加密模拟所需的d参数
          music_d = {
              #ids根据上一步摘出的id值获取
              "ids": str(id_info[0]),
              "level": "standard",
              "encodeType": "aac",
              "csrf_token": ""
          }
          #根据歌曲的d参数构造加密后的form_data
          music_form_data = ea.return_form_data(json.dumps(music_d))
          #发请求获取歌曲响应
          music_reps = crack_spider.get_html(song_url,method='POST',form_data=music_form_data)
          #解析出响应内容中的歌曲下载的URL，再加上歌曲名称，一同作为参数穿给保存文件方法
          crack_spider.save_music(json.loads(music_reps)['data'][0]['url'],id_info[1])
      print(music_info)
  
      # 无关测试
  # print(type(id_text))
      # print(res)
      # print(type(res))
      # music_d = {
      #     "ids": "[1334327077]",
      #     "level": "standard",
      #     "encodeType": "aac",
      #     "csrf_token": ""
      # }
      # music_form_data = ea.display(json.dumps(music_d))
      # music_reps = crack_spider.display(song_url,method='POST',form_data=music_form_data)
      # print(music_reps)
      # print(type(music_reps))
  
  if __name__ == '__main__':
      test()
  ```


# 