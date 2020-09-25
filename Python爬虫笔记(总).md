# **Python爬虫笔记**

作者：**Barranzi_**
个人github主页：**[github]**(https://github.com/La0bALanG)
个人邮箱：awc19930818@outlook.com

**新时代的铁饭碗：一辈子不管走到哪里都有饭吃(还能吃上热乎的)。**
**希望我能把你感染，成为下一个技术狂人！**

**本文所有代码、案例测试环境：1.Linux -- 系统版本：Ubuntu20.04 LTS   2.windows -- 系统版本：WIN10 64位家庭版**





-------





[TOC]



# 爬虫环境搭建

## Anaconda3安装及配置

- **Anaconda3下载**
  下载地址： [Anaconda3](https://mirrors.tuna.tsinghua.edu.cn/anaconda/archive/).
  Linux版选择：**Anaconda3-5.3.1-Linux-x86_64.sh**

- **Anaconda3安装**
  终端下运行：**bash Anaconda3-5.3.1-Linux-x86_64.sh**
  安装过程一路傻瓜式**回车** or **yes**
  *注意*：安装Anaconda3结束前会提示你是否安装**Microsoft Visual studio Code**，此处根据个人喜好选择性安装即可。

- **本地Python环境配置**
  安装完成后进行测试，启动终端，输入**python3**，回车，查看本机python环境，如下：
  ![在这里插入图片描述](https://img-blog.csdnimg.cn/20200507150149981.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2F3YzE5OTMwODE4,size_16,color_FFFFFF,t_70)
  显示仍然使用的是Ubuntu自带Python环境，所以需要进行一下手动配置。
  启动终端，使用vim编辑器打开根目录下配置文件.bashrc，命令如下：
  **sudo vim ~/.bashrc**
  ![在这里插入图片描述](https://img-blog.csdnimg.cn/20200507150054835.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2F3YzE5OTMwODE4,size_16,color_FFFFFF,t_70)
  在文末添加一行代码如下：
  **export PATH="==/home/anwc/anaconda3==/bin:$PATH"**（标记部分为你的**本机Anaconda路径**）	

  最后在终端输入：**source ~/.bashrc**，运行一下即可。


## Chrome浏览器插件安装及配置

*注意*：Chrome浏览器插件需要**FQ**上Google进行下载安装，自行解决**FQ**后继续：
进入Chrome应用商店，依次搜索Proxy-Switch0mega、JSONView、XPath Helper进行安装，安装后即可在开发者工具里看到这三个插件，如图：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200507152230549.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2F3YzE5OTMwODE4,size_16,color_FFFFFF,t_70)
下面简单说下**Proxy-Switch0mega的安装及配置**：

1. 点击浏览器右上角插件图标：
   <img src="https://img-blog.csdnimg.cn/20200507152408540.png" alt="在这里插入图片描述" style="zoom: 33%;" />
   点击选项；
2. 进入后看到如下界面：
   ![在这里插入图片描述](https://img-blog.csdnimg.cn/20200507152512775.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2F3YzE5OTMwODE4,size_16,color_FFFFFF,t_70)
   选择左下角的新建情景模式，进入后如图：
   ![在这里插入图片描述](https://img-blog.csdnimg.cn/2020050715261614.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2F3YzE5OTMwODE4,size_16,color_FFFFFF,t_70)
   情景名称随意，输入后点击创建，如图：
   ![在这里插入图片描述](https://img-blog.csdnimg.cn/20200507152829799.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2F3YzE5OTMwODE4,size_16,color_FFFFFF,t_70)
   至此，基本配置完成。



## Fiddler安装及证书配置

Linux下不能直接使用fiddler，需要先安装mono-conplete
终端输入命令：**sudo apt-get install mono-complete**，如下（测试本机已安装，故不运行仅展示）：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200507154932927.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2F3YzE5OTMwODE4,size_16,color_FFFFFF,t_70)

安装大约需要几分钟；
安装完毕后，点击下方链接下载fiddler Linux版，此为zip压缩包；
**Linux版fiddler下载地址**：
链接: [link](https://pan.baidu.com/s/1VGoNvZ8vfecvr77X36StQQ).
提取码：ov99
下载完毕后解压，终端进入该目录：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200507155112666.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2F3YzE5OTMwODE4,size_16,color_FFFFFF,t_70)
找到**Fiddler.exe**，输入命令：**mono Fiddler.exe**,即可打开熟悉的fiddler主界面：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200507155305254.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2F3YzE5OTMwODE4,size_16,color_FFFFFF,t_70)

接下来需要对fiddler进行一些简单的基本配置；
点击导航栏 **tools**，选择**options**：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200507155409684.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2F3YzE5OTMwODE4,size_16,color_FFFFFF,t_70)
看到**HTTPS**以及**Connections**选项卡：
**HTTPS**选项卡内：
将**Decrypt HTTPS traffic**打钩，下面的选项选择**from browsers only**；
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200507155457167.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2F3YzE5OTMwODE4,size_16,color_FFFFFF,t_70)
**Connections**选项卡内：
将**fiddler listens on port**改为8888（与**Switch0mega**插件中新建的情景模式下**端口号**保持一致即可）；
![在这里插入图片描述](https://img-blog.csdnimg.cn/2020050715571936.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2F3YzE5OTMwODE4,size_16,color_FFFFFF,t_70)
期间所有弹窗一律ok or yes，保存，关闭窗口即可。
**至此，fiddler基本配置完成。**

# 开发环境搭建

## MySQL安装及配置

Linux下MySQL5.7诟病百出，已经不建议使用，那么如何在Linux下安装MySQL8.0呢？

- **将MySQL APT存储库添加到系统的软件存储库列表中**
  进入[MySQL官网](https://dev.mysql.com/downloads/repo/apt/)查看版本号：
  ![在这里插入图片描述](https://img-blog.csdnimg.cn/20200507162702783.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2F3YzE5OTMwODE4,size_16,color_FFFFFF,t_70)
  图片中红框标识出来的就是最新版本号，复制此版本号；
  使用**wget**进行下载：

  ~~~
  wget https://dev.mysql.com/get/mysql-apt-config_0.8.15-1_all.deb
  ~~~

  将下载好的文件使用**dpkg**命令进行安装：

  ~~~
  sudo dpkg -i mysql-apt-config_0.8.15-1_all.deb
  ~~~

  中间弹窗直接点击OK；
  然后更新一下存储库信息：

  ~~~
  sudo apt-get update
  ~~~




- **使用APT安装MySQL**
  （*注意*：如果不执行以上步骤直接进行APT安装，则安装的是MySQL5.7版本）
  命令：

  ~~~
  sudo apt-get install mysql-server
  ~~~

  其中两个弹窗:

  第一个是确认密码（这一步一定要设置数据库密码）

  另一个是选择加密方式，工具较新选第一个，较老选第二个

- **开放远程访问**
  为了方便后期使用可视化图形界面操作数据库，这里需要开放一下远程访问权限。
  1.连接到数据库；

  ~~~
  mysql -uroot -p
  ~~~

  输入密码进入；
  2.查看数据库中mysql表；

  ~~~
  show databases;
  ~~~

  3.选择当前使用数据库为mysql；

  ~~~
  use mysql;
  ~~~

  4.查看权限：

  ~~~
  select host, user, authentication_string, plugin from user;
  ~~~

  5.更改加密方式（******为你自己设置的密码）：

  ~~~
  ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY '******';
  ~~~

  6.开放远程访问权限（授权远程连接）：

  ~~~
  ALTER USER 'root'@'%' IDENTIFIED BY '123456' PASSWORD EXPIRE NEVER;
  
  GRANT ALL PRIVILEGES ON *.* TO 'root'@'%' WITH GRANT OPTION;
  
  ALTER USER 'root'@'%' IDENTIFIED WITH mysql_native_password BY '123456';
  ~~~

  7.刷新权限：

  ~~~
  flush privileges;
  ~~~

## MongoDB安装及配置

首先检查一下本机是否安装MongoDB：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200507165848927.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2F3YzE5OTMwODE4,size_16,color_FFFFFF,t_70)
确认未安装，执行**APT**命令进行安装MongoDB：

~~~
sudo apt-get install mongodb
~~~

如下图：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200507170104699.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2F3YzE5OTMwODE4,size_16,color_FFFFFF,t_70)
安装完毕后简单测试一下：
输入命令：

~~~
mongo
mongod
~~~

出现下图所示：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200507170247711.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2F3YzE5OTMwODE4,size_16,color_FFFFFF,t_70)
已经能够正常进入MongoDB界面，安装成功。

## Redis安装及配置

使用**APT**命令安装Redis数据库：

~~~
sudo apt-get install redis-server
~~~

安装完毕后测试：

~~~
redis-cli
~~~

至此安装成功。
接下来对redis进行基本配置：
进入 /etc/redis 下的redis.conf配置文件：

~~~
sudo vi /etc/redis/redis.conf
~~~

如下图所示：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200507171000652.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2F3YzE5OTMwODE4,size_16,color_FFFFFF,t_70)
找到**bind 127.0.0.1**,将其注释掉即可；
继续下拉，找到**requirepass foobared**,如图：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200507171128647.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2F3YzE5OTMwODE4,size_16,color_FFFFFF,t_70)
这里就是设置redis的连接密码，将其解除注释，并修改**foobared**为任意自己想要设置的密码即可；
修改完毕后，输入：

~~~
:wq
~~~

保存，关闭窗口，然后输入：

~~~
sudo service redis restart
~~~

重启一下redis服务即可。
在设置完毕redis连接密码后，如果仍然以无密码状态登录，当你做任何操作时，会提示你没有权限，此时只需要退出redis再重新进入：

~~~
redis-cli -a yourpassword
~~~

即可恢复正常使用，如下图：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200507171707858.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2F3YzE5OTMwODE4,size_16,color_FFFFFF,t_70)

# Python爬虫常用库的安装及配置

Python爬虫常用库有很多，在这里只介绍几个比较常见的库的安装。

## pip包管理工具安装

Linux下常用的Python库大部分都是通过pip3包管理工具进行安装的，所以在安装这些库之前，我们先安装pip3：

~~~
sudo apt-get install python3-pip
~~~

测试本机已安装，故不作图片演示；
安装完毕之后查看下版本号：

~~~
pip3 --version
~~~

确认为pip3即可：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200507172130584.png)
爬虫常用库的安装：

~~~
pip3 install requests selenium beautifulsoup4 pyquery pymongo redis flask django jupyter
~~~

其实诸如redis等我们之前已经安装过了，jupyter也已经在安装Anaconda3的时候自动安装好了。

## 其他常用Python库安装

### **pymysql**

~~~
pip3 install pymysql
~~~

### **lxml**

~~~
sudo pip3 install lxml
~~~

### **scrapy**

首先安装依赖，依次执行以下命令安装所需依赖库：

~~~
sudo apt-get install python-dev
sudo apt-get install build-essential
sudo apt-get install libxml2-dev
sudo apt-get install libxslt1-dev
sudo apt-get install python-setuptools
~~~

如图所示：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200508101103512.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2F3YzE5OTMwODE4,size_16,color_FFFFFF,t_70)
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200508101207149.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2F3YzE5OTMwODE4,size_16,color_FFFFFF,t_70)
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200508101234999.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2F3YzE5OTMwODE4,size_16,color_FFFFFF,t_70)
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200508101306961.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2F3YzE5OTMwODE4,size_16,color_FFFFFF,t_70)
然后再安装scrapy：

~~~
pip3 install Scrapy
~~~

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200508103216573.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2F3YzE5OTMwODE4,size_16,color_FFFFFF,t_70)
验证是否安装成功：终端输入命令：

~~~
scrapy
~~~

如图：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200508103257217.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2F3YzE5OTMwODE4,size_16,color_FFFFFF,t_70)

### **BeautifulSoup4**

```python
pip3 install bs4 -i https://pypi.douban.com/simple
```

### **Selenium Webdriver**

```python
pip3 install selenium -i https://pypi.doubancom/simple
```

webdriver需要单独安装，具体下载流程：

- 官网寻找对应浏览器厂商及其具体版本的driver；
- 下载到本地后解压至浏览器安装所在路径即可。

# Chrome浏览器插件安装
## **安装方法**

```python
# 在线安装
1、下载插件 - google访问助手
2、安装插件 - google访问助手: 
  Chrome浏览器-设置-更多工具-扩展程序-开发者模式-拖拽(解压后的插件文件夹)
3、在线安装其他插件 - 打开google访问助手 - google应用商店 - 搜索插件 - 添加即可

# 离线安装
1、下载插件 - xxx.crx 重命名为 xxx.zip
2、输入地址: chrome://extensions/   打开- 开发者模式
3、拖拽 插件(或者解压后文件夹) 到浏览器中
4、重启浏览器，使插件生效
```

## **爬虫常用插件**

```python
1、google-access-helper : 谷歌访问助手,可访问 谷歌应用商店
2、Xpath Helper: 轻松获取HTML元素的xPath路径
   开启/关闭: Ctrl + Shift + x
3、JsonView: 格式化输出json格式数据
4、Proxy SwitchyOmega: Chrome浏览器中的代理管理扩展程序
```

# 爬虫基本概念
## 定义

```python	
网络蜘蛛、网络机器人，抓取网络数据的程序
其实就是用Python程序模仿人点击浏览器并访问网站，而且模仿的越像越好，让Web站点无法发现你不是人
```

## 使用爬虫的目的

```python
1、公司项目测试数据
2、公司业务部门及其他部门所需数据
3、数据分析
```

## 爬虫的特点

```python
1.爬虫只是一种技术的分支，主要面向网站，网页应用等的数据爬取，是众多数据获取途径中成本最低，效率最高的方式
2.爬虫工程师理论上归属软件开发工程师的一种
3.从技术层面来说，“万维网上一切数据皆可爬”，但实际应用过程中必须遵守国家相关法律法规，遵守各大企业机构制定的协议。
```

## 企业获取数据的方式

```python
1.公司自有数据
2.人工采集获取
3.第三方数据平台
4.爬虫爬取
```

## 使用Python做爬虫的优势

```python
1、Python ：请求模块、解析模块丰富成熟,强大的Scrapy网络爬虫框架
2、PHP ：对多线程、异步支持不太好
3、JAVA：代码笨重,代码量大
4、C/C++：虽然效率高,但是代码成型慢
```

## 爬虫分类

```python
根据使用场景，网络爬虫可分为通用爬虫和聚焦爬虫
    1、通用网络爬虫(搜索引擎使用,遵守robots协议)
    2、聚焦网络爬虫 ：自己写的爬虫程序
```

### 通用爬虫

#### 介绍

```python
通用网络爬虫是搜索引擎的关键组成部分，其主要目的是将互联网上的网页下载到本地，形成一个互联网内容的镜像或备份。
```

#### 通用搜索引擎(Search Engine)工作流程

```python
	通用网络爬虫主要工作就是从互联网中搜集网页，采集信息。这些被采集到的网页信息用于搜索引擎建立索引从而提供支持，它决定着整个引擎系统的内容是否丰富，信息是否即时，因此其性能的优劣直接影响着搜索引擎的效果。
	一般的，通用搜索引擎大致的工作步骤如下：
	1.抓取网页。
    	1.首先选取一部分的种子URL，将这些URL放入待抓取URL队列；
        2.取出待抓取的URL,解析DNS得到主机的IP,并将URL对应的网页下载下来，存储进已下载网页库中，并将这些URL放进已抓取URL队列；
        3.分析已抓取URL队列中的URL,分析其内部包含的其他URL，并且一并将URL放入待抓取的URL队列，继而实现下一个循环...
    搜索引擎如何获取一个新网站的URL：
    	1.新网站向搜索引擎主动提交网址。例如百度：https://ziyuan.baidu.com/linksubmit/url
        2.在其网站上设置新网站的外链(尽可能处理搜索引擎爬虫爬取的范围)
        3.搜索引擎和DNS解析服务商(比如DNSPod等)合作，新网站域名将被迅速抓取。
    robots协议：也叫作爬虫协议，机器人协议等，全称为“网络爬虫排除标准(Robots Exclusion Protocol)”,网站通过Robots协议告诉搜索引擎哪些页面可以抓取，哪些页面不能抓取。例如：
    	淘宝网：https://www.taobao.com/robots.txt
		腾讯网：http://www.qq.com/robots.txt
    2.数据存储
    搜索引擎通过爬虫爬取到的页面，将数据存入原始页面数据库。其中的页面数据与用户浏览器得到的HTML完全一致。
    搜索引擎蜘蛛在爬取页面时，也做一定的重复内容检测，一旦遇到访问权重很低的网站上有大量抄袭、采集或者复制的内容，很可能就不在运行。    
    3.预处理
    搜索引擎将爬虫抓取回来的页面，进行各种步骤的预处理。常见的预处理步骤如下：
    	1.提取文字
        2.中文分词
        3.消除噪音(比如版权声明，广告等)
        4.索引处理
        5.链接关系计算
        6.特殊文件处理
    4.提供检索，网站排名等具体实质服务。
    搜索引擎在对信息进行组织和处理后，为用户提供关键字检索服务，将用户检索相关的信息展示给用户。
    同时还会根据页面的PageRank值(链接的访问量排名)来进行网站排名，以及其他的各种可能提供的服务。
```

通用搜索引擎大致工作流程图示如下：

![image-20200915143522371](C:\Users\安伟超\AppData\Roaming\Typora\typora-user-images\image-20200915143522371.png)



### 聚焦爬虫

```python
聚焦爬虫是指面向特定需求的网络爬虫程序，其与通用搜索引擎爬虫的区别在于：聚焦爬虫在实施网页抓取时会对内容进行处理筛选，尽量保证之抓取与需求相关的网页信息。
```

## 爬虫固定套路（语义层面概括）

```python
1.分析页面
	1.分析网站URL规律，确定具体的URL
	2.分析网页结构，确定目标数据具体所在位置
		1.数据存在于响应的页面主体(最理想的位置，无需进行抓包分析)
		2.数据不在响应的页面主体：
			1.使用自带的浏览器控制台进行抓包分析，突破AJAX异步加载确定数据位置
			2.使用fiddler抓包分析
3.向网站发起请求获得响应数据
4.对响应得到的数据进行筛选(也叫做解析或提取)
	1.直接得到所需数据，清洗入库(通常称为持久化存储)
	2.页面中存在其他需要继续抓取的URL地址，重复第三步，如此循环
```

### 爬虫固定套路图示注解

![image-20200915143953116](C:\Users\安伟超\AppData\Roaming\Typora\typora-user-images\image-20200915143953116.png)

## HTTP/HTTPS协议
### HTTP协议简介
```python
概念：通信计算机双方必须共同遵守的一种约定，只有遵守这个约定，计算机之间才能进行通信。

HTTP协议是Hyper Text Transfer Protocol（超文本传输协议）的缩写，是一种发布和接受HTML页面的方法。

HTTPS （全称：Hyper Text Transfer Protocol over SecureSocket Layer），是以安全为目标的 HTTP 通道，在HTTP的基础上通过传输加密和身份认证保证了传输过程的安全性 。HTTPS 在HTTP 的基础下加入SSL 层，HTTPS 的安全基础是 SSL，因此加密的详细内容就需要 SSL。 HTTPS 存在不同于 HTTP 的默认端口及一个加密/身份验证层（在 HTTP与 TCP 之
间）。这个系统提供了身份验证与加密通讯方法。它被广泛用于万维网上安全敏感的通讯，例如交易支付等方面 。

HTTPS是加密之后的HTML，说白了就是安全版的HTML，其加入的SSL层保证了数据传输的安全性及可靠性。

SSL(Secure Sockets Layer安全套接层)主要用于web的安全传输协议，在传输层对网络连接进行加密，保证在internet上的数据传输安全。
```
### HTTP请求与响应

![image-20200915144942788](C:\Users\安伟超\AppData\Roaming\Typora\typora-user-images\image-20200915144942788.png)

```python
HTTP通信由两部分组成：
	1.客户端请求消息
    2.服务器响应消息

大致通信流程如下：

	1.当用户在浏览器的地址栏中输入一个URL并按下回车键后，浏览器会向HTTP服务器发送HTTP请求。HTTP常用的请求方式为get请求方法和post请求方法。
    
    2.当我们在浏览器输入URL：https://www.baidu.com的时候，浏览器发送一个request请求去获取该网站的html文件，服务器把response文件对象返回给浏览器
    
    3.浏览器分析response中的html，分析过程中发现其引用些许外部文件，如样式表，js文件，图片，音频，视频等，浏览器会自动再次发送request去获取对应的外部文件。
    
    4.当所有的文件都下载，加载完毕后，网页会根据html语法结构，完整的渲染出最终页面。
```
### 统一资源定位符：URL

```python
URL:统一资源定位符，用于完整的描述internet上网页和其他资源的地址的一种标识方法。
    
URL基本格式如下：

协议://主机:[端口号]/路径/?[请求or查询参数].../[#锚点]
    
    协议：scheme，指的就是HTTP或HTTPS
    主机：host，服务器的IP地址或域名
    端口号：port，服务器端口
    路径：path，访问资源的路径
    请求参数：query_string，发送给http服务器的数据
    查询参数：parmas，参数的一种常见形式
    auther：锚点，用于页面内跳转
```

### 请求内容

```python
1.请求行
	由请求方式+URL+协议版本组成
	例如：GET https://www.baidu.com/aaa/bbb/?aa=xx HTTP/1.1
        
2.请求头：客户端向服务器发送请求的补充说明，不可缺少。
	HOST：主机，即请求地址
    User-Agent：客户端使用的操作系统和浏览器的名称和版本
    Content-Length：发送给HTTP服务器数据的长度。
    Content-Type：参数的数据类型
    Cookie：发送给HTTP 服务器的cookie值
    Accept：浏览器接受的媒体类型
    Accept-Language：浏览器自己接收的语言
    Accept-Charset：自己接收的字符集
3.请求体
    一般携带的请求参数。只有当请求方式为POST时才有请求体，GET的请求体直接包含在了URL部分。

请求内容举例：

GET / HTTP/1.1
Host: www.baidu.com
Connection: keep-alive
Cache-Control: max-age=0
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHT
Sec-Fetch-Mode: navigate
Sec-Fetch-User: ?1
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,imag
Sec-Fetch-Site: same-origin
Referer: https://www.baidu.com/s?ie=utf-8&f=8&rsv_bp=1&rsv_idx=1&tn=baidu&wd=
Accept-Encoding: gzip, deflate, br
Accept-Language: zh-CN,zh;q=0.9
Cookie:BIDUPSID=4049831E3DB8DE890DFFCA6103FF02C1;
```

### 请求方法

| 序号 | 方法    | 描述                                                         |
| ---- | ------- | ------------------------------------------------------------ |
| 1    | GET     | 请求指定的页面信息，并返回实体主体                           |
| 2    | HEAD    | 类似于get请求，只不过返回的响应中没有具体的内容，用于获取请求头 |
| 3    | POST    | 向指定资源提交数据进行处理请求(例如提交表单或者上传文件)，数据被包含在请求体中。POST请求可能会导致新的资源建立或已有资源的修改 |
| 4    | PUT     | 从客户端向服务器传送的数据取代指定的文档内容                 |
| 5    | DELETE  | 请求服务器删除指定的页面                                     |
| 6    | CONNECT | HTTP/1.1协议中预留给能够将连接改为管道方式的代理服务器       |
| 7    | OPTIONS | 允许客户端查看服务器的性能                                   |
| 8    | TRACE   | 回显服务器收到的请求，主要用于测试                           |

### 响应内容

```python
1.响应行：由“HTTP 版本号 + 响应状态码 + 状态说明”组成。

例如：HTTP/1.1 200 OK

2.响应头：与请求头对应

3.响应体：这才是真正的响应数据，这些数据其实就是网页的HTML源码

响应内容举例：

HTTP/1.1 200 OK
Bdpagetype: 1
Bdqid: 0xdbeb11ea000cfef4
Cache-Control: private
Connection: keep-alive
Content-Encoding: gzip
Content-Type: text/html
Cxy_all: baidu+642857607c537ed21fa04bcfb54ff6ee
Date: Thu, 02 Jan 2020 06:32:55 GMT
Expires: Thu, 02 Jan 2020 06:32:51 GMT
Server: BWS/1.1
Set-Cookie: delPer=0; path=/; domain=.baidu.com
Set-Cookie: BDSVRTM=6; path=/
Set-Cookie: BD_HOME=0; path=/
Set-Cookie: H_PS_PSSID=1448_21096_30210_30283_30504; path=/; domain=.baidu.co
Strict-Transport-Security: max-age=172800
Traceid: 1577946775028760116215846779410554093300
Vary: Accept-Encoding
X-Ua-Compatible: IE=Edge,chrome=1
Transfer-Encoding: chunked
```

### 响应状态码

```python
响应状态码有 1XX、2XX、3XX、4XX、5XX、5XX。
    1XX 提示信息 - 表示请求已被成功接收，继续处理
    2XX 成功 - 表示请求已被成功接收，理解，接受
    3XX 重定向 - 要完成请求必须进行更进一步的处理
    4XX 客户端错误 - 请求有语法错误或请求无法实现
    5XX 服务器端错误 - 服务器未能实现合法的请求响应头
```

## 网站的类型

```python
1.静态网站：页面数据一次请求时全部加载直接返回至响应数据，局部操作时浏览器跟随刷新；
2.动态网站：页面数据多次请求时跟随每一次请求进行异步刷新，局部操作时浏览器不跟随刷新
```

## 动态网站的特征

```python
1.需要登陆或验证码(常见的图形码，滑块码，拼图码，四位随机验证码，短信邮箱验证码等)
2.站点IP限制：同一个地址在短时间内大量请求的话会限制其请求次数——封IP
3.数据屏蔽：80%的动态网站是无法直接从页面的响应数据中检索目标数据的，大部分需要突破AJAX异步加载及js逆向进行检索，小部分直接采用反爬策略隐藏数据。
4.网站动态加载：跟随每一次请求操作在不刷新页面的情况下使用AJAX异步加载数据。
```

## 反爬虫机制(网站采用的防止爬虫程序请求数据的方式)

```python
1.封IP：监控短时间内同一地址的请求次数过大
2.登录及验证码：对于监控后封IP之后短时间内继续的大量请求，要求登陆或验证码通过验证之后才能继续进行。
3.健全账号体制：即核心数据只能通过账号登录后才能进行访问。
4.动态加载数据：数据通过js进行加载，增加网站分析难度。
```

## 反反爬策略(针对网站常见的反爬虫机制设计的常用反制措施，以达到能顺利获取数据的目的)

```python
1.伪造请求头(伪装浏览器)：故意告诉浏览器我不是爬虫程序我是浏览器。
2.代理IP访问：针对同一时间内大量请求网站数据遭到封IP，使用代理IP不断更换请求地址，迷惑网站，躲过反制措施。
3.请求过于频繁会触发验证码，则模拟用户操作，限制爬虫请求次数及频率，降低验证码机制的风险
4.使用对应的验证码识别手段通过网站验证
5.使用第三方工具完全模拟浏览器操作(selenium+webdriver)
```

## 网站为何要反制爬虫

```python
1.保护企业自有数据的安全。
2.保护企业服务器正常稳定运行。
3.版权等其他原因。

爬虫 VS 网站数据安全
矛		盾
```

# 爬虫请求模块——urllib.request
## 模块及导入

```python
1、模块名：urllib.request
2、导入方式：
	1、import urllib.request
	2、from urllib import request
```

## 常用方法详解

### urllib.request.urlopen

- **作用**
  向网站发起请求并获取响应对象
- **语法**

```python
变量名 = urllib.requrest.urlopen(url,timeout)
```

- **参数**

```python
1.url:需要爬取的网站的URL地址
2.timeout:设置等待超时时间，指定时间内未得到响应则抛出超时异常
```

- **示例：最简单的爬虫程序——输入百度地址（‘http://www.baidu.com’）,得到百度首页的响应内容**

```python
import urllib.request
# urlopen() ： 向URL发请求,返回响应对象,保存变量于response
response=urllib.request.urlopen('http://www.baidu.com/')
# 提取响应内容:响应对象调用read方法读取对应的响应内容，因为得到的是字节串，所以解码为字符串，注意设置编码方式utf-8
html = response.read().decode('utf-8')
# 打印响应内容
print(html)
```

- **响应对象（response）方法**

```python
1、bytes = response.read() # read()得到结果为 bytes 数据类型
2、string = response.read().decode() # decode() 转为 string 数据类型
3、url = response.geturl() # 返回实际数据的URL地址
4、code = response.getcode() # 返回HTTP响应码
# 补充
5、string.encode() # bytes -> string
6、bytes.decode() # string -> bytes
```

**思考：网站是如何判断是人类正常访问还是爬虫程序访问？接下来通过一段简单测试代码查看：**

```python
import urllib.request
# 向测试网站：http://httpbin.org/get发送请求，获取响应对象并查看请求头
response = urllib.request.urlopen('http://httpbin.org/get')
# 响应对象读取响应内容并转为字符串显示
html = response.read().decode('utf-8')
print(html)

====================================================================================

得到的响应结果如下：

/home/anwc/anaconda3/bin/python /home/anwc/文档/文档、代码杂七八/code_demo.py
{
  "args": {}, 
  "headers": {
    "Accept-Encoding": "identity", 
    "Host": "httpbin.org", 
    "User-Agent": "Python-urllib/3.6", 
    "X-Amzn-Trace-Id": "Root=1-5eb51309-98987ec462d6a7fe19b38aea"
  }, 
  "origin": "27.18.84.11", 
  "url": "http://httpbin.org/get"
}


Process finished with exit code 0

====================================================================================

通过响应内容我们发现：请求头中User-Agent竟然是:Python-urllib/3.6!!!!!!!!!!!!!!!!!!!

我们需要重构User-Agent,发请求时带着User-Agent过去,但是 urlopen()方法不支持重构User-Agent！

那我们怎么办？请看下面的方法！！！
```

### urllib.request.Request

- **作用**
  创建请求对象(包装请求，重构User-Agent，使程序更像正常人类请求)
- **语法**

```python
response = urllib.request.Request(url = url,headers = headers)
```

- **参数**

```python
1、url：请求的URL地址
2、headers：添加请求头（爬虫和反爬虫斗争的第一步）
```

- **使用流程**

```python
1、构造请求对象(重构User-Agent)
2、发请求获取响应对象(urlopen)
3、获取响应对象内容
```

- **示例：向测试网站发起请求，构造请求头并从响应对象中确认请求头信息**

```python
from urllib import request

# 定义常用变量
url = 'http://httpbin.org/get'
headers = {'User-Agent':'Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/81.0.4044.138 Safari/537.36'}
# 1.创建请求对象
req = request.Request(url=url,headers=headers)
# 2.获取响应对象
resp = request.urlopen(req)
# 3.提取响应内容
html = resp.read().decode()

print(html)

==================================================================================

得到的响应信息如下：

/home/anwc/anaconda3/bin/python /home/anwc/文档/文档、代码杂七八/code_demo.py
{
  "args": {}, 
  "headers": {
    "Accept-Encoding": "identity", 
    "Host": "httpbin.org", 
    "User-Agent": "Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/81.0.4044.138 Safari/537.36", 
    "X-Amzn-Trace-Id": "Root=1-5eb515fc-67a09f30af080940ecd78190"
  }, 
  "origin": "27.18.84.11", 
  "url": "http://httpbin.org/get"
}


Process finished with exit code 0

```



# 爬虫请求模块——requests

## 安装

- **Linux**

```python
sudo pip3 install requests
```

- **Windows**

```python
# 方法一
   进入cmd命令行 ：python -m pip install requests
# 方法二
   右键管理员进入cmd命令行 ：pip install requests
```

## requests.get()

- **作用**

```python
# 向网站发起请求,并获取响应对象
res = requests.get(url,headers=headers)
```

- **参数**

```python
1、url ：需要抓取的URL地址
2、headers : 请求头
3、timeout : 超时时间，超过时间会抛出异常
```

- **响应对象(res)属性**

```python
1、encoding ：响应字符编码
   res.encoding = 'utf-8'
2、text ：字符串
3、content ：字节流
4、status_code ：HTTP响应码
5、url ：实际数据的URL地址

```

- **非结构化数据保存**

```python
with open('xxx.jpg','wb') as f:
	f.write(res.content)
```

### requests.get()参数

### 查询参数-params

- **参数类型**

```python
字典,字典中键值对作为查询参数
```

- **使用方法**

```python
1、res = requests.get(url,params=params,headers=headers)
2、特点: 
   * url为基准的url地址，不包含查询参数
   * 该方法会自动对params字典编码,然后和url拼接
```

- **示例**

```python
import requests

baseurl = 'http://tieba.baidu.com/f?'
params = {
  'kw' : '赵丽颖吧',
  'pn' : '50'
}
headers = {'User-Agent' : 'Mozilla/4.0'}
# 自动对params进行编码,然后自动和url进行拼接,去发请求
res = requests.get(url=baseurl,params=params,headers=headers)
res.encoding = 'utf-8'
print(res.text)
```

**练习**

```python
把抓取百度贴吧的案例改为 params 参数实现
```

### Web客户端验证参数-auth

- **作用及类型**

```python
1、针对于需要web客户端用户名密码认证的网站
2、auth = ('username','password')
```

### SSL证书认证参数-verify

- **适用网站及场景**

```python
1、适用网站: https类型网站但是没有经过 证书认证机构 认证的网站
2、适用场景: 抛出 SSLError 异常则考虑使用此参数
```

- **参数类型**

  ```python
  1、verify=True(默认)   : 检查证书认证
  2、verify=False（常用）: 忽略证书认证
  # 示例
  response = requests.get(
  	url=url,
  	params=params,
  	headers=headers,
  	verify=False
  )
  ```

### 代理参数-proxies

- **定义**

```python
1、定义: 代替你原来的IP地址去对接网络的IP地址。
2、作用: 隐藏自身真实IP,避免被封。
```

## requests.post()参数

- **适用场景**

```
Post类型请求的网站
```

- **参数-data**

```python
response = requests.post(url,data=data,headers=headers)
# data ：post数据（Form表单数据-字典格式）
```

- **请求方式的特点**

```python
# 一般
GET请求 : 参数在URL地址中有显示
POST请求: Form表单提交数据
```

# 案例1：百度图片爬取

```python
需求：保存任意想搜索的明星的图片到本地

编码实现：

基础编码

#导入所需模块
import requests
from urllib import parse
import re
import os
from lxml import etree
#------第一步：确定目标url，伪造headers，为正式发起请求作准备------
# 1.确定基本url格式
# 即你要向哪个网站发起请求，本案例中，我们要在百度图片网站上搜索明星图片
# 即需要向百度图片网站发起请求
url = 'https://image.baidu.com/search/index?tn=baiduimage&word={}'

# 2.明确目标url基本格式
# 目标关键词：你想搜谁的图片，就输入谁的名字，该关键词最后要拼接进基本url
word = input('你想要谁的照片？请输入:')
# 3.因为直接输入的字符类型为字符串，并不能直接使用，所以需要转unicode码
# 转unicode码
params = parse.quote(word)

# 4.拼接得到最终请求url
url = url.format(params)
# 5.伪造headers：说白了就是骗浏览器“我们不是机器，我们是人～”
headers = { 'User-Agent': 'Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/81.0.4044.138 Safari/537.36'}

#------第二步：发请求------
#向网站正式发起请求，获取页面数据，转为字符文本
html = requests.get(url=url,headers=headers).text

#------第三步：数据筛选
# 响应结果中的html文本内容很多，需要从中找出我们所需的图片url文本并采用合适的方式保存以备后续使用
# 筛选、解析方式很多，介绍两种基本方式
# 1.使用xpath匹配
# dom = etree.HTML(html)
# link_list = dom.xpath('//ul[@class="imglist clearfix pageNum0"]/li[@class="imgitem"]/@data-thumburl')
# 从得到的响应结果中可以看到，目标图片的路径不在html元素的属性或内容中，而是在js的传参数据中
# 结论：此案例中无法使用xpath解析，因为解析出来的html元素中不存在目标图片路径，xpath解析内容为空
# 2.使用正则匹配
# 找到js中存在的目标图片的路径，因为此时js代码也是属于响应内容的文本之一，可以使用正则表达式进行匹配。
# 编写正则表达式，采用compile方法匹配，参数1：正则表达式，参数2：匹配包括换行在内的所有字符
# p = re.compile('"thumbURL":"(.*?)"',re.S)
# link_list = p.findall(html)
# 直接使用findall()
link_list = re.findall('"thumbURL":"(.*?)"',html)
# 使用search()方法
# link_list = re.search('"thumbURL":"(.*?)"',html).group(1)

# # 验证是否获取到url
# print(link_list)
# link_list: ['xxx.jpg','xxx.jpg']

#------第四步：对目标图片发起请求并将响应内容进行持久化存储
# 1.创建图片保存路径，保存图片到本地
directory = '/home/anwc/桌面/{}/'.format(word)

#os.path.exists(directory)表示目录存在
#如果目录不存在(即先判断是否已存在目标目录)
if not os.path.exists(directory):
    # 创建空目录并命名
    os.makedirs(directory)
# 2.循环的对目标图片发起请求获得响应
for link in link_list:
    # 请求图片获得响应
    html = requests.get(url=link, headers=headers).content
    # 拼接我们想要的图片文件名(包含路径)
    filename = directory + '{}.jpg'.format(link[-24:-15])
    # 写入文件
    with open(filename, 'wb') as f:
        f.write(html)
    f.close()
    print(filename, '下载成功')
    

面向对象编程：


# -*- encoding: utf-8 -*-
'''
@File    :   demo04_BaiduImageSpider_OOP.py
@Time    :   2020/09/09 10:01:20
@Author  :   安伟超 
@Version :   1.0
@Contact :   awc19930818@outlook.com
@github  :   https://github.com/La0bALanG
@requirement:
'''

import threading
import requests
from urllib import parse
import re
import os
from lxml import etree


class BaiduImageSpider(object):
    '''
    
    面向对象思路：
    1.拆分功能细节。整体程序可拆分为:
        1.发请求获得页面
        2.解析页面
        3.持久化存储(写入文件保存)
    2.结合开闭原则，封装功能方法为私有方法，对外提供统一公共接口
    3.采用单例模式：假设本爬虫程序在多个时间、不同情况下多次使用，单例模式实现只创建一个对象，提升性能避免内存占用过高。


    
    '''
    _instance_lock = threading.Lock()
    
    #单例模式实现：__new__方法
    def __new__(cls, *args, **kwargs):
        if not hasattr(BaiduImageSpider, '_instance'):
            with BaiduImageSpider._instance_lock:
                if not hasattr(BaiduImageSpider, '_instance'):
                    BaiduImageSpider._instance = object.__new__(cls)
        return BaiduImageSpider._instance

    def __init__(self):
        self.__url = 'https://image.baidu.com/search/index?tn=baiduimage&word={}'
        self.__headers = {
            'User-Agent': 'Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/81.0.4044.138 Safari/537.36'
        }

    #设置只读属性
    @property
    def url(self):
        return self.__url

    @property
    def headers(self):
        return self.__headers

    def __get_html(self,url):
        return requests.get(url=url, headers=self.__headers).text

    def __parse_html(self,html):
        return re.findall('"thumbURL":"(.*?)"', html)

    def __download_image(self,url):
        return requests.get(url=url,headers=self.__headers).content

    def __save_html(self,directory,data):

        # os.path.exists(directory)表示目录存在
        # 如果目录不存在(即先判断是否已存在目标目录)
        if not os.path.exists(directory):
            # 创建空目录并命名
            os.makedirs(directory)
        # 2.循环的对目标图片发起请求获得响应
        for link in data:
            # 请求图片获得响应
            img = self.__download_image(link)
            # 拼接我们想要的图片文件名(包含路径)
            filename = directory + '{}.jpg'.format(link[-24:-15])
            # 写入文件
            with open(filename, 'wb') as f:
                f.write(img)
            f.close()

    def display(self,word):
        directory = '/home/anwc/桌面/{}/'.format(word)
        self.__save_html(directory,self.__parse_html(self.__get_html(self.__url.format(parse.quote(word)))))


def test():
    word = input('请输入明星>>>:')
    BaiduImageSpider.display(word)

if __name__ == '__main__':
    test()

```

# URL地址编码模块——urllib.parse

## 模块及导入

- **模块**

```python
# 模块名
urllib.parse
# 导入
import urllib.parse
from urllib import parse
```

- **作用**
  给URL地址中查询参数进行编码

```python
编码前：https://www.baidu.com/s?wd=美女
编码后：https://www.baidu.com/s?wd=%E7%BE%8E%E5%A5%B3
```

## 常用方法详解

### urllib.parse.urlencode({dict})

- **URL地址中查询一个参数**

	* **示例3：给定一个查询参数并将其进行编码**

```python
import urllib.parse
# 给定一个查询参数
query_str = {'wd':'美眉'}
# 调用urlencode方法将其编码
result = urllib.parse.urlencode(query_str)
print(result)
```

- **URL地址中多个查询参数**

	* **示例4：给定多个查询参数并将其进行编码**

```python
from urllib import parse
params = {
    'wd':'美眉',
    'pn':'50'
}
params = parse.urlencode(params)
url = 'http://www.baidu.com/s?{}'.format(params)
print(url)

```

- **拼接URL地址的3种方式**

```python
# 1、字符串相加
baseurl = 'http://www.baidu.com/s?'
params = 'wd=%E7XXXX&pn=20'
url = baseurl + params
# 2、字符串格式化（占位符）
params = 'wd=%E7XXXX&pn=20'
url = 'http://www.baidu.com/s?%s'% params
# 3、format()方法
url = 'http://www.baidu.com/s?{}'
params = 'wd=#E7XXXX&pn=20'
url = url.format(params)
```

- **示例：在百度种输入要搜索的内容，把响应内容保存到本地文件**

```python
from urllib import request,parse
# 拼接URL
my_input = input('请输入你要搜索的内容：')
parmas = parse.urlencode({'wd':my_input})
url = 'http://www.baidu.com/s?{}'.format(parmas)

# 创建请求头
headers = {
    'User-Agent':'Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/81.0.4044.138 Safari/537.36'
}

# 创建请求对象
req = request.Request(url=url,headers=headers)
# 获取响应对象并读取响应内容
response = request.urlopen(req)
result = response.read().decode()
# 将响应内容写入文件
filename = my_input + '.html'
with open(filename,'w') as f:
    f.write(result)
```

### quote(str)编码

- **示例：对单个字符串进行编码**

```python
from urllib import parse
str1 = '美眉'
print(parse.quote(str1))
```

- **示例7：针对示例5，将URL编码改为使用quote方法实现**

```python
from urllib import request,parse
# 拼接URL
my_input = input('请输入你要搜索的内容：')
parmas = parse.quote(my_input)
url = 'https://www.baidu.com/s?wd={}'.format(parmas)

# 创建请求头
headers = {
    'User-Agent':'Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/81.0.4044.138 Safari/537.36'
}

# 创建请求对象
req = request.Request(url=url,headers=headers)
# 获取响应对象并读取响应内容
response = request.urlopen(req)
result = response.read().decode()
# 将响应内容写入文件
filename = my_input + '.html'
with open(filename,'w') as f:
    f.write(result)
```

### unquote(str)解码

- **示例8：对单个字符进行解码**

```python
from urllib import parse
string = '%E7%BE%8E%E5%A5%B3'
result = parse.unquote(string)
print(result)
```

# re正则表达式

## re模块使用流程

- **方法一**

```python
r_list=re.findall('正则表达式',html,re.S)
```

- **方法二**

```python
# 1、创建正则编译对象
pattern = re.compile(r'正则表达式',re.S)
r_list = pattern.findall(html)
```

## 正则表达式元字符

| 元字符 | 含义                     |
| ------ | ------------------------ |
| .      | 任意一个字符（不包括\n） |
| \d     | 一个数字                 |
| \s     | 空白字符                 |
| \S     | 非空白字符               |
| []     | 包含[]内容               |
| *      | 出现0次或多次            |
| +      | 出现1次或多次            |

## 思考：请写出匹配任意一个字符的正则表达式？

```python
import re
# 方法一
pattern = re.compile('.',re.S)
# 方法二
pattern = re.compile('[\s\S]')
```

## 贪婪匹配（默认）

```python
1、在整个表达式匹配成功的前提下,尽可能多的匹配 *
2、表示方式： .*
```

## 非贪婪匹配

```python
1、在整个表达式匹配成功的前提下,尽可能少的匹配 *
2、表示方式：.*?
```

**示例10:正则匹配演示**

```python
import re

html = '''
<div><p>九霄龙吟惊天变</p></div>
<div><p>风云际会浅水游</p></div>
'''

# 贪婪匹配
p = re.compile('<div><p>.*</p></div>',re.S)
r_list = p.findall(html)

# 非贪婪匹配
p = re.compile('<div><p>.*?</p></div>',re.S)
r_list = p.findall(html)
```

## 正则表达式分组

- **作用**

在完整的模式中定义子模式，将每个圆括号中子模式匹配出来的结果提取出来

- **示例11：分组演示**

```python
import re

s = 'A B C D'
p1 = re.compile('\w+\s+\w+')
print(p1.findall(s))
# 结果: ？？？

p2 = re.compile('(\w+)\s+\w+')
print(p2.findall(s))
# 结果: ？？？

p3 = re.compile('(\w+)\s+(\w+)')
print(p3.findall(s))
# 结果: ？？？
```

- **分组总结**

```python
1、在网页中,想要什么内容,就加()
2、先按整体正则匹配,然后再提取分组()中的内容
  如果有2个及以上分组(),则结果中以元组形式显示 [('小区1','500万'),('小区2','600万'),()]
```

- **练习**

页面结构如下：

```html
# <div class="animal">.*?title="(.*?)".*?
<div class="animal">
    <p class="name">
		<a title="Tiger"></a>
    </p>
    <p class="content">
		Two tigers two tigers run fast
    </p>
</div>

<div class="animal">
    <p class="name">
		<a title="Rabbit"></a>
    </p>

    <p class="content">
		Small white rabbit white and white
    </p>
</div>
```

从以上html代码结构中完成如下内容信息的提取：

```python
# 问题1
[('Tiger',' Two...'),('Rabbit','Small..')]
# 问题2
动物名称 ：Tiger
动物描述 ：Two tigers two tigers run fast
***************************************
动物名称 ：Rabbit
动物描述 ：Small white rabbit white and white
```

- **代码实现**

```python
import re

html = '''
<div class="animal">
    <p class="name">
		<a title="Tiger"></a>
    </p>
    <p class="content">
		Two tigers two tigers run fast
    </p>
</div>

<div class="animal">
    <p class="name">
		<a title="Rabbit"></a>
    </p>

    <p class="content">
		Small white rabbit white and white
    </p>
</div>
'''
p = re.compile('<div class="animal">.*?<a title="(.*?)"'
               '.*?<p class="content">(.*?)</p>',re.S)
r_list = p.findall(html)

# 第1步: r_list: [('Tiger','\n\t\tTwo tigers'),()]
print(r_list)
# 第2步
for r in r_list:
    print('动物名称:',r[0].strip())
    print('动物描述:',r[1].strip())
    print('*' * 50)


==========================================================================================

运行结果：

/home/anwc/anaconda3/bin/python /home/anwc/文档/文档、代码杂七八/code_demo.py
[('Tiger', '\n\t\tTwo tigers two tigers run fast\n    '), ('Rabbit', '\n\t\tSmall white rabbit white and white\n    ')]
动物名称: Tiger
动物描述: Two tigers two tigers run fast
**************************************************
动物名称: Rabbit
动物描述: Small white rabbit white and white
**************************************************

Process finished with exit code 0

==========================================================================================

常见方法总结：
1. strip()  - 去掉左右两侧的空白
2. split()
  '东方美景|200万|23层'.split('|')
  ['东方美景','200万','23层']
3. replace()
  '霸王别姬&nbsp;大话西游&nbsp;'.replace('&nbsp;',' ')
  结果: '霸王别姬 大话西游'
4. startswith()
5. endswith()
   if 'xxx.zip'.endswith('.zip'):
       开始抓取 xxx.zip 文件到本地
6. join()
   '\n'.join(['第一章:大圣娶亲','第二章:月光宝盒','第三章:美人鱼'])
   '第一章:大圣娶亲\n第二章xxx'
7. 切片
```

# 爬虫数据解析模块——re模块

## re模块支持的正则语法

```python
"."
"^"
"$"
"*"
"+"
"?"
*?,+?,??
{m,n}
{m,n}?
"\\"
[]
"|"
(...)
(?aiLmsux)
(?:...)
(?P<name>...)
(?P=name)
(?#...)
(?=...)
(?!...)
(?<=...)
(?<!...)
(?(id/name)yes|no)
```

## re模块内置的常用方法

| 方法              | 描述                                   | 返回值                           |
| ----------------- | -------------------------------------- | -------------------------------- |
| comple(re,flags)  | 根据包含正则表达式的字符串创建模式对象 | re对象                           |
| search(re,flags)  | 在字符串中查找                         | 第一个匹配到的对象或者None       |
| match(re,flags)   | 在字符串的开始处匹配查找               | 在字符串开头匹配到的对象或者None |
| split()           | 根据模式的匹配项来分割字符串           | 分割后的字符串列表               |
| findall(re,flags) | 列出字符串中模式的所有匹配项           | 所有匹配到的字符串列表           |
| sub()             | 将字符串中所有的匹配项用repl替换       | 完成替换后的新字符串             |

常见的flag匹配模式：

| 匹配模式 | 描述                                                       |
| -------- | ---------------------------------------------------------- |
| re.A     | ASCII字符模式                                              |
| re.I     | 使匹配对大小写不敏感，也就是不区分大小写                   |
| re.L     | 做本地化识别匹配                                           |
| re.M     | 多行匹配，影响^和 $                                        |
| re.S     | 使.这个通配符能够匹配包括换行在内的所有字符，针对多行匹配  |
| re.U     | 根据unicode字符集解析字符，这个标志影响\w,\W,\b,\B         |
| re.X     | 该标志通过给予你更灵活的格式以便将正则表达式写的更易于理解 |

# 案例2：百度贴吧数据抓取

```python
#------基础编码实现-------
# -*- coding:utf-8 _*-
"""
@version:
author:安伟超
@time: 2020/09/07
@file: demo01_baidutieba_simple.py
@environment:virtualenv
@email:awc19930818@outlook.com
@github:https://github.com/La0bALanG
@requirement:1.输入贴吧名称 2.输入起始页 3.输入终止页 4.保存响应的页面内容至txt文档
"""

from urllib import request,parse

"""
思路：
1.分析页面URL规律
2.构造查询参数
3.发起请求获得响应
4.写入文件

"""
"""
1.分析页面URL规律

打开百度贴吧，随便搜索一个吧，进入，提取出URL：

https://tieba.baidu.com/f?kw=%E9%95%BF%E6%B2%99&ie=utf-8&pn=0
https://tieba.baidu.com/f?kw=%E6%9D%8E%E6%AF%85&ie=utf-8&pn=0
...

查找规律：
    1.kw查询关键字，需要实时传参；
    2.pn页码参数，单位50，代表当前第几页
    3.查询参数因为是汉字，传入时需要先转成urlencode编码
    
总结URL基本格式：
https://tieba.baidu.com/f?kw={}&ie=utf-8&pn={}

所以，总结思路如下：
    1.构造基本URL格式
    2.构造查询起始页及终止页页码数
    3.构造查询参数及页码参数
    4.字符串拼接，完成最终URL确定格式
"""

"""

2.确定URL后：
    1.伪造headers
    2.发起正式请求

"""

"""

3.获得具体响应内容后：
写入文件

"""

#伪造headers
headers = {
    'User-Agent':'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/85.0.4183.83 Safari/537.36'
}



#构造基本URL格式
url = 'https://tieba.baidu.com/f?kw={}&ie=utf-8&pn={}'

#构造起始页及终止页
begin = int(input('请输入起始页：'))
end = int(input('请输入终止页：'))
#查询页码数量：end - begin
# page = end - begin

#构造查询参数并转urlencode编码
kw = input('请输入您想搜索的贴吧名称>>>:')
parmas = parse.quote(kw)
#依据页码构造最终n个URL
for page in range(begin,end + 1):
    pn = (page - 1) * 50
    # print(pn)
    finall_url = url.format(parmas,pn)
    #测试URL格式
    # print(finall_url)


    #发请求
    #1.创建请求对象
    print('开始爬取第%d页...'%page)

    reqs = request.Request(url=finall_url,headers = headers)
    #2.发起正式请求并解码请求内容
    resp = request.urlopen(reqs).read()
    # print(resp)

    print('第%d页爬取完成，稍等，马上开始写入文件内容...'%page)
    # 写入文件：

    filename = kw + '吧' + '_第%d页.html'%page
    with open(filename,'wb') as f:
        f.write(resp)

    f.close()
    print('文件写入完毕，开始下一页爬取...')


print('程序结束。')


#-----面向对象编程-----
# -*- coding:utf-8 _*-
"""
@version:
author:安伟超
@time: 2020/09/07
@file: demo01_baidutieba_OOP.py
@environment:virtualenv
@email:awc19930818@outlook.com
@github:https://github.com/La0bALanG
@requirement:1.输入贴吧名称 2.输入起始页 3.输入终止页 4.保存响应的页面内容至txt文档
"""
import threading
from urllib import request, parse

"""
思路：
1.分析页面URL规律
2.构造查询参数
3.发起请求获得响应
4.写入文件

"""
"""
1.分析页面URL规律

打开百度贴吧，随便搜索一个吧，进入，提取出URL：

https://tieba.baidu.com/f?kw=%E9%95%BF%E6%B2%99&ie=utf-8&pn=0
https://tieba.baidu.com/f?kw=%E6%9D%8E%E6%AF%85&ie=utf-8&pn=0
...

查找规律：
    1.kw查询关键字，需要实时传参；
    2.pn页码参数，单位50，代表当前第几页
    3.查询参数因为是汉字，传入时需要先转成urlencode编码

总结URL基本格式：
https://tieba.baidu.com/f?kw={}&ie=utf-8&pn={}

所以，总结思路如下：
    1.构造基本URL格式
    2.构造查询起始页及终止页页码数
    3.构造查询参数及页码参数
    4.字符串拼接，完成最终URL确定格式
"""

"""

确定URL后：
    1.伪造headers
    2.发起正式请求

"""

"""

获得具体响应内容后：
写入文件

"""


class BaiduTiebaSpider(object):
    """

    面向对象思路：
        1.拆分功能细节。整体程序可拆分为:
            1.发请求获得页面
            2.解析页面
            3.持久化存储(写入文件保存)
        2.结合开闭原则，封装功能方法为私有方法，对外提供统一公共接口
        3.采用单例模式：假设本爬虫程序在多个时间、不同情况下多次使用，单例模式实现只创建一个对象，提升性能避免内存占用过高。


    """

    #添加线程锁，避免实际运行过程中受多线程影响
    _instance_lock = threading.Lock()

    def __init__(self):
        self.__url = 'https://tieba.baidu.com/f?kw={}&ie=utf-8&pn={}'

    #单例模式实现：__new__方法

    def __new__(cls, *args, **kwargs):
        if not hasattr(BaiduTiebaSpider, '_instance'):
            with BaiduTiebaSpider._instance_lock:
                if not hasattr(BaiduTiebaSpider, '_instance'):
                    BaiduTiebaSpider._instance = object.__new__(cls)
        return BaiduTiebaSpider._instance

    #设置只读属性，体现封装思想
    @property
    def url(self):
        return self.__url

    def __get_html(self,url):
        # 伪造headers
        headers = {
            'User-Agent': 'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/85.0.4183.83 Safari/537.36'
        }
        # 发请求
        # 1.创建请求对象

        reqs = request.Request(url=url, headers=headers)
        # 2.发起正式请求，获得页面响应数据
        return request.urlopen(reqs).read()

    def __parse_html(self):
        pass

    def __save_html(self,filename,html):
        with open(filename,'wb') as f:
            f.write(html)

    def display(self):
        # 构造起始页及终止页
        begin = int(input('请输入起始页：'))
        end = int(input('请输入终止页：'))
        # 查询页码数量：end - begin
        # page = end - begin

        # 构造查询参数并转urlencode编码
        kw = input('请输入您想搜索的贴吧名称>>>:')
        parmas = parse.quote(kw)
        # 依据页码构造最终n个URL
        for page in range(begin, end + 1):
            pn = (page - 1) * 50
            # print(pn)
            finall_url = self.__url.format(parmas, pn)
            html = self.__get_html(finall_url)
            filename = kw + '吧' + '_第%d页.html'%page
            self.__save_html(filename,html)

def test():
    BaiduTiebaSpider().display()

if __name__ == '__main__':
    test()


```

# 案例3：猫眼电影top100抓取

```python
# -*- coding:utf-8 _*-
"""
@version:
author:安伟超
@time: 2020/09/07
@file: demo02_MaoYanMovie_simple.py.py
@environment:virtualenv
@email:awc19930818@outlook.com
@github:https://github.com/La0bALanG
@requirement:1.获取top100榜单页面全部内容；
	2.使用正则匹配出每一条的电影名称，主演，上映时间
	3.将获取的内容写入字典（下一节讲解写入持久化存储）
"""
import threading
import re
from urllib import request
from time import sleep
from random import randint

"""

数据抓取实现思路：
1.分析URL规律
2.分析页面结构，确定存在所需数据
3.构造headers及最终请求URL
4.发送请求获得相应数据
5.使用正则匹配解析所需数据存入字典

1.分析URL规律

进入猫眼电影网-榜单-top100，随意查看几页，观察其URL规律：
https://maoyan.com/board/4?offset=20
https://maoyan.com/board/4?offset=30
...
https://maoyan.com/board/4?offset=(页数 - 1) * 10

2.分析页面结构，确定存在所需数据
浏览器F12-打开控制台-抓手工具-抓到对应电影内容-查看html信息，如下：

<div class="movie-item-info">
        <p class="name"><a href="/films/4883" title="钢琴家" data-act="boarditem-click" data-val="{movieId:4883}">钢琴家</a></p>
        <p class="star">
                主演：艾德里安·布洛迪,艾米莉娅·福克斯,米哈乌·热布罗夫斯基
        </p>
        <p class="releasetime">上映时间：2002-05-24(法国)</p>    </div>

所需数据存在上部分的响应内容中

3.构造headers及最终请求URL

4.发送请求获得响应数据

5.解析数据
依据上述内容，确定使用正则表达式匹配
匹配思路：
    1.class为name的p标签内部的a标签，其title属性的属性值为电影名称；
    2.class为star的p标签的内容为电影的主演信息；
    3.class为releasetime的p标签的内容为电影的上映时间；
    
构造正则表达式，匹配以上内容即可：
<div class="movie-item-info">.*?title="(.*?)".*?class="star">(.*?)</p>.*?releasetime">(.*?)</p>

6.数据按照合适形式组织存入字典
"""

class MaoYanMovieSpider(object):
    '''

    面向对象思路：
        1.拆分功能细节。整体程序可拆分为:
            1.发请求获得页面
            2.解析页面
            3.持久化存储(写入文件保存)
        2.结合开闭原则，封装功能方法为私有方法，对外提供统一公共接口
        3.采用单例模式：假设本爬虫程序在多个时间、不同情况下多次使用，单例模式实现只创建一个对象，提升性能避免内存占用过高。

    '''
    #添加线程锁，避免实际运行过程中受多线程影响

    _instance_lock = threading.Lock()

    def __init__(self):
        self.__url = 'https://maoyan.com/board/4?offset={}'

        #计数变量
        self.__i = 0

    #单例模式实现：__new__方法
    def __new__(cls, *args, **kwargs):
        if not hasattr(MaoYanMovieSpider, '_instance'):
            with MaoYanMovieSpider._instance_lock:
                if not hasattr(MaoYanMovieSpider, '_instance'):
                    MaoYanMovieSpider._instance = object.__new__(cls)
        return MaoYanMovieSpider._instance

    #设置只读属性
    @property
    def url(self):
        return self.__url

    @property
    def i(self):
        return self.__i

    def __get_html(self,url):
        #伪造headers
        headers = {
            'User-Agent': 'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/85.0.4183.83 Safari/537.36'
        }
        # 发请求
        # 1.创建请求对象
        reqs = request.Request(url=url, headers=headers)
        # 2.发起正式请求，获得页面响应数据
        reps = request.urlopen(reqs).read().decode()
        self.__parse_html(reps)


    def __parse_html(self,html):
        #创建正则对象
        r = re.compile('<div class="movie-item-info">.*?title="(.*?)".*?class="star">(.*?)</p>.*?releasetime">(.*?)</p>',re.S)
        #正则匹配，查找到的结果存入列表
        find_list = re.findall(r,html)
        self.__save_html(find_list)

    def __save_html(self,data_list):
        dict = {}
        # 遍历查询结果集
        for item in data_list:
            # 每一项内容清洗后存入对应的键名
            dict['name'] = item[0].strip()
            dict['star'] = item[1].strip()
            dict['time'] = item[2].strip()[5:15]
            self.__i += 1
            print(dict)
    def display(self):
        print('爬虫程序开始执行，即将爬取top100榜单信息，每间隔3到5秒继续...')
        for i in range(0,91,10):
            url = self.__url.format(i)
            self.__get_html(url)
            sleep(randint(3,5))
        print('抓取的数据量：%d'%self.__i)

def test():
    MaoYanMovieSpider().display()
    print('程序结束！')

if __name__ == '__main__':
    test()





    

========================================================================

得到的结果：

anwc@anwc:~/文档/文档、代码杂七八$ python3 demo_spider_maoyan.py
程序开始执行，即将爬取top100榜单信息，每10条将间隔三到五秒继续...
{'name': '活着', 'star': '主演：葛优,巩俐,牛犇', 'time': '1994-05-17'}
{'name': '钢琴家', 'star': '主演：艾德里安·布洛迪,艾米莉娅·福克斯,米哈乌·热布罗夫斯基', 'time': '2002-05-24'}
{'name': '勇敢的心', 'star': '主演：梅尔·吉布森,苏菲·玛索,帕特里克·麦高汉', 'time': '1995-05-18'}
{'name': '阿飞正传', 'star': '主演：张国荣,张曼玉,刘德华', 'time': '2018-06-25'}
{'name': '射雕英雄传之东成西就', 'star': '主演：张国荣,梁朝伟,张学友', 'time': '1993-02-05'}
{'name': '爱·回家', 'star': '主演：俞承豪,金艺芬,童孝熙', 'time': '2002-04-05'}
{'name': '初恋这件小事', 'star': '主演：马里奥·毛瑞尔,平采娜·乐维瑟派布恩,阿查拉那·阿瑞亚卫考', 'time': '2012-06-05'}
{'name': '泰坦尼克号', 'star': '主演：莱昂纳多·迪卡普里奥,凯特·温丝莱特,比利·赞恩', 'time': '1998-04-03'}
{'name': '迁徙的鸟', 'star': '主演：雅克·贝汉,Philippe Labro', 'time': '2001-12-12'}
{'name': '蝙蝠侠：黑暗骑士', 'star': '主演：克里斯蒂安·贝尔,希斯·莱杰,阿伦·伊克哈特', 'time': '2008-07-14'}
{'name': '恐怖直播', 'star': '主演：河正宇,李璟荣,李大卫', 'time': '2013-07-31'}
{'name': '我爱你', 'star': '主演：宋在浩,李顺才,尹秀晶', 'time': '2011-02-17'}
{'name': '大闹天宫', 'star': '主演：邱岳峰,毕克,富润生', 'time': '1965-12-31'}
{'name': '剪刀手爱德华', 'star': '主演：约翰尼·德普,薇诺娜·瑞德,黛安娜·威斯特', 'time': '1990-12-06'}
{'name': '甜蜜蜜', 'star': '主演：黎明,张曼玉,杜可风', 'time': '2015-02-13'}
{'name': '闻香识女人', 'star': '主演：阿尔·帕西诺,克里斯·奥唐纳,加布里埃尔·安瓦尔', 'time': '1992-12-23'}
{'name': '英雄本色', 'star': '主演：狄龙,张国荣,周润发', 'time': '2017-11-17'}
{'name': '三傻大闹宝莱坞', 'star': '主演：阿米尔·汗,黄渤,卡琳娜·卡普', 'time': '2011-12-08'}
{'name': '黑客帝国3：矩阵革命', 'star': '主演：基努·里维斯,雨果·维文,凯瑞-安·莫斯', 'time': '2003-11-05'}
{'name': '触不可及', 'star': '主演：弗朗索瓦·克鲁塞,奥玛·希,安娜·勒尼', 'time': '2011-11-02'}
{'name': '忠犬八公物语', 'star': '主演：仲代达矢,春川真澄,井川比佐志', 'time': '1987-08-01'}
{'name': '辩护人', 'star': '主演：宋康昊,郭度沅,吴达洙', 'time': '2013-12-18'}
{'name': '喜剧之王', 'star': '主演：周星驰,莫文蔚,张柏芝', 'time': '1999-02-13'}
{'name': '黄金三镖客', 'star': '主演：克林特·伊斯特伍德,李·范·克里夫,埃里·瓦拉赫 Eli Wallach', 'time': '1966-12-23'}
{'name': '这个杀手不太冷', 'star': '主演：让·雷诺,加里·奥德曼,娜塔莉·波特曼', 'time': '1994-09-14'}
{'name': '借东西的小人阿莉埃蒂', 'star': '主演：志田未来,神木隆之介,大竹忍', 'time': '2010-07-17'}
{'name': '大话西游之月光宝盒', 'star': '主演：周星驰,莫文蔚,吴孟达', 'time': '2014-10-24'}
{'name': '一一', 'star': '主演：吴念真,金燕玲,李凯莉', 'time': '2000-05-15'}
{'name': '窃听风暴', 'star': '主演：乌尔里希·穆埃,塞巴斯蒂安·科赫,马蒂娜·格德克', 'time': '2006-03-23'}
{'name': '楚门的世界', 'star': '主演：金·凯瑞,劳拉·琳妮,诺亚·艾默里奇', 'time': '1998(罗马尼亚)'}
{'name': '飞屋环游记', 'star': '主演：爱德华·阿斯纳,乔丹·长井,鲍勃·彼德森', 'time': '2009-08-04'}
{'name': '哈尔的移动城堡', 'star': '主演：倍赏千惠子,木村拓哉,美轮明宏', 'time': '2004-09-05'}
{'name': '上帝之城', 'star': '主演：亚历桑德雷·罗德里格斯,艾莉丝·布拉加,莱安德鲁·菲尔米诺', 'time': '2002(俄罗斯)'}
{'name': '美丽心灵', 'star': '主演：罗素·克洛,詹妮弗·康纳利,艾德·哈里斯', 'time': '2001-12-13'}
{'name': '肖申克的救赎', 'star': '主演：蒂姆·罗宾斯,摩根·弗里曼,鲍勃·冈顿', 'time': '1994-09-10'}
{'name': '美丽人生', 'star': '主演：罗伯托·贝尼尼,尼可莱塔·布拉斯基,乔治·坎塔里尼', 'time': '2020-01-03'}
{'name': '倩女幽魂', 'star': '主演：张国荣,王祖贤,午马', 'time': '2011-04-30'}
{'name': '搏击俱乐部', 'star': '主演：爱德华·哈里森·诺顿,布拉德·皮特,海伦娜·伯翰·卡特', 'time': '1999-09-10'}
{'name': '春光乍泄', 'star': '主演：张国荣,梁朝伟,张震', 'time': '1997-05-17'}
{'name': '海上钢琴师', 'star': '主演：蒂姆·罗斯,比尔·努恩,克兰伦斯·威廉姆斯三世', 'time': '2019-11-15'}
{'name': '新龙门客栈', 'star': '主演：张曼玉,梁家辉,甄子丹', 'time': '2012-02-24'}
{'name': '驯龙高手', 'star': '主演：杰伊·巴鲁切尔,杰拉德·巴特勒,亚美莉卡·费雷拉', 'time': '2010-05-14'}
{'name': '教父2', 'star': '主演：阿尔·帕西诺,罗伯特·德尼罗,黛安·基顿', 'time': '1974-12-12'}
{'name': '美国往事', 'star': '主演：罗伯特·德尼罗,詹姆斯·伍兹,伊丽莎白·麦戈文', 'time': '2015-04-23'}
{'name': '魂断蓝桥', 'star': '主演：费雯·丽,罗伯特·泰勒,露塞尔·沃特森', 'time': '1940-05-17'}
{'name': '狮子王', 'star': '主演：马修·布罗德里克,尼基塔·卡兰姆,詹姆斯·厄尔·琼斯', 'time': '1995-07-15'}
{'name': '疯狂原始人', 'star': '主演：尼古拉斯·凯奇,艾玛·斯通,瑞安·雷诺兹', 'time': '2013-04-20'}
{'name': '唐伯虎点秋香', 'star': '主演：周星驰,巩俐,郑佩佩', 'time': '1993-07-01'}
{'name': '速度与激情5', 'star': '主演：范·迪塞尔,保罗·沃克,道恩·强森', 'time': '2011-05-12'}
{'name': 'V字仇杀队', 'star': '主演：娜塔莉·波特曼,雨果·维文,斯蒂芬·瑞', 'time': '2005-12-11'}
{'name': '龙猫', 'star': '主演：秦岚,糸井重里,岛本须美', 'time': '2018-12-14'}
{'name': '本杰明·巴顿奇事', 'star': '主演：布拉德·皮特,凯特·布兰切特,塔拉吉·P·汉森', 'time': '2008-12-25'}
{'name': '指环王2：双塔奇兵', 'star': '主演：伊莱贾·伍德,伊恩·麦克莱恩,丽芙·泰勒', 'time': '2003-04-25'}
{'name': '指环王1：护戒使者', 'star': '主演：伊莱贾·伍德,伊恩·麦克莱恩,丽芙·泰勒', 'time': '2002-04-04'}
{'name': '时空恋旅人', 'star': '主演：瑞秋·麦克亚当斯,多姆纳尔·格里森,比尔·奈伊', 'time': '2013-09-04'}
{'name': '末代皇帝', 'star': '主演：尊龙,陈冲,彼得·奥图尔', 'time': '1987-10-23'}
{'name': '天空之城', 'star': '主演：寺田农,鹫尾真知子,龟山助清', 'time': '1992-05-01'}
{'name': '风之谷', 'star': '主演：岛本须美,永井一郎,坂本千夏', 'time': '1992-05'}
{'name': '幽灵公主', 'star': '主演：松田洋治,石田百合子,田中裕子', 'time': '1998-05-01'}
{'name': '蝙蝠侠：黑暗骑士崛起', 'star': '主演：克里斯蒂安·贝尔,迈克尔·凯恩,加里·奥德曼', 'time': '2012-08-27'}
{'name': '十二怒汉', 'star': '主演：亨利·方达,李·科布,马丁·鲍尔萨姆', 'time': '1957-04-13'}
{'name': '素媛', 'star': '主演：李来,薛耿求,严志媛', 'time': '2013-10-02'}
{'name': '大话西游之大圣娶亲', 'star': '主演：周星驰,朱茵,莫文蔚', 'time': '2014-10-24'}
{'name': '教父', 'star': '主演：马龙·白兰度,阿尔·帕西诺,詹姆斯·肯恩', 'time': '2015-04-18'}
{'name': '海洋', 'star': '主演：雅克·贝汉,姜文,兰斯洛特·佩林', 'time': '2011-08-12'}
{'name': '黑客帝国', 'star': '主演：基努·里维斯,凯瑞-安·莫斯,劳伦斯·菲什伯恩', 'time': '2000-01-14'}
{'name': '鬼子来了', 'star': '主演：姜文,姜宏波,陈强', 'time': '2000-05-13'}
{'name': '哈利·波特与死亡圣器（下）', 'star': '主演：丹尼尔·雷德克里夫,鲁伯特·格林特,艾玛·沃特森', 'time': '2011-08-04'}
{'name': '辛德勒的名单', 'star': '主演：连姆·尼森,拉尔夫·费因斯,本·金斯利', 'time': '1993-11-30'}
{'name': '指环王3：王者无敌', 'star': '主演：伊莱贾·伍德,伊恩·麦克莱恩,丽芙·泰勒', 'time': '2004-03-15'}
{'name': '7号房的礼物', 'star': '主演：柳承龙,郑镇荣,朴信惠', 'time': '2013-01-23'}
{'name': '盗梦空间', 'star': '主演：莱昂纳多·迪卡普里奥,渡边谦,约瑟夫·高登-莱维特', 'time': '2010-09-01'}
{'name': '加勒比海盗', 'star': '主演：约翰尼·德普,凯拉·奈特莉,奥兰多·布鲁姆', 'time': '2003-11-21'}
{'name': '当幸福来敲门', 'star': '主演：威尔·史密斯,贾登·史密斯,坦迪·牛顿', 'time': '2008-01-17'}
{'name': '穿条纹睡衣的男孩', 'star': '主演：阿沙·巴特菲尔德,维拉·法梅加,大卫·休里斯', 'time': '2008-08-28'}
{'name': '音乐之声', 'star': '主演：朱莉·安德鲁斯,克里斯托弗·普卢默,埃琳诺·帕克', 'time': '1965-03-02'}
{'name': '无间道', 'star': '主演：刘德华,梁朝伟,黄秋生', 'time': '2003-09-05'}
{'name': '致命魔术', 'star': '主演：休·杰克曼,克里斯蒂安·贝尔,迈克尔·凯恩', 'time': '2006-10-17'}
{'name': '小鞋子', 'star': '主演：默罕默德·阿米尔·纳吉,Kamal Mirkarimi,Behzad Rafi', 'time': '1997(伊朗)'}
{'name': '萤火之森', 'star': '主演：内山昂辉,佐仓绫音,后藤弘树', 'time': '2011-09-17'}
{'name': '少年派的奇幻漂流', 'star': '主演：苏拉·沙玛,伊尔凡·可汗,塔布', 'time': '2012-11-22'}
{'name': '断背山', 'star': '主演：希斯·莱杰,杰克·吉伦哈尔,米歇尔·威廉姆斯', 'time': '2005-09-02'}
{'name': '罗马假日', 'star': '主演：格利高里·派克,奥黛丽·赫本,埃迪·艾伯特', 'time': '1953-08-20'}
{'name': '夜访吸血鬼', 'star': '主演：汤姆·克鲁斯,布拉德·皮特,克尔斯滕·邓斯特', 'time': '1994-11-11'}
{'name': '天堂电影院', 'star': '主演：菲利浦·诺瓦雷,赛尔乔·卡斯特利托,蒂兹亚娜·罗达托', 'time': '1988-11-17'}
{'name': '怦然心动', 'star': '主演：玛德琳·卡罗尔,卡兰·麦克奥利菲,艾丹·奎因', 'time': '2010-07-26'}
{'name': '乱世佳人', 'star': '主演：费雯·丽,克拉克·盖博,奥利维娅·德哈维兰', 'time': '1939-12-15'}
{'name': '完美的世界', 'star': '主演：凯文·科斯特纳,克林特·伊斯特伍德,T·J·劳瑟', 'time': '1993-11-24'}
{'name': '霸王别姬', 'star': '主演：张国荣,张丰毅,巩俐', 'time': '1993-07-26'}
{'name': '七武士', 'star': '主演：三船敏郎,志村乔,千秋实', 'time': '1954-04-26'}
{'name': '忠犬八公的故事', 'star': '主演：Forest,理查·基尔,琼·艾伦', 'time': '2009-06-13'}
{'name': '海豚湾', 'star': '主演：里克·奥巴瑞,路易·西霍尤斯,哈迪·琼斯', 'time': '2009-07-31'}
{'name': '拯救大兵瑞恩', 'star': '主演：汤姆·汉克斯,马特·达蒙,汤姆·塞兹摩尔', 'time': '1998-11-13'}
{'name': '机器人总动员', 'star': '主演：本·贝尔特,艾丽莎·奈特,杰夫·格尔林', 'time': '2008-06-27'}
{'name': '神偷奶爸', 'star': '主演：史蒂夫·卡瑞尔,杰森·席格尔,拉塞尔·布兰德', 'time': '2010-06-20'}
{'name': '放牛班的春天', 'star': '主演：热拉尔·朱尼奥,让-巴蒂斯特·莫尼耶,玛丽·布奈尔', 'time': '2004-10-16'}
{'name': '熔炉', 'star': '主演：孔刘,郑有美,金智英', 'time': '2011-09-22'}
{'name': '阿凡达', 'star': '主演：萨姆·沃辛顿,佐伊·索尔达娜,米歇尔·罗德里格兹', 'time': '2010-01-04'}
{'name': '千与千寻', 'star': '主演：柊瑠美,周冬雨,入野自由', 'time': '2019-06-21'}
{'name': '无敌破坏王', 'star': '主演：约翰·C·赖利,萨拉·西尔弗曼,简·林奇', 'time': '2012-11-06'}
爬取数量：100
程序结束！


```



# 爬虫数据解析模块——xpath

## 定义

```python
XPath即为XML路径语言，它是一种用来确定XML文档中某部分位置的语言，同样适用于HTML文档的检索
```

## 示例

```html
<ul class="CarList">
	<li class="bjd" id="car_001" href="http://www.bjd.com/">
        <p class="name">布加迪</p>
        <p class="model">威航</p>
        <p class="price">2500万</p>
        <p class="color">红色</p>
    </li>
    
    <li class="byd" id="car_002" href="http://www.byd.com/">
        <p class="name">比亚迪</p>
        <p class="model">秦</p>
        <p class="price">15万</p>
        <p class="color">白色</p>
    </li>
</ul>
```

## 匹配演示

```python
1、查找所有的li节点
  //li
2、获取所有汽车的名称: 所有li节点下的子节点p的值 (class属性值为name）
  //li/p[@class="name"]  
3、找比亚迪车的信息: 获取ul节点下第2个li节点的汽车信息
  //ul/li[2]                          
4、获取所有汽车的链接: ul节点下所有li子节点的href属性的值
  //ul/li/@href

# 只要涉及到条件,加 []
# 只要获取属性值,加 @
```

## 选取节点

```python
1、// ：从所有节点中查找（包括子节点和后代节点）
2、@  ：获取属性值
   # 使用场景1（属性值作为条件）
     //div[@class="movie-item-info"]
   # 使用场景2（直接获取属性值）
     //div[@class="movie-item-info"]/a/img/@src
```

## 匹配多路径（或）

```python
xpath表达式1 | xpath表达式2 | xpath表达式3
```

## 常用函数

```python
1、contains() ：匹配属性值中包含某些字符串节点
   # 查找id属性值中包含字符串 "car_" 的 li 节点
   //li[contains(@id,"car_")]
2、text() ：获取节点的文本内容
   # 查找所有汽车的价格
   //li/p[@class="price"]/text()
```

## lxml解析库

### 安装

```python
sudo pip3 install lxml
```

### 使用流程

```python
1、导模块
   from lxml import etree
2、创建解析对象
   parse_html = etree.HTML(html)
3、解析对象调用xpath
   r_list = parse_html.xpath('xpath表达式')
```

### html样本

```html
<div class="wrapper">
	<a href="/" id="channel">新浪社会</a>
	<ul id="nav">
		<li><a href="http://domestic.sina.com/" title="国内">国内</a></li>
		<li><a href="http://world.sina.com/" title="国际">国际</a></li>
		<li><a href="http://mil.sina.com/" title="军事">军事</a></li>
		<li><a href="http://photo.sina.com/" title="图片">图片</a></li>
		<li><a href="http://society.sina.com/" title="社会">社会</a></li>
		<li><a href="http://ent.sina.com/" title="娱乐">娱乐</a></li>
		<li><a href="http://tech.sina.com/" title="科技">科技</a></li>
		<li><a href="http://sports.sina.com/" title="体育">体育</a></li>
		<li><a href="http://finance.sina.com/" title="财经">财经</a></li>
		<li><a href="http://auto.sina.com/" title="汽车">汽车</a></li>
	</ul>
</div>
```

### 示例+练习

```python
from lxml import etree

html = '''
<div class="wrapper">
	<a href="/" id="channel">新浪社会</a>
	<ul id="nav">
		<li><a href="http://domestic.sina.com/" title="国内">国内</a></li>
		<li><a href="http://world.sina.com/" title="国际">国际</a></li>
		<li><a href="http://mil.sina.com/" title="军事">军事</a></li>
		<li><a href="http://photo.sina.com/" title="图片">图片</a></li>
		<li><a href="http://society.sina.com/" title="社会">社会</a></li>
		<li><a href="http://ent.sina.com/" title="娱乐">娱乐</a></li>
		<li><a href="http://tech.sina.com/" title="科技">科技</a></li>
		<li><a href="http://sports.sina.com/" title="体育">体育</a></li>
		<li><a href="http://finance.sina.com/" title="财经">财经</a></li>
		<li><a href="http://auto.sina.com/" title="汽车">汽车</a></li>
	</ul>
</div>'''
# 创建解析对象
parse_html = etree.HTML(html)
# 调用xpath返回结束,text()为文本内容
a_list = parse_html.xpath('//a/text()')
print(a_list)

# 提取所有的href的属性值
href_list = parse_html.xpath('//a/@href')
print(href)
# 提取所有href的值,不包括 / 
href_list = parse_html.xpath('//ul[@id="nav"]/li/a/@href')
print(href_list)
# 获取 图片、军事、...,不包括新浪社会
a_list = parse_html.xpath('//ul[@id="nav"]/li/a/text()')
for a in a_list:
  print(a)
```

## xpath最常使用方法

```python
1、先匹配节点对象列表
  # r_list: ['节点对象1','节点对象2']
  r_list = parse_html.xpath('基准xpath表达式')
2、遍历每个节点对象,利用节点对象继续调用 xpath
  for r in r_list:
        name = r.xpath('./xxxxxx')
        star = r.xpath('.//xxxxx')
        time = r.xpath('.//xxxxx')
```

# 案例4：猫眼电影数据抓取

```python
# -*- coding:utf-8 _*-
"""
@version:
author:安伟超
@time: 2020/09/09
@file: demo05_MaoYanMovie_xpath_OOP.py.py
@environment:virtualenv
@email:awc19930818@outlook.com
@github:https://github.com/La0bALanG
@requirement:
"""

import threading
import requests
from lxml import etree
from fake_useragent import UserAgent


"""

分析
1、基准xpath: 匹配所有电影信息的节点对象列表
    //dl[@class="board-wrapper"]/dd
    
2、遍历对象列表，依次获取每个电影信息
   for dd in dd_list:
	   电影名称 ：.//p[@class="name"]/a/@title
	   电影主演 ：.//p[@class="star"]/text()
	   上映时间 ：.//p[@class="releasetime"]/text()

"""


class MaoYanMovieXpathSpider(object):
    '''

    面向对象思路：
    1.拆分功能细节。整体程序可拆分为:
        1.发请求获得页面
        2.解析页面
        3.持久化存储(写入文件保存)
    2.结合开闭原则，封装功能方法为私有方法，对外提供统一公共接口
    3.采用单例模式：假设本爬虫程序在多个时间、不同情况下多次使用，单例模式实现只创建一个对象，提升性能避免内存占用过高。



    '''
    _instance_lock = threading.Lock()

    # 单例模式实现：__new__方法
    def __new__(cls, *args, **kwargs):
        if not hasattr(MaoYanMovieXpathSpider, '_instance'):
            with MaoYanMovieXpathSpider._instance_lock:
                if not hasattr(MaoYanMovieXpathSpider, '_instance'):
                    MaoYanMovieXpathSpider._instance = object.__new__(cls)
        return MaoYanMovieXpathSpider._instance

    def __init__(self):
        self.__url = 'https://maoyan.com/board/4?offset={}'
        self.__headers = {
            'User-Agent':UserAgent().random
        }

    #设置只读属性
    @property
    def url(self):
        return self.__url

    @property
    def headers(self):
        return self.__headers

    def __get_html(self,url):
        return requests.get(url=url,headers=self.__headers).text

    def __parse_html(self,html):
        dict = {}
        dom = etree.HTML(html)
        dd_list = dom.xpath('//dl[@class="board-wrapper"]/dd')
        for item in dd_list:
            dict['name'] = item.xpath('.//p[@class="name"]/a/@title')
            dict['star'] = item.xpath('.//p[@class="star"]/text()')
            dict['time'] = item.xpath('.//p[@class="releasetime"]/text()')
            print(dict)

    def display(self):
        for offset in range(0,91,10):
            url = self.__url.format(offset)
            self.__parse_html(self.__get_html(url))

def test():
    MaoYanMovieXpathSpider().display()

if __name__ == '__main__':
    test()
```

# 案例5：链接二手房爬取房源信息

```python
# -*- coding:utf-8 _*-
"""
@version:
author:安伟超
@time: 2020/09/09
@file: demo06_LianjiaHouseSpider_OOP.py.py
@environment:virtualenv
@email:awc19930818@outlook.com
@github:https://github.com/La0bALanG
@requirement:
"""

import threading
import requests
from lxml import etree
from fake_useragent import UserAgent

"""

实现步骤及思路：
1.确定是否为静态页面
打开二手房页面 -> 查看网页源码 -> 搜索关键字

2.确定xpath表达式

    1、基准xpath表达式(匹配每个房源信息节点列表)
       此处滚动鼠标滑轮时,li节点的class属性值会发生变化,通过查看网页源码确定xpath表达式
      //ul[@class="sellListContent"]/li[@class="clear LOGVIEWDATA LOGCLICKDATA"]
    
    2、依次遍历后每个房源信息xpath表达式
       * 名称: './/a[@data-el="region"]/text()'
       
       # 户型+面积+方位+是否精装
       info_list = './/div[@class="houseInfo"]/text()'  [0].strip().split('|')
       * 户型: info_list[1]
       * 面积: info_list[2]
       * 方位: info_list[3]
       * 精装: info_list[4]
       
    
       * 楼层: './/div[@class="positionInfo"]/text()'
       * 区域: './/div[@class="positionInfo"]/a/text()'
       * 总价: './/div[@class="totalPrice"]/span/text()'
       * 单价: './/div[@class="unitPrice"]/span/text()'

"""

class LianjiaHouseSpider(object):
    '''

    面向对象思路：
    1.拆分功能细节。整体程序可拆分为:
        1.发请求获得页面
        2.解析页面
        3.持久化存储(写入文件保存)
    2.结合开闭原则，封装功能方法为私有方法，对外提供统一公共接口
    3.采用单例模式：假设本爬虫程序在多个时间、不同情况下多次使用，单例模式实现只创建一个对象，提升性能避免内存占用过高。

    '''

    _instance_lock = threading.Lock()

    # 单例模式实现：__new__方法
    def __new__(cls, *args, **kwargs):
        if not hasattr(LianjiaHouseSpider, '_instance'):
            with LianjiaHouseSpider._instance_lock:
                if not hasattr(LianjiaHouseSpider, '_instance'):
                    LianjiaHouseSpider._instance = object.__new__(cls)
        return LianjiaHouseSpider

    def __init__(self):
        self.__url = 'https://bj.lianjia.com/ershoufang/pg{}/'
        self.__headers = {
            'User-Agent':UserAgent().random
        }

    #设置只读属性
    @property
    def url(self):
        return self.__url

    @property
    def headers(self):
        return self.__headers

    def __get_html(self,url):
        for i in range(3):
            try:
                return requests.get(url=url, headers=self.__headers,timeout=3).text
            except Exception as e:
                print('Retry')

    def __parse_html(self,html):
        dict = {}
        dom = etree.HTML(html)
        li_list = dom.xpath('//ul[@class="sellListContent"]/li[@class="clear LOGVIEWDATA LOGCLICKDATA"]')
        for item in li_list:

            #解析名称+位置
            name_list = item.xpath('.//div[@class="positionInfo"]/a[1]/text()')
            dict['name'] = name_list[0].strip() if name_list else None
            address_list = item.xpath('.//div[@class="positionInfo"]/a[2]/text()')
            item['address'] = address_list[0] if address_list else None

            #解析：户型+面积+方位+精装+楼层+年代+类型
            hlist = item.xpath('.//div[@class="houseInfo"]/text()')
            if hlist:
                # hlist: ['三室两厅','100平米','南北',...]
                hlist = hlist[0].split('|')
                dict['model'] = hlist[0].strip()
                dict['area'] = hlist[1].strip()
                dict['direct'] = hlist[2].strdict
                dict['perfect'] = hlist[3].strip()
                dict['floor'] = hlist[4].strip()
                dict['year'] = hlist[5].strip()
                dict['type'] = hlist[6].strip()
            else:
                dict['model'] = dict['area'] = dict['direct'] = dict['perfect'] = dict['floor'] = dict['year'] = dict[
                    'type'] = None

            #解析单价+总价
            total_list = item.xpath('.//div[@class="totalPrice"]/span/text()')
            dict['total'] = float(total_list[0]) * 10000 if total_list else None
            unit_list = item.xpath('.//div[@class="unitPrice"]/span/text()')
            dict['unit'] = unit_list[0][2:-4] if unit_list else None

            print(dict)

    def display(self):
        for pg in range(1,101):
            url = self.__url.format(pg)
            self.__parse_html(self.__get_html(url))

def test():
    LianjiaHouseSpider().display()

if __name__ == '__main__':
    test()
```

# 案例6：百度贴吧图片爬取

```python
# -*- coding:utf-8 _*-
"""
@version:
author:安伟超
@time: 2020/09/11
@file: demo07_BaiduTiebaSpider_OOP.py.py
@environment:virtualenv
@email:awc19930818@outlook.com
@github:https://github.com/La0bALanG
@requirement:
"""

import threading
import requests
import random
import time
from urllib import parse
from lxml import etree
from fake_useragent import UserAgent

"""

设计思路：

目标：爬取贴吧详情页图片及视频

思路：
    1.分析URL规律
        http://tieba.baidu.com/f?kw=??&pn=50
    2.三级爬取
        1.爬取第一级页面：贴吧主页(分页，多页爬取)
        2.爬取第二级页面：帖子详情页，从主页获取帖子链接
        3.爬取第三级：请求图片及视频


xpath表达式
    1、帖子链接xpath
   //div[@class="t_con cleafix"]/div/div/div/a/@href
    
    2、图片链接xpath
   //div[@class="d_post_content j_d_post_content  clearfix"]/img[@class="BDE_Image"]/@src
    
    3、视频链接xpath
   //div[@class="video_src_wrapper"]/embed/@data-video
   # 注意: 此处视频链接前端对响应内容做了处理,需要查看网页源代码来查看，复制HTML代码在线格式化



"""


class BaiduTiebaSpider(object):
    '''

        面向对象思路：
        1.拆分功能细节。整体程序可拆分为:
            1.发请求获得页面
            2.解析页面
            3.持久化存储(写入文件保存)
        2.结合开闭原则，封装功能方法为私有方法，对外提供统一公共接口
        3.采用单例模式：假设本爬虫程序在多个时间、不同情况下多次使用，单例模式实现只创建一个对象，提升性能避免内存占用过高。

        '''

    _instance_lock = threading.Lock()

    # 单例模式实现：__new__方法
    def __new__(cls, *args, **kwargs):
        if not hasattr(BaiduTiebaSpider, '_instance'):
            with BaiduTiebaSpider._instance_lock:
                if not hasattr(BaiduTiebaSpider, '_instance'):
                    BaiduTiebaSpider._instance = object.__new__(cls)
        return BaiduTiebaSpider

    def __init__(self):
        self.__url = 'http://tieba.baidu.com/f?kw={}&pn={}'
        self.__headers = {
            'User-Agent':UserAgent().random
        }

    def __get_html(self,url,headers):
        return requests.get(url=url,headers=headers).content.decode('utf-8','ignore')

    def __xpath_function(self,html,xpath_expression):
        dom = etree.HTML(html)
        return dom.xpath(xpath_expression)

    def __parse_html(self,url):
        html = self.__get_html(url)
        link_lists = self.__xpath_function(html,'//div[@class="t_con cleafix"]/div/div/div/a/@href')
        for link in link_lists:
            tie_url = 'https://tieba.baidu.com' + link
            self.__get_image(tie_url)
            time.sleep(random.randint(0,2))

    def __get_image(self,url):
        html = self.__get_html(url)
        img_lists = self.__xpath_function(html,'//div[@class="d_post_content j_d_post_content  clearfix"]/img[@class="BDE_Image"]/@src')
        for img in img_lists:
            img_bytes = self.__get_html(img).encode()
            self.__save_img(img_bytes,img)

    def __save_img(self,data,img):
        filename = img[-10:]
        with open(filename,'wb') as f:
            f.write(data)
        print('%s下载成功'%img)


    def display(self):
        name = input('请输入贴吧名称：')
        begin = int(input('请输入起始页：'))
        end = int(input('请输入终止页：'))
        kw = parse.quote(name)
        for page in range(begin,end + 1):
            pn = (page - 1) * 50
            url = self.__url.format(kw,pn)
            self.__parse_html(url)

def test():
    res = BaiduTiebaSpider()
    res.display()

if __name__ == '__main__':
    test()
```

# 案例7：电影天堂二级页面抓取电影磁力下载链接

```python
# -*- coding:utf-8 _*-
"""
@version:
author:安伟超
@time: 2020/09/07
@file: demo03_MoiveDYTT.py.py
@environment:virtualenv
@email:awc19930818@outlook.com
@github:https://github.com/La0bALanG
@requirement:把电影天堂数据存入MySQL数据库
"""

# import pymysql
import threading
import pymysql
import re
import requests
from selenium import webdriver
from lxml import etree


"""

需求：把电影天堂数据存入MySQL数据库
地址:
    一级页面：
        https://www.dytt8.net/html/gndy/index.html
    二级页面：
        https://www.dytt8.net/html/gndy/china/index.html
        https://www.dytt8.net/html/gndy/rihan/index.html
        https://www.dytt8.net/html/gndy/oumei/index.html

    二级页面分页规律：
        国产电影：
            https://www.dytt8.net/html/gndy/china/list_4_1.html
            https://www.dytt8.net/html/gndy/china/list_4_2.html
            https://www.dytt8.net/html/gndy/china/list_4_3.html
            ...
            https://www.dytt8.net/html/gndy/china/list_4_n.html
        欧美电影：
            https://www.dytt8.net/html/gndy/oumei/list_7_1.html
            https://www.dytt8.net/html/gndy/oumei/list_7_2.html
            https://www.dytt8.net/html/gndy/oumei/list_7_3.html
            https://www.dytt8.net/html/gndy/oumei/list_7_4.html
            ...
            https://www.dytt8.net/html/gndy/oumei/list_7_n.html
        日韩电影：
            https://www.dytt8.net/html/gndy/rihan/list_6_1.html
            https://www.dytt8.net/html/gndy/rihan/list_6_2.html
            https://www.dytt8.net/html/gndy/rihan/list_6_3.html
            ...
            https://www.dytt8.net/html/gndy/rihan/list_6_n.html

    总结：
        china -- 4
        rihan -- 6
        oumei -- 7
        
        https://www.dytt8.net/html/gndy/{}/list_{}_n.html
        {
            'china':'4',
            'rihan':'6',
            'oumei':'7'
        }

目标:电影名称、下载链接
分析：
*********一级页面所需数据***********
        1、提取二级页面URL
        2、分类电影详情页链接
        
*********二级页面所需数据***********
        1、提取三级页面URL
  		3、单个电影详情页链接
*********三级页面所需数据***********
        1、电影名称
  		3、对应的磁力下载链接

实现步骤:
1、发请求，拿数据
2、写xpath表达式依次解析数据
    一级页面：
        电影地区：'//div[@class="title_all"]/p/strong/text()'
        二级页面URL：'//div[@class="title_all"]/p/em/a/@href'
    二级页面：
        电影详情页URL：'//table/tbody/tr[2]/td[2]/b/a[2]/@href'
    三级页面：        
        电影名称：'//div[@class="title_all"]/h1/font/text()'
        磁力链接：'//div[@id="Zoom"]/span[@style="FONT-SIZE: 12px"]/a/@href'
3.数据持久化存储

数据库建库建表：

create database filmskydb charset utf8;
use filmskydb;
create table request_finger(
finger char(32)
)charset=utf8;
create table filmtab(
name varchar(200),
download varchar(500)
)charset=utf8;

"""

class MovieDYTTSpider(object):
    '''

    面向对象思路：
        1.拆分功能细节。整体程序可拆分为:
            1.发请求获得页面
            2.解析页面
            3.持久化存储(写入文件保存)
        2.结合开闭原则，封装功能方法为私有方法，对外提供统一公共接口
        3.采用单例模式：假设本爬虫程序在多个时间、不同情况下多次使用，单例模式实现只创建一个对象，提升性能避免内存占用过高。

    '''
    # 添加线程锁，避免实际运行过程中受多线程影响

    _instance_lock = threading.Lock()

    def __init__(self):

        #初始页面url，可获取二级页面url
        self.__init_url = 'https://www.dytt8.net/html/gndy/index.html'

        #二级页面url，可获取电影详情页url
        self.__second_url = ''

        #三级页面：电影详情页url，获取最终目标数据
        self.__movie_url = ''

        #二级页面url所需格式参数，用于拼接最终二级url
        self.__i = [4,6,7]

        #伪造请求头
        self.__headers = {
            'User-Agent': 'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/85.0.4183.83 Safari/537.36'
        }

        #使用webdriver模拟浏览器操作

        #模拟chrome浏览器操作，不打开预览页面
        chromeoptions = webdriver.ChromeOptions()
        chromeoptions.add_argument('--headless')

        #创建webdriver对象
        self.__driver = webdriver.Chrome(chrome_options=chromeoptions)

        #建立mysql链接
        self.__db = pymysql.connect(
            'localhost', 'root', '185268', 'filmskydb',
            charset='utf8'
        )
        self.__cursor = self.__db.cursor()

    #单例模式实现
    def __new__(cls, *args, **kwargs):
        if not hasattr(MovieDYTTSpider, '_instance'):
            with MovieDYTTSpider._instance_lock:
                if not hasattr(MovieDYTTSpider, '_instance'):
                    MovieDYTTSpider._instance = object.__new__(cls)
        return MovieDYTTSpider._instance

    #只读属性
    @property
    def init_url(self):
        return self.__init_url

    @property
    def second_url(self):
        return self.__second_url

    @property
    def movie_url(self):
        return self.__movie_url

    @property
    def i(self):
        return self.__i

    @property
    def headers(self):
        return self.__headers

    @property
    def driver(self):
        return self.__driver

    @property
    def db(self):
        return self.__db

    @property
    def cursor(self):
        return self.__cursor


    #-----功能代码实现--------

    #请求页面：私有方法，负责调用chrome对象获取页面并返回页面资源
    def __get_html(self,url):
        self.__driver.get(url)
        reps = self.__driver.page_source
        # print(type(reps))
        return reps

    #解析一级页面
    def __parse_first_html(self,html):
        #xpath解析
        dom = etree.HTML(html)
        movie_area = dom.xpath('//div[@class="title_all"]/p/strong/text()')
        second_html_href = dom.xpath('//div[@class="title_all"]/p/em/a/@href')
        return [movie_area.pop(),second_html_href.pop()]

    #解析二级页面
    def __parse_second_html(self,html):
        dom = etree.HTML(html)
        movie_list = dom.xpath('//table/tbody/tr[2]/td[2]/b/a[2]/@href')
        return movie_list

    #解析三级页面
    def __parse_third_html(self,html):
        dom = etree.HTML(html)
        movie_name = dom.xpath('//div[@class="title_all"]/h1/font/text()')
        movie_marget = dom.xpath('//div[@id="Zoom"]/span[@style="FONT-SIZE: 12px"]/a/@href')
        return zip(movie_name,movie_marget)

    #写入数据库：持久化存储
    def __save_html(self,name,marget):
        ins = 'insert into filmtab values(%s,%s)'
        self.__cursor.execute(ins,name,marget)
        self.__db.commit()

    #公共接口：功能整合，类外返回数据
    def display(self,num):

        #1.请求一级页面并解析数据，获得二级页面所需URL(部分，还要进行拼接)
        res = self.__parse_first_html(self.__get_html(self.__init_url))

        #遍历一级页面响应数据和url所需参数的参数列表
        for (sec,i) in zip(res[1],self.__i):

            #模拟循环多页进行爬取，num表示页数
            for j in range(1, num + 1):
                #拼接出所需的二级页面的URL
                self.__second_url = 'https://www.dytt8.net' + sec[0:-10] + 'list_{}_{}.html'.format(i,j)
                #2.请求2级页面并解析数据，获得电影详情页最终URL(部分，还要进行拼接)
                sec_data = self.__parse_second_html(self.__get_html(self.__second_url))
                #遍历二级页面响应内容
                for m_url in sec_data:
                    #3.拼接电影详情页最终URL
                    self.__movie_url = 'https://www.dytt8.net' + m_url
                    #请求最终电影详情页，获得电影名称及其对应的迅雷下载磁力链接码
                    movie_data = self.__parse_third_html(self.__get_html(self.__movie_url))
                    #遍历电影名称及磁力链接
                    for (name,marget) in movie_data:
                        #调用save方法将数据写入数据库
                        self.__save_html(name,marget)

def test():
    num = int(input('您想爬多少页的内容，请输入>>>:'))
    MovieDYTTSpider().display(num)

if __name__ == '__main__':
    test()
```



# 爬虫数据解析模块——BeautifulSoup4

## Bs4基本介绍及用法

### 基本介绍

BeautifulSoup4，简称bs4，是一个可以从HTML或XML文档中提取数据的Python库.实现对HTML或XML文档解析功能的库有很多，前文我们已经学习使用了很多库，比如最最基本的re正则表达式，它是最基本的HTML或XML文档解析库，特点就是依托正则表达式语法，灵活且高效；还有xpath解析，依托DOM(document object model,文档对象模型)节点对象的解析库，功能也是非常强大。但这两个常见的基本解析库，其具有一个共同的特点：具有其独特的解析语法，两者无一不需要先去学习其复杂的解析语法，再去学习使用解析库解析HTML文档。而bs4的优势就在于没有固定繁杂的解析语法，一切均依托内置的转换器实现功能，简单易上手，同时大幅提升效率，对新手小白极其友好。

### BeautifulSoup4的下载及安装

无论是在windows环境下还是Linux、Unix(mac)下，下载安装的方式都是统一的，即都通过pip包管理工具进行安装。安装命令如下(需要先安装pip包管理工具，不会安装的前文已经说到，自行阅读操作安装一下)：

```python
pip install beautifulsoup4 -i https://pypi.douban.com/simple
```

### BeautifulSoup4模块导入

```python
form bs4 import BeautifulSoup
```

### bs4解析库

BeautifulSoup默认支持Python的标准HTML解析库，但是它也支持一些第三方的解析库：

| 序号 | 解析库          | 使用方法                           | 优势                            | 劣势                  |
| ---- | --------------- | ---------------------------------- | ------------------------------- | --------------------- |
| 1    | Python标准库    | BeautifulSoup(html,’html.parser’)  | Python内置标准库；执行速度快    | 容错能力较差          |
| 2    | lxml HTML解析库 | BeautifulSoup(html,’lxml’)         | 速度快；容错能力强              | 需要安装，需要C语言库 |
| 3    | lxml XML解析库  | BeautifulSoup(html,[‘lxml’,’xml’]) | 速度快；容错能力强；支持XML格式 | 需要C语言库           |
| 4    | htm5lib解析库   | BeautifulSoup(html,’htm5llib’)     | 以浏览器方式解析，最好的容错性  | 速度慢                |

### 解析器安装

Beautiful Soup支持Python标准库中的HTML解析器,还支持一些第三方的解析器,其中一个是 [lxml](http://lxml.de/) .根据操作系统不同,可以选择下列方法来安装lxml:

```python
apt-get install Python-lxml

easy_install lxml

pip install lxml
```

另一个可供选择的解析器是纯Python实现的 [html5lib](http://code.google.com/p/html5lib/) , html5lib的解析方式与浏览器相同,可以选择下列方法来安装html5lib:

```python
apt-get install Python-html5lib

easy_install html5lib

pip install html5lib
```

推荐使用lxml作为解析器,因为效率更高. 在Python2.7.3之前的版本和Python3中3.2.2之前的版本,必须安装lxml或html5lib, 因为那些Python版本的标准库中内置的HTML解析方法不够稳定.

提示: 如果一段HTML或XML文档格式不正确的话,那么在不同的解析器中返回的结果可能是不一样的.

### 基本用法

```python
#导包
from bs4 import BeautifulSoup

#文档对象 = BeautifulSoup(str[doc],[parserMethod])
soup = BeautifulSoup(open("index.html"),'html.parser')#传入文件句柄

soup = BeautifulSoup("<html>data</html>",'lxml')#传入字符串
```

## bs4对象种类——4大常用对象

Beautiful Soup将复杂HTML文档转换成一个复杂的树形结构,每个节点都是Python对象,所有对象可以归纳为4种:

- Tag
- NavigableString
- BeautifulSoup
- Comment

### Tag对象

Tag对象与XML或HTML原生文档中的tag相同:

```python
soup = BeautifulSoup('<b class="boldest">Extremely bold</b>')
tag = soup.b
type(tag)
# <class 'bs4.element.Tag'>
```

Tag有很多方法和属性,其中最重要的属性是: name和attributes

#### name属性

每个tag都有自己的名字,通过.name获取：

```python
tag.name
# u'b'
```

如果改变了tag的name,那将影响所有通过当前Beautiful Soup对象生成的HTML文档:

```python
tag.name = "blockquote"
tag
# <blockquote class="boldest">Extremely bold</blockquote>
```

#### attributes属性

一个tag可能有很多个属性. tag `<b class="boldest">`有一个 “class” 的属性,值为 “boldest” . tag的属性的操作方法与字典相同:

```python
tag['class']
# u'boldest'
```

也可以直接”点”取属性, 比如: `.attrs` :

```python
tag.attrs
# {u'class': u'boldest'}
```

tag的属性可以被添加,删除或修改. 再说一次, tag的属性操作方法与字典一样:

```python
tag['class'] = 'verybold'
tag['id'] = 1
tag
# <blockquote class="verybold" id="1">Extremely bold</blockquote>

del tag['class']
del tag['id']
tag
# <blockquote>Extremely bold</blockquote>

tag['class']
# KeyError: 'class'
print(tag.get('class'))
# None
```

#### 多值属性

HTML 4定义了一系列可以包含多个值的属性.在HTML5中移除了一些,却增加更多.最常见的多值的属性是 class (一个tag可以有多个CSS的class). 还有一些属性 `rel` , `rev` , `accept-charset` , `headers` , `accesskey` . 在Beautiful Soup中多值属性的返回类型是list:

```python
css_soup = BeautifulSoup('<p class="body strikeout"></p>')
css_soup.p['class']
# ["body", "strikeout"]

css_soup = BeautifulSoup('<p class="body"></p>')
css_soup.p['class']
# ["body"]
```

如果某个属性看起来好像有多个值,但在任何版本的HTML定义中都没有被定义为多值属性,那么Beautiful Soup会将这个属性作为字符串返回:

```python
id_soup = BeautifulSoup('<p id="my id"></p>')
id_soup.p['id']
# 'my id'
```

将tag转换成字符串时,多值属性会合并为一个值:

```python
rel_soup = BeautifulSoup('<p>Back to the <a rel="index">homepage</a></p>')
rel_soup.a['rel']
# ['index']
rel_soup.a['rel'] = ['index', 'contents']
print(rel_soup.p)
# <p>Back to the <a rel="index contents">homepage</a></p>
```

如果转换的文档是XML格式,那么tag中不包含多值属性:

```python
xml_soup = BeautifulSoup('<p class="body strikeout"></p>', 'xml')
xml_soup.p['class']
# u'body strikeout'
```

### NavigableString对象(可遍历字符串)

字符串常被包含在tag内.Beautiful Soup用 `NavigableString` 类来包装tag中的字符串:

```python
tag.string
# u'Extremely bold'
type(tag.string)
# <class 'bs4.element.NavigableString'>
```

一个 `NavigableString` 字符串与Python中的Unicode字符串相同,并且还支持包含在 [遍历文档树](https://beautifulsoup.readthedocs.io/zh_CN/v4.4.0/#id18) 和 [搜索文档树](https://beautifulsoup.readthedocs.io/zh_CN/v4.4.0/#id27) 中的一些特性. 通过 `unicode()` 方法可以直接将 `NavigableString` 对象转换成Unicode字符串:

```python
unicode_string = unicode(tag.string)
unicode_string
# u'Extremely bold'
type(unicode_string)
# <type 'unicode'>
```

tag中包含的字符串不能编辑,但是可以被替换成其它的字符串,用 [replace_with()](https://beautifulsoup.readthedocs.io/zh_CN/v4.4.0/#replace-with) 方法:

```python
tag.string.replace_with("No longer bold")
tag
# <blockquote>No longer bold</blockquote>
```

`NavigableString` 对象支持 [遍历文档树](https://beautifulsoup.readthedocs.io/zh_CN/v4.4.0/#id18) 和 [搜索文档树](https://beautifulsoup.readthedocs.io/zh_CN/v4.4.0/#id27) 中定义的大部分属性, 并非全部.尤其是,一个字符串不能包含其它内容(tag能够包含字符串或是其它tag),字符串不支持 `.contents` 或 `.string` 属性或 `find()` 方法.

如果想在Beautiful Soup之外使用 `NavigableString` 对象,需要调用 `unicode()` 方法,将该对象转换成普通的Unicode字符串,否则就算Beautiful Soup已方法已经执行结束,该对象的输出也会带有对象的引用地址.这样会浪费内存.

### BeautifulSoup对象

`BeautifulSoup` 对象表示的是一个文档的全部内容.大部分时候,可以把它当作 `Tag` 对象,它支持 [遍历文档树](https://beautifulsoup.readthedocs.io/zh_CN/v4.4.0/#id18) 和 [搜索文档树](https://beautifulsoup.readthedocs.io/zh_CN/v4.4.0/#id27) 中描述的大部分的方法.

因为 `BeautifulSoup` 对象并不是真正的HTML或XML的tag,所以它没有name和attribute属性.但有时查看它的 `.name` 属性是很方便的,所以 `BeautifulSoup` 对象包含了一个值为 “[document]” 的特殊属性 `.name`

```python
soup.name
# u'[document]'
```

### Comment对象(文档注释)

`Tag` , `NavigableString` , `BeautifulSoup` 几乎覆盖了html和xml中的所有内容,但是还有一些特殊对象.容易让人担心的内容是文档的注释部分:

```python
markup = "<b><!--Hey, buddy. Want to buy a used parser?--></b>"
soup = BeautifulSoup(markup)
comment = soup.b.string
type(comment)
# <class 'bs4.element.Comment'>
```

`Comment` 对象是一个特殊类型的 `NavigableString` 对象:

```python
comment
# u'Hey, buddy. Want to buy a used parser'
```

但是当它出现在HTML文档中时, `Comment` 对象会使用特殊的格式输出:

```python
print(soup.b.prettify())
# <b>
#  <!--Hey, buddy. Want to buy a used parser?-->
# </b>
```

Beautiful Soup中定义的其它类型都可能会出现在XML的文档中: `CData` , `ProcessingInstruction` , `Declaration` , `Doctype` .与 `Comment` 对象类似,这些类都是 `NavigableString` 的子类,只是添加了一些额外的方法的字符串独享.下面是用CDATA来替代注释的例子:

```python
from bs4 import CData
cdata = CData("A CDATA block")
comment.replace_with(cdata)

print(soup.b.prettify())
# <b>
#  <![CDATA[A CDATA block]]>
# </b>
```

## 遍历文档树

还拿”爱丽丝梦游仙境”的文档来做例子:

```
html_doc = """
<html><head><title>The Dormouse's story</title></head>
    <body>
<p class="title"><b>The Dormouse's story</b></p>

<p class="story">Once upon a time there were three little sisters; and their names were
<a href="http://example.com/elsie" class="sister" id="link1">Elsie</a>,
<a href="http://example.com/lacie" class="sister" id="link2">Lacie</a> and
<a href="http://example.com/tillie" class="sister" id="link3">Tillie</a>;
and they lived at the bottom of a well.</p>

<p class="story">...</p>
"""

from bs4 import BeautifulSoup
soup = BeautifulSoup(html_doc, 'html.parser')
```

通过这段例子来演示怎样从文档的一段内容找到另一段内容

### 子节点

一个Tag可能包含多个字符串或其它的Tag,这些都是这个Tag的子节点.Beautiful Soup提供了许多操作和遍历子节点的属性.

注意: Beautiful Soup中字符串节点不支持这些属性,因为字符串没有子节点

#### tag的名字

操作文档树最简单的方法就是告诉它你想获取的tag的name.如果想获取 <head> 标签,只要用 `soup.head` :

```python
soup.head
# <head><title>The Dormouse's story</title></head>

soup.title
# <title>The Dormouse's story</title>
```

这是个获取tag的小窍门,可以在文档树的tag中多次调用这个方法.下面的代码可以获取<body>标签中的第一个<b>标签:

```python
soup.body.b
# <b>The Dormouse's story</b>
```

通过点取属性的方式只能获得当前名字的第一个tag:

```python
soup.a
# <a class="sister" href="http://example.com/elsie" id="link1">Elsie</a>
```

如果想要得到所有的<a>标签,或是通过名字得到比一个tag更多的内容的时候,就需要用到 Searching the tree 中描述的方法,比如: find_all()

```python
soup.find_all('a')
# [<a class="sister" href="http://example.com/elsie" id="link1">Elsie</a>,
#  <a class="sister" href="http://example.com/lacie" id="link2">Lacie</a>,
#  <a class="sister" href="http://example.com/tillie" id="link3">Tillie</a>]
```

#### .contents 和 .children

tag的 `.contents` 属性可以将tag的子节点以列表的方式输出:

```
head_tag = soup.head
head_tag
# <head><title>The Dormouse's story</title></head>

head_tag.contents
[<title>The Dormouse's story</title>]

title_tag = head_tag.contents[0]
title_tag
# <title>The Dormouse's story</title>
title_tag.contents
# [u'The Dormouse's story']
```

`BeautifulSoup` 对象本身一定会包含子节点,也就是说<html>标签也是 `BeautifulSoup` 对象的子节点:

```python
len(soup.contents)
# 1
soup.contents[0].name
# u'html'
```

字符串没有 `.contents` 属性,因为字符串没有子节点:

```python
text = title_tag.contents[0]
text.contents
# AttributeError: 'NavigableString' object has no attribute 'contents'
```

通过tag的 `.children` 生成器,可以对tag的子节点进行循环:

```python
for child in title_tag.children:
    print(child)
    # The Dormouse's story
```

#### .descendants

`.contents` 和 `.children` 属性仅包含tag的直接子节点.例如,<head>标签只有一个直接子节点<title>

```python
head_tag.contents
# [<title>The Dormouse's story</title>]
```

但是<title>标签也包含一个子节点:字符串 “The Dormouse’s story”,这种情况下字符串 “The Dormouse’s story”也属于<head>标签的子孙节点. `.descendants` 属性可以对所有tag的子孙节点进行递归循环 [[5\]](https://beautifulsoup.readthedocs.io/zh_CN/v4.4.0/#id92) :

```python
for child in head_tag.descendants:
    print(child)
    # <title>The Dormouse's story</title>
    # The Dormouse's story
```

上面的例子中, <head>标签只有一个子节点,但是有2个子孙节点:<head>节点和<head>的子节点, `BeautifulSoup` 有一个直接子节点(<html>节点),却有很多子孙节点:

```python
len(list(soup.children))
# 1
len(list(soup.descendants))
# 25
```

#### .string

如果tag只有一个 `NavigableString` 类型子节点,那么这个tag可以使用 `.string` 得到子节点:

```python
title_tag.string
# u'The Dormouse's story'
```

如果一个tag仅有一个子节点,那么这个tag也可以使用 `.string` 方法,输出结果与当前唯一子节点的 `.string` 结果相同:

```python
head_tag.contents
# [<title>The Dormouse's story</title>]

head_tag.string
# u'The Dormouse's story'
```

如果tag包含了多个子节点,tag就无法确定 `.string` 方法应该调用哪个子节点的内容, `.string` 的输出结果是 `None` :

```python
print(soup.html.string)
# None
```

#### .strings 和 stripped_strings

如果tag中包含多个字符串 [[2\]](https://beautifulsoup.readthedocs.io/zh_CN/v4.4.0/#id89) ,可以使用 `.strings` 来循环获取:

```python
for string in soup.strings:
    print(repr(string))
    # u"The Dormouse's story"
    # u'\n\n'
    # u"The Dormouse's story"
    # u'\n\n'
    # u'Once upon a time there were three little sisters; and their names were\n'
    # u'Elsie'
    # u',\n'
    # u'Lacie'
    # u' and\n'
    # u'Tillie'
    # u';\nand they lived at the bottom of a well.'
    # u'\n\n'
    # u'...'
    # u'\n'
```

输出的字符串中可能包含了很多空格或空行,使用 `.stripped_strings` 可以去除多余空白内容:

```python
for string in soup.stripped_strings:
    print(repr(string))
    # u"The Dormouse's story"
    # u"The Dormouse's story"
    # u'Once upon a time there were three little sisters; and their names were'
    # u'Elsie'
    # u','
    # u'Lacie'
    # u'and'
    # u'Tillie'
    # u';\nand they lived at the bottom of a well.'
    # u'...'
```

全部是空格的行会被忽略掉,段首和段末的空白会被删除

### 父节点

继续分析文档树,每个tag或字符串都有父节点:被包含在某个tag中

#### .parent

通过 `.parent` 属性来获取某个元素的父节点.在例子“爱丽丝”的文档中,<head>标签是<title>标签的父节点:

```python
title_tag = soup.title
title_tag
# <title>The Dormouse's story</title>
title_tag.parent
# <head><title>The Dormouse's story</title></head>
```

文档title的字符串也有父节点:<title>标签

```python
title_tag.string.parent
# <title>The Dormouse's story</title>
```

文档的顶层节点比如<html>的父节点是 `BeautifulSoup` 对象:

```python
html_tag = soup.html
type(html_tag.parent)
# <class 'bs4.BeautifulSoup'>
```

`BeautifulSoup` 对象的 `.parent` 是None:

```python
print(soup.parent)
# None
```

#### .parents

通过元素的 `.parents` 属性可以递归得到元素的所有父辈节点,下面的例子使用了 `.parents` 方法遍历了<a>标签到根节点的所有节点.

```python
link = soup.a
link
# <a class="sister" href="http://example.com/elsie" id="link1">Elsie</a>
for parent in link.parents:
    if parent is None:
        print(parent)
    else:
        print(parent.name)
# p
# body
# html
# [document]
# None
```

### 兄弟节点

看一段简单的例子:

```python
sibling_soup = BeautifulSoup("<a><b>text1</b><c>text2</c></b></a>")
print(sibling_soup.prettify())
# <html>
#  <body>
#   <a>
#    <b>
#     text1
#    </b>
#    <c>
#     text2
#    </c>
#   </a>
#  </body>
# </html>
```

因为<b>标签和<c>标签是同一层:他们是同一个元素的子节点,所以<b>和<c>可以被称为兄弟节点.一段文档以标准格式输出时,兄弟节点有相同的缩进级别.在代码中也可以使用这种关系.

#### .next_sibling 和 .previous_sibling

在文档树中,使用 `.next_sibling` 和 `.previous_sibling` 属性来查询兄弟节点:

```python
sibling_soup.b.next_sibling
# <c>text2</c>

sibling_soup.c.previous_sibling
# <b>text1</b>
```

<b>标签有 `.next_sibling` 属性,但是没有 `.previous_sibling` 属性,因为<b>标签在同级节点中是第一个.同理,<c>标签有 `.previous_sibling` 属性,却没有 `.next_sibling` 属性:

```python
print(sibling_soup.b.previous_sibling)
# None
print(sibling_soup.c.next_sibling)
# None
```

例子中的字符串“text1”和“text2”不是兄弟节点,因为它们的父节点不同:

```python
sibling_soup.b.string
# u'text1'

print(sibling_soup.b.string.next_sibling)
# None
```

实际文档中的tag的 `.next_sibling` 和 `.previous_sibling` 属性通常是字符串或空白. 看看“爱丽丝”文档:

```python
<a href="http://example.com/elsie" class="sister" id="link1">Elsie</a>
<a href="http://example.com/lacie" class="sister" id="link2">Lacie</a>
<a href="http://example.com/tillie" class="sister" id="link3">Tillie</a>
```

如果以为第一个<a>标签的 `.next_sibling` 结果是第二个<a>标签,那就错了,真实结果是第一个<a>标签和第二个<a>标签之间的顿号和换行符:

```python
link = soup.a
link
# <a class="sister" href="http://example.com/elsie" id="link1">Elsie</a>

link.next_sibling
# u',\n'
```

第二个<a>标签是顿号的 `.next_sibling` 属性:

```python
link.next_sibling.next_sibling
# <a class="sister" href="http://example.com/lacie" id="link2">Lacie</a>
```

#### .next_siblings 和 .previous_siblings

通过 `.next_siblings` 和 `.previous_siblings` 属性可以对当前节点的兄弟节点迭代输出:

```python
for sibling in soup.a.next_siblings:
    print(repr(sibling))
    # u',\n'
    # <a class="sister" href="http://example.com/lacie" id="link2">Lacie</a>
    # u' and\n'
    # <a class="sister" href="http://example.com/tillie" id="link3">Tillie</a>
    # u'; and they lived at the bottom of a well.'
    # None

for sibling in soup.find(id="link3").previous_siblings:
    print(repr(sibling))
    # ' and\n'
    # <a class="sister" href="http://example.com/lacie" id="link2">Lacie</a>
    # u',\n'
    # <a class="sister" href="http://example.com/elsie" id="link1">Elsie</a>
    # u'Once upon a time there were three little sisters; and their names were\n'
    # None
```

### 回退和前进

看一下“爱丽丝” 文档:

```python
<html><head><title>The Dormouse's story</title></head>
<p class="title"><b>The Dormouse's story</b></p>
```

HTML解析器把这段字符串转换成一连串的事件: “打开<html>标签”,”打开一个<head>标签”,”打开一个<title>标签”,”添加一段字符串”,”关闭<title>标签”,”打开<p>标签”,等等.Beautiful Soup提供了重现解析器初始化过程的方法.

#### .next_element 和 .previous_element

`.next_element` 属性指向解析过程中下一个被解析的对象(字符串或tag),结果可能与 `.next_sibling` 相同,但通常是不一样的.

这是“爱丽丝”文档中最后一个<a>标签,它的 `.next_sibling` 结果是一个字符串,因为当前的解析过程 [[2\]](https://beautifulsoup.readthedocs.io/zh_CN/v4.4.0/#id89) 因为当前的解析过程因为遇到了<a>标签而中断了:

```python
last_a_tag = soup.find("a", id="link3")
last_a_tag
# <a class="sister" href="http://example.com/tillie" id="link3">Tillie</a>

last_a_tag.next_sibling
# '; and they lived at the bottom of a well.'
```

但这个<a>标签的 `.next_element` 属性结果是在<a>标签被解析之后的解析内容,不是<a>标签后的句子部分,应该是字符串”Tillie”:

```python
last_a_tag.next_element
# u'Tillie'
```

这是因为在原始文档中,字符串“Tillie” 在分号前出现,解析器先进入<a>标签,然后是字符串“Tillie”,然后关闭</a>标签,然后是分号和剩余部分.分号与<a>标签在同一层级,但是字符串“Tillie”会被先解析.

`.previous_element` 属性刚好与 `.next_element` 相反,它指向当前被解析的对象的前一个解析对象:

```python
last_a_tag.previous_element
# u' and\n'
last_a_tag.previous_element.next_element
# <a class="sister" href="http://example.com/tillie" id="link3">Tillie</a>
```

#### .next_elements 和 .previous_elements

通过 `.next_elements` 和 `.previous_elements` 的迭代器就可以向前或向后访问文档的解析内容,就好像文档正在被解析一样:

```python
for element in last_a_tag.next_elements:
    print(repr(element))
# u'Tillie'
# u';\nand they lived at the bottom of a well.'
# u'\n\n'
# <p class="story">...</p>
# u'...'
# u'\n'
# None
```

## 搜索文档树

Beautiful Soup定义了很多搜索方法,这里着重介绍2个: `find()` 和 `find_all()` .其它方法的参数和用法类似,请读者举一反三.

再以“爱丽丝”文档作为例子:

```python
html_doc = """
<html><head><title>The Dormouse's story</title></head>
<body>
<p class="title"><b>The Dormouse's story</b></p>

<p class="story">Once upon a time there were three little sisters; and their names were
<a href="http://example.com/elsie" class="sister" id="link1">Elsie</a>,
<a href="http://example.com/lacie" class="sister" id="link2">Lacie</a> and
<a href="http://example.com/tillie" class="sister" id="link3">Tillie</a>;
and they lived at the bottom of a well.</p>

<p class="story">...</p>
"""

from bs4 import BeautifulSoup
soup = BeautifulSoup(html_doc, 'html.parser')
```

使用 `find_all()` 类似的方法可以查找到想要查找的文档内容.

### 过滤器

介绍 `find_all()` 方法前,先介绍一下过滤器的类型 [[3\]](https://beautifulsoup.readthedocs.io/zh_CN/v4.4.0/#id90) ,这些过滤器贯穿整个搜索的API.过滤器可以被用在tag的name中,节点的属性中,字符串中或他们的混合中.

#### 字符串

最简单的过滤器是字符串.在搜索方法中传入一个字符串参数,Beautiful Soup会查找与字符串完整匹配的内容,下面的例子用于查找文档中所有的<b>标签:

```python
soup.find_all('b')
# [<b>The Dormouse's story</b>]
```

如果传入字节码参数,Beautiful Soup会当作UTF-8编码,可以传入一段Unicode 编码来避免Beautiful Soup解析编码出错

#### 正则表达式

如果传入正则表达式作为参数,Beautiful Soup会通过正则表达式的 `match()` 来匹配内容.下面例子中找出所有以b开头的标签,这表示<body>和<b>标签都应该被找到:

```python
import re
for tag in soup.find_all(re.compile("^b")):
    print(tag.name)
# body
# b
```

下面代码找出所有名字中包含”t”的标签:

```python
for tag in soup.find_all(re.compile("t")):
    print(tag.name)
# html
# title
```

#### 列表

如果传入列表参数,Beautiful Soup会将与列表中任一元素匹配的内容返回.下面代码找到文档中所有<a>标签和<b>标签:

```python
soup.find_all(["a", "b"])
# [<b>The Dormouse's story</b>,
#  <a class="sister" href="http://example.com/elsie" id="link1">Elsie</a>,
#  <a class="sister" href="http://example.com/lacie" id="link2">Lacie</a>,
#  <a class="sister" href="http://example.com/tillie" id="link3">Tillie</a>]
```

#### True

`True` 可以匹配任何值,下面代码查找到所有的tag,但是不会返回字符串节点

```python
for tag in soup.find_all(True):
    print(tag.name)
# html
# head
# title
# body
# p
# b
# p
# a
# a
# a
# p
```

#### 方法

如果没有合适过滤器,那么还可以定义一个方法,方法只接受一个元素参数 [[4\]](https://beautifulsoup.readthedocs.io/zh_CN/v4.4.0/#id91) ,如果这个方法返回 `True` 表示当前元素匹配并且被找到,如果不是则反回 `False`

下面方法校验了当前元素,如果包含 `class` 属性却不包含 `id` 属性,那么将返回 `True`:

```python
def has_class_but_no_id(tag):
    return tag.has_attr('class') and not tag.has_attr('id')
```

将这个方法作为参数传入 `find_all()` 方法,将得到所有<p>标签:

```python
soup.find_all(has_class_but_no_id)
# [<p class="title"><b>The Dormouse's story</b></p>,
#  <p class="story">Once upon a time there were...</p>,
#  <p class="story">...</p>]
```

返回结果中只有<p>标签没有<a>标签,因为<a>标签还定义了”id”,没有返回<html>和<head>,因为<html>和<head>中没有定义”class”属性.

通过一个方法来过滤一类标签属性的时候, 这个方法的参数是要被过滤的属性的值, 而不是这个标签. 下面的例子是找出 `href` 属性不符合指定正则的 `a` 标签.

```python
def not_lacie(href):
        return href and not re.compile("lacie").search(href)
soup.find_all(href=not_lacie)
# [<a class="sister" href="http://example.com/elsie" id="link1">Elsie</a>,
#  <a class="sister" href="http://example.com/tillie" id="link3">Tillie</a>]
```

标签过滤方法可以使用复杂方法. 下面的例子可以过滤出前后都有文字的标签.

```python
from bs4 import NavigableString
def surrounded_by_strings(tag):
    return (isinstance(tag.next_element, NavigableString)
            and isinstance(tag.previous_element, NavigableString))

for tag in soup.find_all(surrounded_by_strings):
    print tag.name
# p
# a
# a
# a
# p
```

现在来了解一下搜索方法的细节.

### find_all()

find_all( [name](https://beautifulsoup.readthedocs.io/zh_CN/v4.4.0/#id35) , [attrs](https://beautifulsoup.readthedocs.io/zh_CN/v4.4.0/#css) , [recursive](https://beautifulsoup.readthedocs.io/zh_CN/v4.4.0/#recursive) , [string](https://beautifulsoup.readthedocs.io/zh_CN/v4.4.0/#id36) , [**kwargs](https://beautifulsoup.readthedocs.io/zh_CN/v4.4.0/#keyword) )

`find_all()` 方法搜索当前tag的所有tag子节点,并判断是否符合过滤器的条件.这里有几个例子:

```python
soup.find_all("title")
# [<title>The Dormouse's story</title>]

soup.find_all("p", "title")
# [<p class="title"><b>The Dormouse's story</b></p>]

soup.find_all("a")
# [<a class="sister" href="http://example.com/elsie" id="link1">Elsie</a>,
#  <a class="sister" href="http://example.com/lacie" id="link2">Lacie</a>,
#  <a class="sister" href="http://example.com/tillie" id="link3">Tillie</a>]

soup.find_all(id="link2")
# [<a class="sister" href="http://example.com/lacie" id="link2">Lacie</a>]

import re
soup.find(string=re.compile("sisters"))
# u'Once upon a time there were three little sisters; and their names were\n'
```

有几个方法很相似,还有几个方法是新的,参数中的 `string` 和 `id` 是什么含义? 为什么 `find_all("p", "title")` 返回的是CSS Class为”title”的<p>标签? 我们来仔细看一下 `find_all()` 的参数

#### name 参数

`name` 参数可以查找所有名字为 `name` 的tag,字符串对象会被自动忽略掉.

简单的用法如下:

```python
soup.find_all("title")
# [<title>The Dormouse's story</title>]
```

重申: 搜索 `name` 参数的值可以使任一类型的 [过滤器](https://beautifulsoup.readthedocs.io/zh_CN/v4.4.0/#id28) ,字符窜,正则表达式,列表,方法或是 `True` .

#### keyword 参数

如果一个指定名字的参数不是搜索内置的参数名,搜索时会把该参数当作指定名字tag的属性来搜索,如果包含一个名字为 `id` 的参数,Beautiful Soup会搜索每个tag的”id”属性.

```python
soup.find_all(id='link2')
# [<a class="sister" href="http://example.com/lacie" id="link2">Lacie</a>]
```

如果传入 `href` 参数,Beautiful Soup会搜索每个tag的”href”属性:

```python
soup.find_all(href=re.compile("elsie"))
# [<a class="sister" href="http://example.com/elsie" id="link1">Elsie</a>]
```

搜索指定名字的属性时可以使用的参数值包括 [字符串](https://beautifulsoup.readthedocs.io/zh_CN/v4.4.0/#id30) , [正则表达式](https://beautifulsoup.readthedocs.io/zh_CN/v4.4.0/#id31) , [列表](https://beautifulsoup.readthedocs.io/zh_CN/v4.4.0/#id32), [True](https://beautifulsoup.readthedocs.io/zh_CN/v4.4.0/#true) .

下面的例子在文档树中查找所有包含 `id` 属性的tag,无论 `id` 的值是什么:

```python
soup.find_all(id=True)
# [<a class="sister" href="http://example.com/elsie" id="link1">Elsie</a>,
#  <a class="sister" href="http://example.com/lacie" id="link2">Lacie</a>,
#  <a class="sister" href="http://example.com/tillie" id="link3">Tillie</a>]
```

使用多个指定名字的参数可以同时过滤tag的多个属性:

```python
soup.find_all(href=re.compile("elsie"), id='link1')
# [<a class="sister" href="http://example.com/elsie" id="link1">three</a>]
```

有些tag属性在搜索不能使用,比如HTML5中的 data-* 属性:

```python
data_soup = BeautifulSoup('<div data-foo="value">foo!</div>')
data_soup.find_all(data-foo="value")
# SyntaxError: keyword can't be an expression
```

但是可以通过 `find_all()` 方法的 `attrs` 参数定义一个字典参数来搜索包含特殊属性的tag:

```python
data_soup.find_all(attrs={"data-foo": "value"})
# [<div data-foo="value">foo!</div>]
```

#### 按CSS搜索

按照CSS类名搜索tag的功能非常实用,但标识CSS类名的关键字 `class` 在Python中是保留字,使用 `class` 做参数会导致语法错误.从Beautiful Soup的4.1.1版本开始,可以通过 `class_` 参数搜索有指定CSS类名的tag:

```python
soup.find_all("a", class_="sister")
# [<a class="sister" href="http://example.com/elsie" id="link1">Elsie</a>,
#  <a class="sister" href="http://example.com/lacie" id="link2">Lacie</a>,
#  <a class="sister" href="http://example.com/tillie" id="link3">Tillie</a>]
```

`class_` 参数同样接受不同类型的 `过滤器` ,字符串,正则表达式,方法或 `True` :

```python
soup.find_all(class_=re.compile("itl"))
# [<p class="title"><b>The Dormouse's story</b></p>]

def has_six_characters(css_class):
    return css_class is not None and len(css_class) == 6

soup.find_all(class_=has_six_characters)
# [<a class="sister" href="http://example.com/elsie" id="link1">Elsie</a>,
#  <a class="sister" href="http://example.com/lacie" id="link2">Lacie</a>,
#  <a class="sister" href="http://example.com/tillie" id="link3">Tillie</a>]
```

tag的 `class` 属性是 [多值属性](https://beautifulsoup.readthedocs.io/zh_CN/v4.4.0/#id15) .按照CSS类名搜索tag时,可以分别搜索tag中的每个CSS类名:

```python
css_soup = BeautifulSoup('<p class="body strikeout"></p>')
css_soup.find_all("p", class_="strikeout")
# [<p class="body strikeout"></p>]

css_soup.find_all("p", class_="body")
# [<p class="body strikeout"></p>]
```

搜索 `class` 属性时也可以通过CSS值完全匹配:

```python
css_soup.find_all("p", class_="body strikeout")
# [<p class="body strikeout"></p>]
```

完全匹配 `class` 的值时,如果CSS类名的顺序与实际不符,将搜索不到结果:

```python
soup.find_all("a", attrs={"class": "sister"})
# [<a class="sister" href="http://example.com/elsie" id="link1">Elsie</a>,
#  <a class="sister" href="http://example.com/lacie" id="link2">Lacie</a>,
#  <a class="sister" href="http://example.com/tillie" id="link3">Tillie</a>]
```

#### `string` 参数

通过 `string` 参数可以搜搜文档中的字符串内容.与 `name` 参数的可选值一样, `string` 参数接受 [字符串](https://beautifulsoup.readthedocs.io/zh_CN/v4.4.0/#id30) , [正则表达式](https://beautifulsoup.readthedocs.io/zh_CN/v4.4.0/#id31) , [列表](https://beautifulsoup.readthedocs.io/zh_CN/v4.4.0/#id32), [True](https://beautifulsoup.readthedocs.io/zh_CN/v4.4.0/#true) . 看例子:

```python
soup.find_all(string="Elsie")
# [u'Elsie']

soup.find_all(string=["Tillie", "Elsie", "Lacie"])
# [u'Elsie', u'Lacie', u'Tillie']

soup.find_all(string=re.compile("Dormouse"))
[u"The Dormouse's story", u"The Dormouse's story"]

def is_the_only_string_within_a_tag(s):
    ""Return True if this string is the only child of its parent tag.""
    return (s == s.parent.string)

soup.find_all(string=is_the_only_string_within_a_tag)
# [u"The Dormouse's story", u"The Dormouse's story", u'Elsie', u'Lacie', u'Tillie', u'...']
```

虽然 `string` 参数用于搜索字符串,还可以与其它参数混合使用来过滤tag.Beautiful Soup会找到 `.string` 方法与 `string` 参数值相符的tag.下面代码用来搜索内容里面包含“Elsie”的<a>标签:

```python
soup.find_all("a", string="Elsie")
# [<a href="http://example.com/elsie" class="sister" id="link1">Elsie</a>]
```

#### `limit` 参数

`find_all()` 方法返回全部的搜索结构,如果文档树很大那么搜索会很慢.如果我们不需要全部结果,可以使用 `limit` 参数限制返回结果的数量.效果与SQL中的limit关键字类似,当搜索到的结果数量达到 `limit` 的限制时,就停止搜索返回结果.

文档树中有3个tag符合搜索条件,但结果只返回了2个,因为我们限制了返回数量:

```python
soup.find_all("a", limit=2)
# [<a class="sister" href="http://example.com/elsie" id="link1">Elsie</a>,
#  <a class="sister" href="http://example.com/lacie" id="link2">Lacie</a>]
```

#### `recursive` 参数

调用tag的 `find_all()` 方法时,Beautiful Soup会检索当前tag的所有子孙节点,如果只想搜索tag的直接子节点,可以使用参数 `recursive=False` .

一段简单的文档:

```python
<html>
 <head>
  <title>
   The Dormouse's story
  </title>
 </head>
...
```

是否使用 `recursive` 参数的搜索结果:

```python
soup.html.find_all("title")
# [<title>The Dormouse's story</title>]

soup.html.find_all("title", recursive=False)
# []
```

这是文档片段

```python
<html>
        <head>
        <title>
        The Dormouse's story
    </title>
        </head>
        ...
```

<title>标签在 <html> 标签下, 但并不是直接子节点, <head> 标签才是直接子节点. 在允许查询所有后代节点时 Beautiful Soup 能够查找到 <title> 标签. 但是使用了 `recursive=False` 参数之后,只能查找直接子节点,这样就查不到 <title> 标签了.

Beautiful Soup 提供了多种DOM树搜索方法. 这些方法都使用了类似的参数定义. 比如这些方法: `find_all()`: `name`, `attrs`, `text`, `limit`. 但是只有 `find_all()` 和 `find()` 支持 `recursive` 参数.

### 像调用 `find_all()` 一样调用tag

`find_all()` 几乎是Beautiful Soup中最常用的搜索方法,所以我们定义了它的简写方法. `BeautifulSoup` 对象和 `tag` 对象可以被当作一个方法来使用,这个方法的执行结果与调用这个对象的 `find_all()` 方法相同,下面两行代码是等价的:

```python
soup.find_all("a")
soup("a")
```

这两行代码也是等价的:

```python
soup.title.find_all(string=True)
soup.title(string=True)
```

### find()

find( [name](https://beautifulsoup.readthedocs.io/zh_CN/v4.4.0/#id35) , [attrs](https://beautifulsoup.readthedocs.io/zh_CN/v4.4.0/#css) , [recursive](https://beautifulsoup.readthedocs.io/zh_CN/v4.4.0/#recursive) , [string](https://beautifulsoup.readthedocs.io/zh_CN/v4.4.0/#id36) , [**kwargs](https://beautifulsoup.readthedocs.io/zh_CN/v4.4.0/#keyword) )

`find_all()` 方法将返回文档中符合条件的所有tag,尽管有时候我们只想得到一个结果.比如文档中只有一个<body>标签,那么使用 `find_all()` 方法来查找<body>标签就不太合适, 使用 `find_all` 方法并设置 `limit=1` 参数不如直接使用 `find()` 方法.下面两行代码是等价的:

```python
soup.find_all('title', limit=1)
# [<title>The Dormouse's story</title>]

soup.find('title')
# <title>The Dormouse's story</title>
```

唯一的区别是 `find_all()` 方法的返回结果是值包含一个元素的列表,而 `find()` 方法直接返回结果.

`find_all()` 方法没有找到目标是返回空列表, `find()` 方法找不到目标时,返回 `None` .

```python
print(soup.find("nosuchtag"))
# None
```

`soup.head.title` 是 [tag的名字](https://beautifulsoup.readthedocs.io/zh_CN/v4.4.0/#id20) 方法的简写.这个简写的原理就是多次调用当前tag的 `find()` 方法:

```python
soup.head.title
# <title>The Dormouse's story</title>

soup.find("head").find("title")
# <title>The Dormouse's story</title>
```

## CSS选择器

Beautiful Soup支持大部分的CSS选择器,在 `Tag` 或 `BeautifulSoup` 对象的 `.select()` 方法中传入字符串参数, 即可使用CSS选择器的语法找到tag:

```python
soup.select("title")
# [<title>The Dormouse's story</title>]

soup.select("p nth-of-type(3)")
# [<p class="story">...</p>]
```

通过tag标签逐层查找:

```python
soup.select("body a")
# [<a class="sister" href="http://example.com/elsie" id="link1">Elsie</a>,
#  <a class="sister" href="http://example.com/lacie"  id="link2">Lacie</a>,
#  <a class="sister" href="http://example.com/tillie" id="link3">Tillie</a>]

soup.select("html head title")
# [<title>The Dormouse's story</title>]
```

找到某个tag标签下的直接子标签 [[6\]](https://beautifulsoup.readthedocs.io/zh_CN/v4.4.0/#id93) :

```python
soup.select("head > title")
# [<title>The Dormouse's story</title>]

soup.select("p > a")
# [<a class="sister" href="http://example.com/elsie" id="link1">Elsie</a>,
#  <a class="sister" href="http://example.com/lacie"  id="link2">Lacie</a>,
#  <a class="sister" href="http://example.com/tillie" id="link3">Tillie</a>]

soup.select("p > a:nth-of-type(2)")
# [<a class="sister" href="http://example.com/lacie" id="link2">Lacie</a>]

soup.select("p > #link1")
# [<a class="sister" href="http://example.com/elsie" id="link1">Elsie</a>]

soup.select("body > a")
# []
```

找到兄弟节点标签:

```python
soup.select("#link1 ~ .sister")
# [<a class="sister" href="http://example.com/lacie" id="link2">Lacie</a>,
#  <a class="sister" href="http://example.com/tillie"  id="link3">Tillie</a>]

soup.select("#link1 + .sister")
# [<a class="sister" href="http://example.com/lacie" id="link2">Lacie</a>]
```

通过CSS的类名查找:

```python
soup.select(".sister")
# [<a class="sister" href="http://example.com/elsie" id="link1">Elsie</a>,
#  <a class="sister" href="http://example.com/lacie" id="link2">Lacie</a>,
#  <a class="sister" href="http://example.com/tillie" id="link3">Tillie</a>]

soup.select("[class~=sister]")
# [<a class="sister" href="http://example.com/elsie" id="link1">Elsie</a>,
#  <a class="sister" href="http://example.com/lacie" id="link2">Lacie</a>,
#  <a class="sister" href="http://example.com/tillie" id="link3">Tillie</a>]
```

通过tag的id查找:

```python
soup.select("#link1")
# [<a class="sister" href="http://example.com/elsie" id="link1">Elsie</a>]

soup.select("a#link2")
# [<a class="sister" href="http://example.com/lacie" id="link2">Lacie</a>]
```

同时用多种CSS选择器查询元素:

```python
soup.select("#link1,#link2")
# [<a class="sister" href="http://example.com/elsie" id="link1">Elsie</a>,
#  <a class="sister" href="http://example.com/lacie" id="link2">Lacie</a>]
```

通过是否存在某个属性来查找:

```python
soup.select('a[href]')
# [<a class="sister" href="http://example.com/elsie" id="link1">Elsie</a>,
#  <a class="sister" href="http://example.com/lacie" id="link2">Lacie</a>,
#  <a class="sister" href="http://example.com/tillie" id="link3">Tillie</a>]
```

通过属性的值来查找:

```python
soup.select('a[href="http://example.com/elsie"]')
# [<a class="sister" href="http://example.com/elsie" id="link1">Elsie</a>]

soup.select('a[href^="http://example.com/"]')
# [<a class="sister" href="http://example.com/elsie" id="link1">Elsie</a>,
#  <a class="sister" href="http://example.com/lacie" id="link2">Lacie</a>,
#  <a class="sister" href="http://example.com/tillie" id="link3">Tillie</a>]

soup.select('a[href$="tillie"]')
# [<a class="sister" href="http://example.com/tillie" id="link3">Tillie</a>]

soup.select('a[href*=".com/el"]')
# [<a class="sister" href="http://example.com/elsie" id="link1">Elsie</a>]
```

通过语言设置来查找:

```python
multilingual_markup = """
 <p lang="en">Hello</p>
 <p lang="en-us">Howdy, y'all</p>
 <p lang="en-gb">Pip-pip, old fruit</p>
 <p lang="fr">Bonjour mes amis</p>
"""
multilingual_soup = BeautifulSoup(multilingual_markup)
multilingual_soup.select('p[lang|=en]')
# [<p lang="en">Hello</p>,
#  <p lang="en-us">Howdy, y'all</p>,
#  <p lang="en-gb">Pip-pip, old fruit</p>]
```

返回查找到的元素的第一个

```python
soup.select_one(".sister")
# <a class="sister" href="http://example.com/elsie" id="link1">Elsie</a>
```

对于熟悉CSS选择器语法的人来说这是个非常方便的方法.Beautiful Soup也支持CSS选择器API, 如果你仅仅需要CSS选择器的功能,那么直接使用 `lxml` 也可以, 而且速度更快,支持更多的CSS选择器语法,但Beautiful Soup整合了CSS选择器的语法和自身方便使用API.

# 爬虫数据处理模块——json

## json.loads(json)

- **作用**

```python
把json格式的字符串转为Python数据类型
```

- **示例**

```python
html_json = json.loads(res.text)
```

## json.dump(python,f,ensure_ascii=False)

- **作用**

```python
把python数据类型 转为 json格式的字符串
# 一般让你把抓取的数据保存为json文件时使用
```

- **参数说明**

```python
第1个参数: python类型的数据(字典，列表等)
第2个参数: 文件对象
第3个参数: ensure_ascii=False # 序列化时编码
```

- **示例**

```python
# 示例1
import json

item = {'name':'QQ','app_id':1}
with open('小米.json','a') as f:
  json.dump(item,f,ensure_ascii=False)
  
# 示例2
import json

item_list = []
for i in range(3):
  item = {'name':'QQ','id':i}
  item_list.append(item)
    
with open('xiaomi.json','a') as f:
	json.dump(item_list,f,ensure_ascii=False)
```

## json.dumps(python)

- **作用**

```python
把 python 类型 转为 json 类型
```

- **示例**

```python
import json

# json.dumps()之前
item = {'name':'QQ','app_id':1}
print('before dumps',type(item)) # dict
# json.dumps之后
item = json.dumps(item)
print('after dumps',type(item)) # str
```

## json.load(f)

**作用**

```python
将json文件读取,并转为python类型
```

示例

```python
import json

with open('D:\\spider_test\\xiaomi.json','r') as f:
    data = json.load(f)
    
print(data)
```

## json模块总结

```python
# 爬虫最常用
1、数据抓取 - json.loads(html)
   将响应内容由: json 转为 python
2、数据保存 - json.dump(item_list,f,ensure_ascii=False)
   将抓取的数据保存到本地 json文件

# 抓取数据一般处理方式
1、txt文件
2、csv文件
3、json文件
4、MySQL数据库
5、MongoDB数据库
6、Redis数据库
```

# 爬虫数据持久化存储——写入文件

## open方法

- 方法名称及参数

  ```python
  **open(file, mode='r', buffering=None, encoding=None, errors=None, newline=None, closefd=True)**
  
  **file** 文件的路径，需要带上文件名包括文件后缀（c:\\1.txt）
  
  **mode** 打开的方式（r,w,a,x,b,t,r+,w+,a+,U）
  
  **buffering** 缓冲的buffering大小， 0，就不会有寄存。1，寄存行。大于 1 的整数，寄存区的缓冲大小。负值，寄存区的缓冲大小为系统默认。
  
  **encoding** 文件的编码格式(utf-8,GBK等)
  ```

- 常用的文件打开方式

  ```python
  r  以只读方式打开文件。文件的指针会放在文件的开头。
  
  w 以写入方式打开文件。文件存在覆盖文件，文件不存在创建一个新文件。
  
  a 以追加方式打开文件。如果文件已存在，文件指针放在文件末尾。如果文件不存在，创建新文件并可写入。
  
  r+  打开一个文件用于读写。文件指针会放在文件的开头
  
  w+  打开一个文件用于读写。文件存在覆盖文件，文件不存在创建一个新文件。
  
  a+  打开一个文件用于读写。如果文件已存在，文件指针放在文件末尾。如果文件不存在，创建新文件并可写入。
  
  记忆方法：记住r读，w写，a追加，每个模式后加入+号就变成可读写。
  ```

## 文件的读取及写入

### 读取文件

```python
file.read([size])：读取文件(读取size个字节，默认读取全部)
file.readline())：读取一行
file.readlines()：读取完整的文件，返回每一行所组成的列表
```

### 写入文件

```python
file.write(str)：将字符串写入文件

file.writelines(lines)：将多行文本写入文件中，lines为字符串组成的列表或元组
```





# 爬虫数据持久化存储——csv文件

## 作用

```python
将爬取的数据存放到本地的csv文件中
```

## 使用流程

```python
1、导入模块
2、打开csv文件
3、初始化写入对象
4、写入数据(参数为列表)
import csv 

with open('film.csv','w') as f:
    writer = csv.writer(f)
    writer.writerow([])
```

## 示例：创建 test.csv 文件，在文件中写入数据

```python
# 单行写入（writerow([]))
import csv
with open('test.csv','w',newline='') as f:
	writer = csv.writer(f)
	writer.writerow(['步惊云','36'])
	writer.writerow(['超哥哥','25'])

# 多行写入(writerows([(),(),()]
import csv
with open('test.csv','w',newline='') as f:
	writer = csv.writer(f)
	writer.writerows([('聂风','36'),('秦霜','25'),('孔慈','30')])
```

# 爬虫数据处理:操作数据库模块——pymysql

## pymysql介绍

PyMySQL是在 Python3.x 版本中用于连接 MySQL 服务器的一个库，Python2中是使用mysqldb

### pymysql安装

```python
pip install pymysql -i https://pypi.douban.com/simple
```

## pymysql基本使用

```python
# 导入pymysql模块
import pymysql
 
# 连接database
conn = pymysql.connect(
    host=“你的数据库地址”,
    user=“用户名”,password=“密码”,
    database=“数据库名”,
    charset=“utf8”)
 
# 得到一个可以执行SQL语句的光标对象
cursor = conn.cursor()  # 执行完毕返回的结果集默认以元组显示
# 得到一个可以执行SQL语句并且将结果作为字典返回的游标
#cursor = conn.cursor(cursor=pymysql.cursors.DictCursor)
 
# 定义要执行的SQL语句
sql = """
CREATE TABLE USER1 (
id INT auto_increment PRIMARY KEY ,
name CHAR(10) NOT NULL UNIQUE,
age TINYINT NOT NULL
)ENGINE=innodb DEFAULT CHARSET=utf8;  #注意：charset='utf8' 不能写成utf-8
"""
 
# 执行SQL语句
cursor.execute(sql)
 
# 关闭光标对象
cursor.close()
 
# 关闭数据库连接
conn.close()
```

## 增删改查操作

### 添加一条或多条数据

```python
#假设已有某数据库xing，其中包含姓名及编号两个字段
import pymysql
 
conn = pymysql.connect(
    host='192.168.0.103',
    port=3306,
    user='root',
    password='123',
    database='xing',
    charset='utf8'
)
# 获取一个光标
cursor = conn.cursor()
 
# 定义要执行的sql语句
sql = 'insert into userinfo(user,pwd) values(%s,%s);'
data = [
    ('july', '147'),
    ('june', '258'),
    ('marin', '369')
]
# 拼接并执行sql语句
cursor.executemany(sql, data)
 
# 涉及写操作要注意提交
conn.commit()
 
# 关闭连接
cursor.close()
conn.close()
```

### 插入单条数据

```python
import pymysql
conn =pymysql.connect(
    host ='192.168.0.103',
    port = 3306,
    user = 'root',
    password ='123',
    database ='xing',
    charset ='utf8'
)
cursor =conn.cursor()  #获取一个光标
sql ='insert into userinfo (user,pwd) values (%s,%s);'
 
name = 'wuli'
pwd = '123456789'
cursor.execute(sql, [name, pwd])
conn.commit()
cursor.close()
conn.close()
```

### 获取最新插入数据

```python
import pymysql
 
# 建立连接
conn = pymysql.connect(
    host="192.168.0.103",
    port=3306,
    user="root",
    password="123",
    database="xing",
    charset="utf8"
)
# 获取一个光标
cursor = conn.cursor()
# 定义将要执行的SQL语句
sql = "insert into userinfo (user, pwd) values (%s, %s);"
name = "wuli"
pwd = "123456789"
# 并执行SQL语句
cursor.execute(sql, [name, pwd])
# 涉及写操作注意要提交
conn.commit()
# 关闭连接
 
# 获取最新的那一条数据的ID
last_id = cursor.lastrowid
print("最后一条数据的ID是:", last_id)
 
cursor.close()
conn.close()
```

### 删除操作

```python
import pymysql
 
# 建立连接
conn = pymysql.connect(
    host="192.168.0.103",
    port=3306,
    user="root",
    password="123",
    database="xing",
    charset="utf8"
)
# 获取一个光标
cursor = conn.cursor()
# 定义将要执行的SQL语句
sql = "delete from userinfo where user=%s;"
name = "june"
# 拼接并执行SQL语句
cursor.execute(sql, [name])
# 涉及写操作注意要提交
conn.commit()
# 关闭连接
 
cursor.close()
conn.close()
```

### 更新数据

```python
import pymysql
 
# 建立连接
conn = pymysql.connect(
    host="192.168.0.103",
    port=3306,
    user="root",
    password="123",
    database="xing",
    charset="utf8"
)
# 获取一个光标
cursor = conn.cursor()
# 定义将要执行的SQL语句
sql = "delete from userinfo where user=%s;"
name = "june"
# 拼接并执行SQL语句
cursor.execute(sql, [name])
# 涉及写操作注意要提交
conn.commit()
# 关闭连接
 
cursor.close()
conn.close()
```

### 查询数据

```python
# 可以获取指定数量的数据
cursor.fetchmany(3)
# 光标按绝对位置移动1
cursor.scroll(1, mode="absolute")
# 光标按照相对位置(当前位置)移动1
cursor.scroll(1, mode="relative"
```



# 爬虫数据持久化存储——写入MySQL

**1、在数据库中建库建表**

```mysql
# 连接到mysql数据库
mysql -h127.0.0.1 -uroot -p123456
# 建库建表
create database maoyandb charset utf8;
use maoyandb;
create table filmtab(
name varchar(100),
star varchar(300),
time varchar(50)
)charset=utf8;
```

- **2、回顾pymysql基本使用**

```python
一般方法：

import pymysql

# 创建2个对象
db = pymysql.connect('localhost','root','123456','maoyandb',charset='utf8')
cursor = db.cursor()

# 执行SQL命令并提交到数据库执行
# execute()方法第二个参数为列表传参补位
ins = 'insert into filmtab values(%s,%s,%s)'
cursor.execute(ins,['霸王别姬','张国荣','1993'])
db.commit()

# 关闭
cursor.close()
db.close()
```

- **来试试高效的executemany()方法？**

```python
import pymysql

# 创建2个对象
db = pymysql.connect('192.168.153.137','tiger','123456','maoyandb',charset='utf8')
cursor = db.cursor()

# 抓取的数据
film_list = [('月光宝盒','周星驰','1994'),('大圣娶亲','周星驰','1994')]

# 执行SQL命令并提交到数据库执行
# execute()方法第二个参数为列表传参补位
cursor.executemany('insert into filmtab values(%s,%s,%s)',film_list)
db.commit()

# 关闭
cursor.close()
db.close()
```

# 案例8：将top100榜单电影信息存入MySQL数据库(尽量使用executemany方法)

```python
# -*- coding:utf-8 _*-
"""
@version:
author:安伟超
@time: 2020/09/07
@file: demo02_MaoYanMovie_simple.py.py
@environment:virtualenv
@email:awc19930818@outlook.com
@github:https://github.com/La0bALanG
@requirement:1.获取top100榜单页面全部内容；
	2.使用正则匹配出每一条的电影名称，主演，上映时间
	3.将获取的内容写入字典（下一节讲解写入持久化存储）
"""
import threading
import re
import pymysql
import csv
from urllib import request
from time import sleep
from random import randint

"""

数据抓取实现思路：
1.分析URL规律
2.分析页面结构，确定存在所需数据
3.构造headers及最终请求URL
4.发送请求获得相应数据
5.使用正则匹配解析所需数据存入字典

1.分析URL规律

进入猫眼电影网-榜单-top100，随意查看几页，观察其URL规律：
https://maoyan.com/board/4?offset=20
https://maoyan.com/board/4?offset=30
...
https://maoyan.com/board/4?offset=(页数 - 1) * 10

2.分析页面结构，确定存在所需数据
浏览器F12-打开控制台-抓手工具-抓到对应电影内容-查看html信息，如下：

<div class="movie-item-info">
        <p class="name"><a href="/films/4883" title="钢琴家" data-act="boarditem-click" data-val="{movieId:4883}">钢琴家</a></p>
        <p class="star">
                主演：艾德里安·布洛迪,艾米莉娅·福克斯,米哈乌·热布罗夫斯基
        </p>
        <p class="releasetime">上映时间：2002-05-24(法国)</p>    </div>

所需数据存在上部分的响应内容中

3.构造headers及最终请求URL

4.发送请求获得响应数据

5.解析数据
依据上述内容，确定使用正则表达式匹配
匹配思路：
    1.class为name的p标签内部的a标签，其title属性的属性值为电影名称；
    2.class为star的p标签的内容为电影的主演信息；
    3.class为releasetime的p标签的内容为电影的上映时间；

构造正则表达式，匹配以上内容即可：
<div class="movie-item-info">.*?title="(.*?)".*?class="star">(.*?)</p>.*?releasetime">(.*?)</p>

6.数据按照合适形式组织存入字典
"""


class MaoYanMovieSpider(object):
    '''

    面向对象思路：
        1.拆分功能细节。整体程序可拆分为:
            1.发请求获得页面
            2.解析页面
            3.持久化存储(写入文件保存)
        2.结合开闭原则，封装功能方法为私有方法，对外提供统一公共接口
        3.采用单例模式：假设本爬虫程序在多个时间、不同情况下多次使用，单例模式实现只创建一个对象，提升性能避免内存占用过高。

    '''
    # 添加线程锁，避免实际运行过程中受多线程影响

    _instance_lock = threading.Lock()

    def __init__(self):
        self.__url = 'https://maoyan.com/board/4?offset={}'

        # 计数变量
        self.__i = 0

        self.__db = pymysql.connect(
            'localhost', 'root', '185268', 'maoyandb',
            charset='utf8'
        )
        self.__cursor = self.db.cursor()

    # 单例模式实现：__new__方法
    def __new__(cls, *args, **kwargs):
        if not hasattr(MaoYanMovieSpider, '_instance'):
            with MaoYanMovieSpider._instance_lock:
                if not hasattr(MaoYanMovieSpider, '_instance'):
                    MaoYanMovieSpider._instance = object.__new__(cls)
        return MaoYanMovieSpider._instance

    # 设置只读属性
    @property
    def url(self):
        return self.__url

    @property
    def i(self):
        return self.__i

    @property
    def db(self):
        return self.__db

    @property
    def curosr(self):
        return self.__cursor

    def __get_html(self, url):
        # 伪造headers
        headers = {
            'User-Agent': 'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/85.0.4183.83 Safari/537.36'
        }
        # 发请求
        # 1.创建请求对象
        reqs = request.Request(url=url, headers=headers)
        # 2.发起正式请求，获得页面响应数据
        reps = request.urlopen(reqs).read().decode()
        self.__parse_html(reps)

    def __parse_html(self, html):
        # 创建正则对象
        r = re.compile(
            '<div class="movie-item-info">.*?title="(.*?)".*?class="star">(.*?)</p>.*?releasetime">(.*?)</p>', re.S)
        # 正则匹配，查找到的结果存入列表
        find_list = re.findall(r, html)
        self.__save_html(find_list)

    # def __save_html(self,data_list):
    #     dict = {}
    #     # 遍历查询结果集
    #     for item in data_list:
    #         # 每一项内容清洗后存入对应的键名
    #         dict['name'] = item[0].strip()
    #         dict['star'] = item[1].strip()
    #         dict['time'] = item[2].strip()[5:15]
    #         self.__i += 1
    #         print(dict)

    def __save_html(self, data_list):
        inser = 'insert into filmtab values (%s,%s,%s)'
        for film in data_list:
            l = [
                film[0],
                film[1].strip(),
                film[2].strip()[5:15]
            ]
            self.__cursor.execute(inser,l)
            self.db.commit()

    def display(self):
        print('爬虫程序开始执行，即将爬取top100榜单信息，每间隔3到5秒继续...')
        for i in range(0, 91, 10):
            url = self.__url.format(i)
            self.__get_html(url)
            # sleep(randint(3,5))
        self.__cursor.close()
        self.__db.close()
        print('抓取的数据量：%d' % self.__i)


def test():
    MaoYanMovieSpider().display()
    print('爬取完毕...')


if __name__ == '__main__':
    test()








executemany方法：

# -*- coding:utf-8 _*-
"""
@version:
author:安伟超
@time: 2020/09/07
@file: demo02_MaoYanMovie_simple.py.py
@environment:virtualenv
@email:awc19930818@outlook.com
@github:https://github.com/La0bALanG
@requirement:1.获取top100榜单页面全部内容；
	2.使用正则匹配出每一条的电影名称，主演，上映时间
	3.将获取的内容写入字典（下一节讲解写入持久化存储）
"""
import threading
import re
import pymysql
import csv
from urllib import request
from time import sleep
from random import randint

"""

数据抓取实现思路：
1.分析URL规律
2.分析页面结构，确定存在所需数据
3.构造headers及最终请求URL
4.发送请求获得相应数据
5.使用正则匹配解析所需数据存入字典

1.分析URL规律

进入猫眼电影网-榜单-top100，随意查看几页，观察其URL规律：
https://maoyan.com/board/4?offset=20
https://maoyan.com/board/4?offset=30
...
https://maoyan.com/board/4?offset=(页数 - 1) * 10

2.分析页面结构，确定存在所需数据
浏览器F12-打开控制台-抓手工具-抓到对应电影内容-查看html信息，如下：

<div class="movie-item-info">
        <p class="name"><a href="/films/4883" title="钢琴家" data-act="boarditem-click" data-val="{movieId:4883}">钢琴家</a></p>
        <p class="star">
                主演：艾德里安·布洛迪,艾米莉娅·福克斯,米哈乌·热布罗夫斯基
        </p>
        <p class="releasetime">上映时间：2002-05-24(法国)</p>    </div>

所需数据存在上部分的响应内容中

3.构造headers及最终请求URL

4.发送请求获得响应数据

5.解析数据
依据上述内容，确定使用正则表达式匹配
匹配思路：
    1.class为name的p标签内部的a标签，其title属性的属性值为电影名称；
    2.class为star的p标签的内容为电影的主演信息；
    3.class为releasetime的p标签的内容为电影的上映时间；

构造正则表达式，匹配以上内容即可：
<div class="movie-item-info">.*?title="(.*?)".*?class="star">(.*?)</p>.*?releasetime">(.*?)</p>

6.数据按照合适形式组织存入字典
"""


class MaoYanMovieSpider(object):
    '''

    面向对象思路：
        1.拆分功能细节。整体程序可拆分为:
            1.发请求获得页面
            2.解析页面
            3.持久化存储(写入文件保存)
        2.结合开闭原则，封装功能方法为私有方法，对外提供统一公共接口
        3.采用单例模式：假设本爬虫程序在多个时间、不同情况下多次使用，单例模式实现只创建一个对象，提升性能避免内存占用过高。

    '''
    # 添加线程锁，避免实际运行过程中受多线程影响

    _instance_lock = threading.Lock()

    def __init__(self):
        self.__url = 'https://maoyan.com/board/4?offset={}'

        # 计数变量
        self.__i = 0

        self.__db = pymysql.connect(
            'localhost', 'root', '185268', 'maoyandb',
            charset='utf8'
        )
        self.__cursor = self.__db.cursor()
        self.all_list = []

    # 单例模式实现：__new__方法
    def __new__(cls, *args, **kwargs):
        if not hasattr(MaoYanMovieSpider, '_instance'):
            with MaoYanMovieSpider._instance_lock:
                if not hasattr(MaoYanMovieSpider, '_instance'):
                    MaoYanMovieSpider._instance = object.__new__(cls)
        return MaoYanMovieSpider._instance

    # 设置只读属性
    @property
    def url(self):
        return self.__url

    @property
    def i(self):
        return self.__i

    @property
    def db(self):
        return self.__db

    @property
    def curosr(self):
        return self.__cursor

    def __get_html(self, url):
        # 伪造headers
        headers = {
            'User-Agent': 'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/85.0.4183.83 Safari/537.36'
        }
        # 发请求
        # 1.创建请求对象
        reqs = request.Request(url=url, headers=headers)
        # 2.发起正式请求，获得页面响应数据
        reps = request.urlopen(reqs).read().decode()
        self.__parse_html(reps)

    def __parse_html(self, html):
        # 创建正则对象
        r = re.compile(
            '<div class="movie-item-info">.*?title="(.*?)".*?class="star">(.*?)</p>.*?releasetime">(.*?)</p>', re.S)
        # 正则匹配，查找到的结果存入列表
        find_list = re.findall(r, html)
        self.__save_html(find_list)

    # def __save_html(self,data_list):
    #     dict = {}
    #     # 遍历查询结果集
    #     for item in data_list:
    #         # 每一项内容清洗后存入对应的键名
    #         dict['name'] = item[0].strip()
    #         dict['star'] = item[1].strip()
    #         dict['time'] = item[2].strip()[5:15]
    #         self.__i += 1
    #         print(dict)

    def __save_html(self, data_list):
        for film in data_list:
            self.all_list.append(
                (film[0], film[1].strip(), film[2][5:15])
            )

    def display(self):
        print('爬虫程序开始执行，即将爬取top100榜单信息，每间隔3到5秒继续...')
        for i in range(0, 91, 10):
            url = self.__url.format(i)
            self.__get_html(url)
            # sleep(randint(3,5))
        ins = 'insert into filmtab values(%s,%s,%s)'
        self.__cursor.executemany(ins, self.all_list)
        self.__db.commit()
        self.__cursor.close()
        self.__db.close()
        print('抓取的数据量：%d' % self.__i)


def test():
    MaoYanMovieSpider().display()
    print('爬取完毕...')


if __name__ == '__main__':
    test()








```

# 爬虫数据持久化存储——写入MongoDB

- **pymongo操作mongodb数据库**

```python
import pymongo

# 1.数据库连接对象
conn=pymongo.MongoClient('localhost',27017)
# 2.库对象
db = conn['库名']
# 3.集合对象
myset = db['集合名']
# 4.插入数据
myset.insert_one({字典})
```

- **mongodb常用命令**

```python
mongo
>show dbs
>use 库名
>show collections
>db.集合名.find().pretty()
>db.集合名.count()
>db.dropDatabase()
```

# 案例9：猫眼电影top100数据写入mongo

```python
# -*- coding:utf-8 _*-
"""
@version:
author:安伟超
@time: 2020/09/07
@file: demo02_MaoYanMovie_simple.py.py
@environment:virtualenv
@email:awc19930818@outlook.com
@github:https://github.com/La0bALanG
@requirement:1.获取top100榜单页面全部内容；
	2.使用正则匹配出每一条的电影名称，主演，上映时间
	3.将获取的内容写入字典（下一节讲解写入持久化存储）
"""
import threading
import re
import pymongo
import csv
from urllib import request
from time import sleep
from random import randint

"""

数据抓取实现思路：
1.分析URL规律
2.分析页面结构，确定存在所需数据
3.构造headers及最终请求URL
4.发送请求获得相应数据
5.使用正则匹配解析所需数据存入字典

1.分析URL规律

进入猫眼电影网-榜单-top100，随意查看几页，观察其URL规律：
https://maoyan.com/board/4?offset=20
https://maoyan.com/board/4?offset=30
...
https://maoyan.com/board/4?offset=(页数 - 1) * 10

2.分析页面结构，确定存在所需数据
浏览器F12-打开控制台-抓手工具-抓到对应电影内容-查看html信息，如下：

<div class="movie-item-info">
        <p class="name"><a href="/films/4883" title="钢琴家" data-act="boarditem-click" data-val="{movieId:4883}">钢琴家</a></p>
        <p class="star">
                主演：艾德里安·布洛迪,艾米莉娅·福克斯,米哈乌·热布罗夫斯基
        </p>
        <p class="releasetime">上映时间：2002-05-24(法国)</p>    </div>

所需数据存在上部分的响应内容中

3.构造headers及最终请求URL

4.发送请求获得响应数据

5.解析数据
依据上述内容，确定使用正则表达式匹配
匹配思路：
    1.class为name的p标签内部的a标签，其title属性的属性值为电影名称；
    2.class为star的p标签的内容为电影的主演信息；
    3.class为releasetime的p标签的内容为电影的上映时间；

构造正则表达式，匹配以上内容即可：
<div class="movie-item-info">.*?title="(.*?)".*?class="star">(.*?)</p>.*?releasetime">(.*?)</p>

6.数据按照合适形式组织存入字典
"""


class MaoYanMovieSpider(object):
    '''

    面向对象思路：
        1.拆分功能细节。整体程序可拆分为:
            1.发请求获得页面
            2.解析页面
            3.持久化存储(写入文件保存)
        2.结合开闭原则，封装功能方法为私有方法，对外提供统一公共接口
        3.采用单例模式：假设本爬虫程序在多个时间、不同情况下多次使用，单例模式实现只创建一个对象，提升性能避免内存占用过高。

    '''
    # 添加线程锁，避免实际运行过程中受多线程影响

    _instance_lock = threading.Lock()

    def __init__(self):
        self.__url = 'https://maoyan.com/board/4?offset={}'

        # 计数变量
        self.__i = 0

        self.__conn = pymongo.MongoClient(
            'localhost', 27017
        )
        self.__db = self.conn['maoyandb']
        self.__myset = self.db['maoyanset']

    # 单例模式实现：__new__方法
    def __new__(cls, *args, **kwargs):
        if not hasattr(MaoYanMovieSpider, '_instance'):
            with MaoYanMovieSpider._instance_lock:
                if not hasattr(MaoYanMovieSpider, '_instance'):
                    MaoYanMovieSpider._instance = object.__new__(cls)
        return MaoYanMovieSpider._instance

    # 设置只读属性
    @property
    def url(self):
        return self.__url

    @property
    def i(self):
        return self.__i

    @property
    def conn(self):
        return self.__conn

    @property
    def db(self):
        return self.__db

    @property
    def myset(self):
        return self.__myset


    @property
    def curosr(self):
        return self.__cursor

    def __get_html(self, url):
        # 伪造headers
        headers = {
            'User-Agent': 'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/85.0.4183.83 Safari/537.36'
        }
        # 发请求
        # 1.创建请求对象
        reqs = request.Request(url=url, headers=headers)
        # 2.发起正式请求，获得页面响应数据
        reps = request.urlopen(reqs).read().decode()
        self.__parse_html(reps)

    def __parse_html(self, html):
        # 创建正则对象
        r = re.compile(
            '<div class="movie-item-info">.*?title="(.*?)".*?class="star">(.*?)</p>.*?releasetime">(.*?)</p>', re.S)
        # 正则匹配，查找到的结果存入列表
        find_list = re.findall(r, html)
        self.__save_html(find_list)

    # def __save_html(self,data_list):
    #     dict = {}
    #     # 遍历查询结果集
    #     for item in data_list:
    #         # 每一项内容清洗后存入对应的键名
    #         dict['name'] = item[0].strip()
    #         dict['star'] = item[1].strip()
    #         dict['time'] = item[2].strip()[5:15]
    #         self.__i += 1
    #         print(dict)

    def __save_html(self, data_list):
        for film in data_list:
            item = {}
            item['name'] = film[0].strip()
            item['star'] = film[1].strip()
            item['time'] = film[2].strip()[5:15]
            print(item)
            self.i += 1
            # 把数据存入mongodb数据库
            self.myset.insert_one(item)

    def display(self):
        print('爬虫程序开始执行，即将爬取top100榜单信息，每间隔3到5秒继续...')
        for i in range(0, 91, 10):
            url = self.__url.format(i)
            self.__get_html(url)
            # sleep(randint(3,5))
        print('抓取的数据量：%d' % self.__i)


def test():
    MaoYanMovieSpider().display()
    print('爬取完毕...')


if __name__ == '__main__':
    test()
```

# 常见反爬机制1：代理IP

- **代理IP概述**

```python
# 1、定义及作用
1、定义: 代替你原来的IP地址去对接网络的IP地址
2、作用: 隐藏自身真实IP,避免被封

# 2、获取代理IP的网站
西刺代理、快代理、全网代理、代理精灵、... ...

# 3、代理IP的分类
1、透明代理: 服务端能看到 - （用户真实IP 以及 代理IP）
2、普通代理: 服务端能看到 - （代理IP，知道有人通过此代理IP访问了网站，但不知用户真实IP）
3、高匿代理: 服务端能看到 - （代理IP）

# 4、常用代理IP类型
1、普通代理: 可用率低、速度慢、不稳定、免费或价格便宜
2、私密代理: 可用率高、速度较快、价格适中、爬虫常用
3、独享代理: 可用率极高、速度快、价格贵
```

## **普通代理**

- **获取代理IP网站**

```python
西刺代理、快代理、全网代理、代理精灵、... ...
```

- **参数类型**

```python
1、语法结构
   	proxies = {
       	'协议':'协议://IP:端口号'
   	}
2、示例
    proxies = {
    	'http':'http://IP:端口号',
    	'https':'https://IP:端口号'
	}
```

- **示例**

使用免费普通代理IP访问测试网站: http://httpbin.org/get

```python
import requests

url = 'http://httpbin.org/get'
headers = {
    'User-Agent':'Mozilla/5.0'
}
# 定义代理,在代理IP网站中查找免费代理IP
proxies = {
    'http':'http://112.85.164.220:9999',
    'https':'https://112.85.164.220:9999'
}
html = requests.get(url,proxies=proxies,headers=headers,timeout=5).text
print(html)
```

**思考: 建立一个自己的代理IP池，随时更新用来抓取网站数据**

```python
1、从免费代理IP网站上,抓取免费代理IP
2、测试抓取的IP,可用的保存在文件中
```

**代码实现**

```python
# -*- coding:utf-8 _*-
"""
@version:
author:安伟超
@time: 2020/09/12
@file: demo10_xicidaili_getIP.py.py
@environment:virtualenv
@email:awc19930818@outlook.com
@github:https://github.com/La0bALanG
@requirement:爬取66代理所有可用代理IP，存入文件，作为个人IP代理池
"""

import threading
import requests
import time
import random
from lxml import etree
from fake_useragent import UserAgent

class GetXiCiDaiLiIPSpider(object):
    '''

        面向对象思路：
        1.拆分功能细节。整体程序可拆分为:
            1.发请求获得页面
            2.解析页面
            3.持久化存储(写入文件保存)
        2.结合开闭原则，封装功能方法为私有方法，对外提供统一公共接口
        3.采用单例模式：假设本爬虫程序在多个时间、不同情况下多次使用，单例模式实现只创建一个对象，提升性能避免内存占用过高。

        '''

    _instance_lock = threading.Lock()

    # 单例模式实现：__new__方法
    def __new__(cls, *args, **kwargs):
        if not hasattr(GetXiCiDaiLiIPSpider, '_instance'):
            with GetXiCiDaiLiIPSpider._instance_lock:
                if not hasattr(GetXiCiDaiLiIPSpider, '_instance'):
                    GetXiCiDaiLiIPSpider._instance = object.__new__(cls)
        return GetXiCiDaiLiIPSpider._instance

    def __init__(self):
        self.__url = 'https://www.kuaidaili.com/free/inha/{}/'
        self.__headers = {
            'User-Agent':UserAgent().random
        }

    def __get_html(self,url,headers):
        return requests.get(url=url,headers=headers).text

    def __parse_html(self,html):
        dom = etree.HTML(html)
        tr_lists = dom.xpath('//table/tbody/tr')
        #第一个tr不是ip及端口号信息，跳过第1个，从第2个tr开始提取
        for tr in tr_lists:
            ip = tr.xpath('./td[1]/text()')[0]
            port = tr.xpath('./td[2]/text()')[0]
            self.__test_IP(ip,port)

    def __test_IP(self,ip,port):
        proxies = {
            'http': 'http://{}:{}'.format(ip, port),
            'https': 'https://{}:{}'.format(ip, port),
        }
        test_url = 'https://www.hao123.com/'
        try:
            res = requests.get(url=test_url,proxies=proxies,timeout=8)
            if res.status_code == 200:
                print('代理ip:%s:%s测试完毕，success,采用，即将写入代理池文件'%(ip,port))
                with open('proxies.txt','a') as f:
                    print('写入代理ip...')
                    f.write(ip + ':' + port + '\n')
                    print('写入完成，测试下一条代理ip...')
        except Exception as e:
            print('代理ip:%s:%s测试完毕，faild,不采用，测试下一条代理ip...'%(ip,port))
    def display(self):
        begin = int(input('请输入开始页数：'))
        end = int(input('请输入结束页数：'))
        for i in range(begin,end + 1):
            print('开始爬取第%d页代理ip...'%i)
            url = self.__url.format(i)
            self.__parse_html(self.__get_html(url,self.__headers))
            time.sleep(random.randint(0,3))

def test():
    GetXiCiDaiLiIPSpider().display()

if __name__ == '__main__':
    test()
```

## **私密代理+独享代理**

- **语法格式**

```python
1、语法结构
proxies = {
    '协议':'协议://用户名:密码@IP:端口号'
}

2、示例
proxies = {
	'http':'http://用户名:密码@IP:端口号',
  'https':'https://用户名:密码@IP:端口号'
}
```

- **示例代码**

```python
import requests
url = 'http://httpbin.org/get'
proxies = {
    'http': 'http://用户名:密码@106.75.71.140:16816',
    'https':'https://用户名:密码@106.75.71.140:16816',
}
headers = {
    'User-Agent' : 'Mozilla/5.0',
}

html = requests.get(url,proxies=proxies,headers=headers,timeout=5).text
print(html)
```

# 常见反爬机制2：动态页面爬虫技术

## 控制台抓包思路

```python
一、静态页面
	一种常见的网站、网页类型。我们爬虫所关注的特点是：该类网站的一次html请求的response中包含部分或所有所需的目标数据。
    注意：静态网页目前来看存在于：
    	1.确确实实没什么技术含量的小网站...
        2.对安全性关注度不高的某些数据，采用静态页面直接渲染出来。
        	特点：此类静态页面包含的数据对企业或机构来说无关痛痒，即不是那么的重要，而静态页面直接渲染的方式相对来说对技术要求又不高，成本较低，所以直接渲染出来，你爱爬你就爬~无所谓~
二、动态网页
	一种常见的网站、网页类型。此类网页才是WWW中最常见的网页。基本现在但凡是个规模的网站，大部分都采用了动态页面技术。动态页面不会将数据直接渲染在response中，且不会一次刷新就全部加载完毕，而是伴随用户对页面的操作实现局部刷新。
    动态页面的核心特点是：
		1.数据不会直接渲染于response中；
        2.大部分动态页面都会采用AJAX异步请求进行局部刷新；
        3.结合以上特点，对响应的数据进行处理，通常采用js进行加载，且处理过程通常伴随着加密。
    所以，动态页面在爬取的过程中难度就增大了，不仅要对响应页面做处理，更重要的是要追踪js加载方式甚至追踪js代码，深层次剖析请求及响应的数据体，进而采用Python进行模拟js操作，实现获取真实数据及破解加密。
三、如何判断一个页面是静态页面还是动态页面？
	一般具有以下几个特征的页面，基本就是动态页面了：
    	1.页面伴随着一些鼠标键盘操作一点点刷新数据的。比如最常见的“加载更多”;
        2.在elements中能解析到数据，但进入具体的response中却查找不到数据的；
        3.采用AJAX异步加载的。
四、html的response中不存在所需数据怎么办？
	如果当前页面的html请求的response中不存在所需数据，但elements选项中能够使用re或xpath解析到我们所需要的数据，则所需数据一定是进行了响应处理，则可以通过控制台抓包分析查找所需数据。
五、控制台抓包分析
    1、打开浏览器，F12打开控制台，找到Network选项卡
    2、控制台常用选项
       1、Network: 抓取网络数据包
            1、ALL: 抓取所有的网络数据包
            2、XHR：抓取异步加载的网络数据包
            3、JS : 抓取所有的JS文件
       2、Sources: 格式化输出并打断点调试JavaScript代码，助于分析爬虫中一些参数
       3、Console: 交互模式，可对JavaScript中的代码进行测试
    3、抓取具体网络数据包后
       1、单击左侧网络数据包地址，进入数据包详情，查看右侧
       2、右侧:
           1、Headers: 整个请求信息
              General、Response Headers、Request Headers、Query String、Form Data
           2、Preview: 对响应内容进行预览
           3、Response：响应内容
```

## 动态加载页面的数据爬取-AJAX

```python
一、什么是AJAX
	AJAX(Asynchronous JavaScript And XML)：异步的JavaScript and XML。通过在后台与服务器进行商量的数据交换，Ajax可以使网页实现异步更新，这意味着可以在不重新加载整个网页的情况下，对网页的某部分进行更新。传统的网页（不使用Ajax）如果需要更新内容，必须重载整个网页页面。又因为传统的数据传输格式使用的是XML语法，因此叫做Ajax。但现如今的数据交互方式，基本上都选择使用JSON格式的字符串，其目的就是为了达到数据传输格式的统一。因为json支持几乎所有编程语言。使用Ajax加载的数据，即使有对应的JS脚本，能够将数据渲染到浏览器中，在查看网页源码时还是不能看到通过Ajax加载的数据，只能看到使用这个url加载的HTML代码。
二、什么是JSON
	JSON(JavaScript Object Notation, JS对象简谱) 是一种轻量级的数据交换格式。它基于 ECMAScript (欧洲计算机协会制定的js规范)的一个子集，采用完全独立于编程语言的文本格式来存储和表示数据。简洁和清晰的层次结构使得 JSON 成为理想的数据交换语言。 易于人阅读和编写，同时也易于机器解析和生成，并有效地提升网络传输效率。
三、动态页面的数据加载特征
	1.几乎统一采用json格式字符串传递；
    2.往往伴随着用户对网页的某些操作，比如鼠标事件，键盘事件等；
    3.几乎无法直接在html的response中直观看到数据；
四、动态页面数据抓取固定套路
	1.请求目标url；
    2.F12打开控制台进行抓包分析；
    	F12 -- network -- XHR/JS -- 网页操作 -- / 查看新增请求项 -- 分析数据及规律
    3.确定目标数据url/接口
    4.发请求，获得response；
    5.解析数据(大部分情况下解析的是json数据)
    6.持久化存储
```

# 案例10：有道翻译破解案例

```python
# -*- coding:utf-8 _*-
"""
@version:
author:安伟超
@time: 2020/09/11
@file: demo08_YouDaoTransforSpider_OOP.py.py
@environment:virtualenv
@email:awc19930818@outlook.com
@github:https://github.com/La0bALanG
@requirement:
"""

import threading
import requests
import random
import time
from urllib import parse
from lxml import etree
from fake_useragent import UserAgent
from hashlib import md5

"""

实现目标：
    破解有道翻译接口，抓取对应翻译结果

目标展示：
    输入原文：你好
    翻译结果：hello

实现步骤：
    1、浏览器F12开启网络抓包,Network-XHR,页面翻译单词后找Form表单数据
    2、在页面中多翻译几个单词，观察Form表单数据变化（有数据是加密字符串）
    3、刷新有道翻译页面，抓取并分析JS代码（本地JS加密）
    4、找到JS加密算法，用Python按同样方式加密生成加密数据
    5、将Form表单数据处理为字典，通过requests.post()的data参数发送
    
实现思路：
    1.F12抓包，一次翻译请求后查看对应form表单数据(有道翻译请求为异步AJAX加载，直接在XHR内部查看即可)
    查找到的form表单数据如下：
    
        i: 电话
        from: AUTO
        to: AUTO
        smartresult: dict
        client: fanyideskweb
        salt: 15997921298483
        sign: 8d61b0f42e54f5901012f69540fc918b
        lts: 1599792129848
        bv: e915c77f633538e8cf44c657fe201ebb
        doctype: json
        version: 2.1
        keyfrom: fanyi.web
        action: FY_BY_REALTlME

    在页面中多翻译几个单词，查看form表单的数据变化：
    
        i: 朋友
        from: AUTO
        to: AUTO
        smartresult: dict
        client: fanyideskweb
        salt: 15997929113988
        sign: 04852e09170834a641b8ab0acff7b6ef
        lts: 1599792911398
        bv: e915c77f633538e8cf44c657fe201ebb
        doctype: json
        version: 2.1
        keyfrom: fanyi.web
        action: FY_BY_REALTlME

    观察发现：不同翻译结果的情况下发生改变的参数为：
    
        salt: 15997921298483
        sign: 8d61b0f42e54f5901012f69540fc918b
        lts: 1599792129848
        bv: e915c77f633538e8cf44c657fe201ebb
        
    3.破解加密：一般为本地js文件加密，刷新一下页面，找到js文件并分析js代码
    如何查找对应的js文件：
        # 方法1
        Network - JS选项 - 搜索关键词salt
        # 方法2
        控制台右上角 - Search - 搜索salt - 查看文件 - 格式化输出
        # 最终找到相关JS文件 : fanyi.min.js
        
    按照如上方法，搜索关键词，例如搜索salt，左侧列出salt关键词存在的js文件为fanyi.min.js
    进入该js文件，继续搜索salt关键词，对多个关键词结果进行筛选，最终在如下js代码中发现关键信息：
    
     var r = function(e) {
        var t = n.md5(navigator.appVersion)
          , r = "" + (new Date).getTime()
          , i = r + parseInt(10 * Math.random(), 10);
        return {
            ts: r,
            bv: t,
            salt: i,
            sign: n.md5("fanyideskweb" + e + i + "]BjuETDhU)zqSxf-=B#7m")
        }
    };
    
    分析如上代码得知：
        1.ts为13位时间戳，字符串类型，对应data中的lts参数
            js代码实现："" + (new Date).getTime()
            python代码实现：str(int(time.time()) * 1000)
        2.salt:ts + 某一随机数，其随机数规律如下：
            js代码实现：r(ts) + parseInt(10 * Math.random(), 10)
            python代码实现：ts+str(random.randint(0,9))
            
        3.sign（设置断点调试，来查看 e 的值，发现 e 为要翻译的单词）
        js代码实现: n.md5("fanyideskweb" + e + salt + "n%A-rKaT5fb[Gy?;N5@Tj")
        python实现:
            from hashlib import md5
            string = "fanyideskweb" + word + salt + "n%A-rKaT5fb[Gy?;N5@Tj"
            s = md5()
            s.update(string.encode())
            sign = s.hexdigest()
"""



class YouDaoTransforSpider(object):
    '''

        面向对象思路：
        1.拆分功能细节。整体程序可拆分为:
            1.发请求获得页面
            2.解析页面
            3.持久化存储(写入文件保存)
        2.结合开闭原则，封装功能方法为私有方法，对外提供统一公共接口
        3.采用单例模式：假设本爬虫程序在多个时间、不同情况下多次使用，单例模式实现只创建一个对象，提升性能避免内存占用过高。

        '''

    _instance_lock = threading.Lock()

    # 单例模式实现：__new__方法
    def __new__(cls, *args, **kwargs):
        if not hasattr(YouDaoTransforSpider, '_instance'):
            with YouDaoTransforSpider._instance_lock:
                if not hasattr(YouDaoTransforSpider, '_instance'):
                    YouDaoTransforSpider._instance = object.__new__(cls)
        return YouDaoTransforSpider._instance

    def __init__(self):
        self.__url = 'http://fanyi.youdao.com/translate_o?smartresult=dict&smartresult=rule'
        self.__headers = {
            'Cookie':'OUTFOX_SEARCH_USER_ID=1559141275@10.169.0.83; JSESSIONID=aaaUEr86rzfeo7xp8b7rx; OUTFOX_SEARCH_USER_ID_NCOO=1009771993.8014448; ___rl__test__cookies=1599793115062',
            'Referer': 'http: // fanyi.youdao.com /',
            'User-Agent':'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/85.0.4183.83 Safari/537.36'
        }

    def __get_salt_sign_ts(self,word):

        #ts
        ts = str(int(time.time()) * 1000)

        #salt
        salt = ts + str(random.randint(0,9))

        #sign
        string = "fanyideskweb" + word + salt + "]BjuETDhU)zqSxf-=B#7m"
        s = md5()
        s.update(string.encode())
        sign = s.hexdigest()

        return salt,sign,ts

    def __get_data(self,word):
        salt,sign,ts = self.__get_salt_sign_ts(word)

        #设置提交数据格式
        data = {
            'i': word,
            'from': 'AUTO',
            'to': 'AUTO',
            'smartresult': 'dict',
            'client': 'fanyideskweb',
            'salt': salt,
            'sign': sign,
            'lts': ts,
            'bv': 'e915c77f633538e8cf44c657fe201ebb',
            'doctype': 'json',
            'version': '2.1',
            'keyfrom': 'fanyi.web',
            'action':'FY_BY_REALTlME'
        }

        return requests.post(url=self.__url,data=data,headers=self.__headers).json()['translateResult'][0][0]['tgt']

    def display(self):
        word = input('请输入要翻译的单词：')
        tre_word = self.__get_data(word)
        print('翻译后的结果：%s'%tre_word)
def test():
    YouDaoTransforSpider().display()

if __name__ == '__main__':
    test()
```

## 思考：手动修改headers或form表单数据相对麻烦，是否有简便的方式？

```python
借助正则表达式处理headers，方便快速修改格式并使用。

举个栗子：

headers：

"""
Accept: application/json, text/javascript, */*; q=0.01
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9
Connection: keep-alive
Content-Length: 248
Content-Type: application/x-www-form-urlencoded; charset=UTF-8
Cookie: OUTFOX_SEARCH_USER_ID=1559141275@10.169.0.83; JSESSIONID=aaaUEr86rzfeo7xp8b7rx; OUTFOX_SEARCH_USER_ID_NCOO=1009771993.8014448; ___rl__test__cookies=1599804152408
Host: fanyi.youdao.com
Origin: http://fanyi.youdao.com
Referer: http://fanyi.youdao.com/
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/85.0.4183.83 Safari/537.36
X-Requested-With: XMLHttpRequest

"""
    
form表单数据：
"""
i: 朋友
from: zh-CHS
to: en
smartresult: dict
client: fanyideskweb
salt: 15998041524052
sign: bf3ecd8f4c8a282ed79468f49aeb69fd
lts: 1599804152405
bv: e915c77f633538e8cf44c657fe201ebb
doctype: json
version: 2.1
keyfrom: fanyi.web
action: lan-select

"""
    

# -*- coding:utf-8 _*-
"""
@version:
author:安伟超
@time: 2020/09/11
@file: demo09_re_headers_and_formData.py.py
@environment:virtualenv
@email:awc19930818@outlook.com
@github:https://github.com/La0bALanG
@requirement:使用正则表达式预处理headers及form表单数据
"""

import re

class demoSpider(object):

    def __init__(self):
        self.__headers = """
Accept: application/json, text/javascript, */*; q=0.01
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9
Connection: keep-alive
Content-Length: 248
Content-Type: application/x-www-form-urlencoded; charset=UTF-8
Cookie: OUTFOX_SEARCH_USER_ID=1559141275@10.169.0.83; JSESSIONID=aaaUEr86rzfeo7xp8b7rx; OUTFOX_SEARCH_USER_ID_NCOO=1009771993.8014448; ___rl__test__cookies=1599804152408
Host: fanyi.youdao.com
Origin: http://fanyi.youdao.com
Referer: http://fanyi.youdao.com/
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/85.0.4183.83 Safari/537.36
X-Requested-With: XMLHttpRequest
"""
        self.__formData = """
i: 朋友
from: zh-CHS
to: en
smartresult: dict
client: fanyideskweb
salt: 15998041524052
sign: bf3ecd8f4c8a282ed79468f49aeb69fd
lts: 1599804152405
bv: e915c77f633538e8cf44c657fe201ebb
doctype: json
version: 2.1
keyfrom: fanyi.web
action: lan-select
        """

    def re_parse(self,str_data):
        dict = {}
        for x,y in re.findall('(.*):(.*)',str_data):
            dict[x] = y.strip()
        return dict

    def display(self):
        headers = self.re_parse(self.__headers)
        form_data = self.re_parse(self.__formData)
        print(headers)
        print(form_data)

demoSpider().display()
```

## 总结：常见基本反制爬虫策略(反爬机制)及处理方式

```python
1、Headers反爬虫 ：Cookie、Referer、User-Agent
	解决方案: 通过F12获取headers,传给requests.get()方法
2、IP限制 ：网站根据IP地址访问频率进行反爬,短时间内限制IP访问
	解决方案:
        1、构造自己IP代理池,每次访问随机选择代理,经常更新代理池
        2、购买开放代理或私密代理IP
        3、降低爬取的速度
3、User-Agent限制 ：类似于IP限制
	解决方案: 构造自己的User-Agent池,每次访问随机选择
4、对响应内容做处理
	解决方案: 打印并查看响应内容,用xpath或正则做处理
5.动态页面技术
	采用AJAX异步加载数据包，增加数据获取难度
```

# 案例11：民政部网站抓取2020年全国最新行政区划代码

```python
#---------------------无增量版-------------------------------

# -*- coding:utf-8 _*-
"""
@version:
author:安伟超
@time: 2020/09/14
@file: demo11_GetGovementAdministrativeArea_OOP.py.py
@environment:virtualenv
@email:awc19930818@outlook.com
@github:https://github.com/La0bALanG
@requirement:
"""

import requests
import threading
from lxml import etree
import re
from fake_useragent import UserAgent


"""

目标
1.目标url：http://www.mca.gov.cn/ - 民政数据 - 行政区划代码
   即: http://www.mca.gov.cn/article/sj/xzqh/2019/
   
2.目标数据: 抓取最新中华人民共和国县以上行政区划代码

实现思路：

1.分析页面及url
    1.请求民政部官网，进入-民政数据-行政区划代码 选项
    2.F12开启控制台，抓手工具抓到：
        
	
        2020年7月份县以上行政区划代码
        2020-09-08
            
        2020年7月份县以下区划变更情况
        2020-09-08
            
        2020年6月份县以上行政区划代码
        2020-08-31
            
        2020年6月份县以下区划变更情况
        2020-08-31
            
        2020年5月份县以上行政区划代码
        
    3.查看elements：
    <a class="artitlelist" href="/article/sj/xzqh/2020/202009/20200900029334.shtml" target="_blank" title="2020年7月份县以上行政区划代码">2020年7月份县以上行政区划代码</a>
    目标链接在上述a标签的href属性
    但！这是假链接！
    
    测试：
        现在向该链接(假链接)直接请求行政区划代码详情页，会直接跳转为一个.html页面(真链接)的响应内容，在控制台的response中确实能看到所需数据，但此为.html页面的相应内容，使用python代码直接请求假页面得到的response却根本没有所需数据！
        
    但是，在假页面的响应内容中，存在如下一段js代码：
    <script>
     window.location.href="http://www.mca.gov.cn//article/sj/xzqh/2020/2020/20200908007001.html";
    </script>
    
    我们真正想要的真链接其实在这里！
    
    没错，这也是常见的一种反爬手段，通过伪造url隐藏真实请求的url。
    
    但，又能奈我何！请求假页面，提取js中的真链接不就行了？

2.拿到真链接。
3.请求真链接的response。
4.解析，持久化存储
    
实现步骤：
1.请求行政区划代码页面，解析html，得到假url；
2.请求假链接页面response，解析js脚本，获取真实链接；
3.向真实链接请求最终数据
4.解析，持久化存储


"""



class GetGovementAdministrativeAreaSpider(object):
    '''

            面向对象思路：
            1.拆分功能细节。整体程序可拆分为:
                1.发请求获得页面
                2.解析页面
                3.持久化存储(写入文件保存)
            2.结合开闭原则，封装功能方法为私有方法，对外提供统一公共接口
            3.采用单例模式：假设本爬虫程序在多个时间、不同情况下多次使用，单例模式实现只创建一个对象，提升性能避免内存占用过高。

	'''

    _instance_lock = threading.Lock()

    # 单例模式实现：__new__方法
    def __new__(cls, *args, **kwargs):
        if not hasattr(GetGovementAdministrativeAreaSpider, '_instance'):
            with GetGovementAdministrativeAreaSpider._instance_lock:
                if not hasattr(GetGovementAdministrativeAreaSpider, '_instance'):
                    GetGovementAdministrativeAreaSpider._instance = object.__new__(cls)
        return GetGovementAdministrativeAreaSpider._instance

    def __init__(self):
        self.__url = 'http://www.mca.gov.cn/article/sj/xzqh/2020/'
        self.__headers = {
            'User-Agent':UserAgent().random
        }

    @property
    def url(self):
        return self.__url

    @property
    def headers(self):
        return self.__headers

    def __get_html(self,url,headers):
        return requests.get(url=url,headers=headers)

    #请求一级页面，解析、构造假链接
    def __get_false_url(self):
        html = self.__get_html(self.__url,self.__headers).text
        dom = etree.HTML(html)
        #只需要最新的，第一个肯定是最新的
        a = dom.xpath('//a[@class="artitlelist"]')[0]
        #获取节点对象的title属性
        title = a.get('title')
        #解析所有以“代码”结尾的title
        if title.endswith('代码'):
            return 'http://www.mca.gov.cn' + a.get('href')#获取节点对象的href属性

    def __get_true_url(self,false_url):
        # 先获取假链接的响应,然后根据响应获取真链接
        html = self.__get_html(url=false_url,headers=self.__headers).text
        # 利用正则提取真实链接
        return re.findall(r'window.location.href="(.*?)"',html)[0]

    #请求真实页面，解析数据
    def __parse_html(self,true_url):
        html = self.__get_html(url=true_url,headers=self.__headers).text
        dom = etree.HTML(html)
        tr_lists = dom.xpath('//tr[@height="19"]')
        for tr in tr_lists:
            code = tr.xpath('./td[2]/text()')
            name = tr.xpath('./td[3]/text()')
            if len(code) and len(name) != 0:
                self.__save_html(code[0].strip(),name[0].strip())
            else:
                pass

    def __save_html(self,code,name):
        print('开始写入行政区划代码...')
        with open('Area_code.txt','a') as f:
            print('写入%s...'%name)
            f.write(code + ':' + name + '\n')
        print('写入完毕.')

    def display(self):
        self.__parse_html(self.__get_true_url(self.__get_false_url()))

def test():
    GetGovementAdministrativeAreaSpider().display()

if __name__ == '__main__':
    test()
    
    

    
    
#---------------增量爬虫版------------------------


# -*- coding:utf-8 _*-
"""
@version:
author:安伟超
@time: 2020/09/14
@file: demo11_GetGovementAdministrativeArea_OOP.py.py
@environment:virtualenv
@email:awc19930818@outlook.com
@github:https://github.com/La0bALanG
@requirement:
"""

import requests
import threading
import re
import time
import sys
from lxml import etree
from fake_useragent import UserAgent

"""

目标
1.目标url：http://www.mca.gov.cn/ - 民政数据 - 行政区划代码
   即: http://www.mca.gov.cn/article/sj/xzqh/2019/

2.目标数据: 抓取最新中华人民共和国县以上行政区划代码

实现思路：

1.分析页面及url
    1.请求民政部官网，进入-民政数据-行政区划代码 选项
    2.F12开启控制台，抓手工具抓到：


        2020年7月份县以上行政区划代码
        2020-09-08

        2020年7月份县以下区划变更情况
        2020-09-08

        2020年6月份县以上行政区划代码
        2020-08-31

        2020年6月份县以下区划变更情况
        2020-08-31

        2020年5月份县以上行政区划代码

    3.查看elements：
    <a class="artitlelist" href="/article/sj/xzqh/2020/202009/20200900029334.shtml" target="_blank" title="2020年7月份县以上行政区划代码">2020年7月份县以上行政区划代码</a>
    目标链接在上述a标签的href属性
    但！这是假链接！

    测试：
        现在向该链接(假链接)直接请求行政区划代码详情页，会直接跳转为一个.html页面(真链接)的响应内容，在控制台的response中确实能看到所需数据，但此为.html页面的相应内容，使用python代码直接请求假页面得到的response却根本没有所需数据！

    但是，在假页面的响应内容中，存在如下一段js代码：
    <script>
     window.location.href="http://www.mca.gov.cn//article/sj/xzqh/2020/2020/20200908007001.html";
    </script>

    我们真正想要的真链接其实在这里！

    没错，这也是常见的一种反爬手段，通过伪造url隐藏真实请求的url。

    但，又能奈我何！请求假页面，提取js中的真链接不就行了？

2.拿到真链接。
3.请求真链接的response。
4.解析，持久化存储

实现步骤：
1.请求行政区划代码页面，解析html，得到假url；
2.请求假链接页面response，解析js脚本，获取真实链接；
3.向真实链接请求最终数据
4.解析，持久化存储


"""


class GetGovementAdministrativeAreaSpider(object):
    '''

            面向对象思路：
            1.拆分功能细节。整体程序可拆分为:
                1.发请求获得页面
                2.解析页面
                3.持久化存储(写入文件保存)
            2.结合开闭原则，封装功能方法为私有方法，对外提供统一公共接口
            3.采用单例模式：假设本爬虫程序在多个时间、不同情况下多次使用，单例模式实现只创建一个对象，提升性能避免内存占用过高。

            '''

    _instance_lock = threading.Lock()

    # 单例模式实现：__new__方法
    def __new__(cls, *args, **kwargs):
        if not hasattr(GetGovementAdministrativeAreaSpider, '_instance'):
            with GetGovementAdministrativeAreaSpider._instance_lock:
                if not hasattr(GetGovementAdministrativeAreaSpider, '_instance'):
                    GetGovementAdministrativeAreaSpider._instance = object.__new__(cls)
        return GetGovementAdministrativeAreaSpider._instance

    def __init__(self):
        self.__url = 'http://www.mca.gov.cn/article/sj/xzqh/2020/'
        self.__headers = {
            'User-Agent': UserAgent().random
        }
        self.__year = ''

    @property
    def url(self):
        return self.__url

    @property
    def headers(self):
        return self.__headers

    @property
    def year(self):
        return self.__year

    def __get_html(self, url, headers):
        return requests.get(url=url, headers=headers)

    # 请求一级页面，解析、构造假链接
    def __get_false_url(self):
        html = self.__get_html(self.__url, self.__headers).text
        dom = etree.HTML(html)
        # 只需要最新的，第一个肯定是最新的
        self.__year = dom.xpath('//li/a[@id="shttnav1"][1]/text()')[0]
        a = dom.xpath('//a[@class="artitlelist"]')[0]
        # 获取节点对象的title属性
        title = a.get('title')
        # 解析所有以“代码”结尾的title
        if title.endswith('代码'):
            return 'http://www.mca.gov.cn' + a.get('href')  # 获取节点对象的href属性

    def __get_true_url(self, false_url):
        # 先获取假链接的响应,然后根据响应获取真链接
        html = self.__get_html(url=false_url, headers=self.__headers).text
        # 利用正则提取真实链接
        return re.findall(r'window.location.href="(.*?)"', html)[0]

    # 请求真实页面，解析数据
    def __parse_html(self, true_url):
        html = self.__get_html(url=true_url, headers=self.__headers).text
        dom = etree.HTML(html)
        tr_lists = dom.xpath('//tr[@height="19"]')
        for tr in tr_lists:
            code = tr.xpath('./td[2]/text()')
            name = tr.xpath('./td[3]/text()')
            if len(code) and len(name) != 0:
                self.__save_html(code[0].strip(), name[0].strip())
            else:
                pass

    def __save_html(self, code, name):
        print('开始写入行政区划代码...')
        filename = self.__year[0:4] + '_Area_code.txt'
        with open(filename, 'a') as f:
            print('写入%s...' % name)
            f.write(code + ':' + name + '\n')
        print('写入完毕.')

    def __Incremental_crawler_simple(self):
        """

        增量爬虫：网站有更新时爬取，无更新时不爬取

        此案例下最简单的增量算法：判断行政区划代码页面第一个是否为当年最新行政区划，是则爬取新代码，否则不爬取
        思路：
            1.解析假url过程中顺带解析“2020年中华人民共和国行政区划代码”该文本
            2.解析出后提取年数信息
            3.time模块获取系统当前时间(获取年份)
            4.判断：解析出的年份与系统年份相符，则未更新，不爬取,否则整体重新爬取行政区划代码

        """

        year = self.__year[0:4]
        os_time = time.strftime('%Y-%m-%d %H:%M:%S')[0:4]
        if year == os_time:
            print('行政区划代码暂无更新，不爬取')
        else:
            update = input('行政区划代码已更新，是否现在立即更新?(y/n):')
            if update == 'y':
                self.__parse_html(self.__get_true_url(self.__get_false_url()))
            else:
                print('暂不更新，增量算法结束，程序执行完毕')
                sys.exit()



    def display(self):
        # self.__parse_html(self.__get_true_url(self.__get_false_url()))
        self.__Incremental_crawler_simple()


def test():
    GetGovementAdministrativeAreaSpider().display()


if __name__ == '__main__':
    test()
```

# 案例12：豆瓣电影评分数据抓取

```python
# -*- coding:utf-8 _*-
"""
@version:
author:安伟超
@time: 2020/09/15
@file: demo12_DouBanMovieComments_OOP.py.py
@environment:virtualenv
@email:awc19930818@outlook.com
@github:https://github.com/La0bALanG
@requirement:豆瓣电影评分数据抓取
"""

import requests
import threading
import re
import time
import random
from fake_useragent import UserAgent


"""

实现思路

思路：
1.目标数据
    地址: 豆瓣电影 - 排行榜 - 剧情
    目标: 电影名称、电影评分
    
2.F12控制台抓包分析
    1.先检索我们所需的第一目标数据：电影名称、电影评分
        F12 -- network -- XHR -- 鼠标滚动不断刷新页面 -- 查看左侧AJAX异步加载项 -- preview 
        
        分析多次刷新规律得知该AJAX接口请求的路径如下：
        https://movie.douban.com/j/chart/top_list?type=11&interval_id=100%3A90&action=&start=0&limit=20
        由此得到基准URL格式：
        https://movie.douban.com/j/chart/top_list?
        后续的参数在请求时通过parmas参数拼接传入
        
        得到的一次AJAX请求的response结果如下：
        [
            {"rating":["9.4","50"],"rank":21,"cover_url":"https://img2.doubanio.com\/view\/photo\/s_ratio_poster\/public\/p2329626263.jpg","is_playable":false,"id":"20326557","types":["剧情","爱情","音乐"],"regions":["法国"],"title":"巴黎圣母院","url":"https:\/\/movie.douban.com\/subject\/20326557\/","release_date":"1998","actor_count":7,"vote_count":9691,"score":"9.4","actors":["海伦娜·赛加拉","加劳","丹尼尔·拉沃伊","布鲁诺·佩尔蒂埃","帕特里克·费欧里","拉克·默维尔","朱丽叶·泽纳缇"],"is_watched":false},
            {"rating":["9.4","50"],"rank":22,"cover_url":"https://img9.doubanio.com\/view\/photo\/s_ratio_poster\/public\/p2224933614.jpg","is_playable":false,"id":"25928148","types":["剧情","爱情","歌舞"],"regions":["法国"],"title":"罗密欧与朱丽叶","url":"https:\/\/movie.douban.com\/subject\/25928148\/","release_date":"2002-02-06","actor_count":4,"vote_count":4782,"score":"9.4","actors":["达米安·萨格","希西莉亚·卡拉","葛里高利·巴奎特","Tom Ross"],"is_watched":false},
            {"rating":["9.3","50"],"rank":23,"cover_url":"https://img2.doubanio.com\/view\/photo\/s_ratio_poster\/public\/p2616355133.jpg","is_playable":true,"id":"3541415","types":["剧情","科幻","悬疑","冒险"],"regions":["美国","英国"],"title":"盗梦空间","url":"https:\/\/movie.douban.com\/subject\/3541415\/","release_date":"2010-09-01","actor_count":28,"vote_count":1570120,"score":"9.3","actors":["莱昂纳多·迪卡普里奥","约瑟夫·高登-莱维特","艾伦·佩吉","汤姆·哈迪","渡边谦","迪利普·劳","基里安·墨菲","汤姆·贝伦杰","玛丽昂·歌迪亚","皮特·波斯尔思韦特","迈克尔·凯恩","卢卡斯·哈斯","李太力","克莱尔·吉尔蕾","马格努斯·诺兰","泰勒·吉蕾","乔纳森·吉尔","水源士郎","冈本玉二","厄尔·卡梅伦","瑞恩·海沃德","米兰达·诺兰","拉什·费加","蒂姆·科勒赫","妲露拉·莱莉","迈克尔·加斯顿","吉尔·马德雷尔","玛格丽特·因索利亚"],"is_watched":false},
            ....
        ]
    
        我们所需的目标数据：电影名称、电影评分分别在每一个大字典的title 及 score字段。

    2.再依次检索第二目标数据：某分类电影总数
        F12 -- network -- XHR -- 鼠标滚动不断刷新页面 -- 查看左侧AJAX异步加载项 -- preview 
        
        观察AJAX请求项得知该AJAX接口请求的URL如下：
        https://movie.douban.com/j/chart/top_list_count?type=11&interval_id=100%3A90
        其中type参数可由程序得到，即该请求的URL基本格式如下：
        'https://movie.douban.com/j/chart/top_list_count?type={}&interval_id=100%3A90'
        
        得到的一次AJAX请求的response如下：
        {"playable_count":380,"total":716,"unwatched_count":716}
        
        total字段为当前某分类下的电影总数量
        
    3.最后检索第三目标数据：所有的电影分类名称及其对应的type值
    
        请求URL：https://movie.douban.com/chart
        F12 -- elements -- 抓手 -- 抓到分类级联菜单
        
        <div>
      <h2>分类排行榜 · · · · · ·<img style=" position: absolute;" src="https://img3.doubanio.com/f/shire/e49eca1517424a941871a2667a8957fd6c72d632/pics/new_menu.gif"></h2>
      <div class="types">
          <span><a href="/typerank?type_name=剧情&type=11&interval_id=100:90&action=">剧情</a></span>
          <span><a href="/typerank?type_name=喜剧&type=24&interval_id=100:90&action=">喜剧</a></span>
          <span><a href="/typerank?type_name=动作&type=5&interval_id=100:90&action=">动作</a></span>
          <span><a href="/typerank?type_name=爱情&type=13&interval_id=100:90&action=">爱情</a></span>
          <span><a href="/typerank?type_name=科幻&type=17&interval_id=100:90&action=">科幻</a></span>
          <span><a href="/typerank?type_name=动画&type=25&interval_id=100:90&action=">动画</a></span>
          <span><a href="/typerank?type_name=悬疑&type=10&interval_id=100:90&action=">悬疑</a></span>
          ...
          
        所需的类型名称及对应的type值在a标签的href属性中，采用正则表达式提取：
        r'<a href=.*?type_name=(.*?)&type=(.*?)&.*?</a>'
        
实现步骤：
1.确定基准URL
2.向第二目标数据的AJAX接口发送请求获取电影总数
3.向第三目标数据的URL页面发起请求获取电影分类名称及对应type值
4.拼接parmas参数
3.向第一目标数据的AJAX接口发送请求，获取电影名称及其对应评分      

"""


class DouBanMovieCommentsSpider(object):
    '''

                面向对象思路：
                1.拆分功能细节。整体程序可拆分为:
                    1.发请求获得页面
                    2.解析页面
                    3.持久化存储(写入文件保存)
                2.结合开闭原则，封装功能方法为私有方法，对外提供统一公共接口
                3.采用单例模式：假设本爬虫程序在多个时间、不同情况下多次使用，单例模式实现只创建一个对象，提升性能避免内存占用过高。

                '''

    _instance_lock = threading.Lock()

    # 单例模式实现：__new__方法
    def __new__(cls, *args, **kwargs):
        if not hasattr(DouBanMovieCommentsSpider, '_instance'):
            with DouBanMovieCommentsSpider._instance_lock:
                if not hasattr(DouBanMovieCommentsSpider, '_instance'):
                    DouBanMovieCommentsSpider._instance = object.__new__(cls)
        return DouBanMovieCommentsSpider._instance

    def __init__(self):
        self.__url = 'https://movie.douban.com/j/chart/top_list?'
        self.__headers = {
            'User-Agent':UserAgent().random
        }
        self.__i = 0

    def __get_page(self,parmas):
        return requests.get(url=self.__url,params=parmas,headers=self.__headers).json()

    def __parse_html(self,html):
        dict = {}
        # 调用get_page返回的响应为大列表：[{电影1信息},{},...,{}]
        for item in html:
            dict[item['title'].strip()] = float(item['score'].strip())
            # dict['name'] = item['title'].strip()
            # dict['score'] = float(item['score'].strip())
            self.__i += 1
        print(dict)

    def __get_total(self,type_number):

        #控制台抓包得到的另一XHR请求对象
        url = 'https://movie.douban.com/j/chart/top_list_count?type={}&interval_id=100%3A90'.format(type_number)
        return int(requests.get(url=url,headers=self.__headers).json()['total'])

    #获取所有电影分类名称及其对应type值
    def __get_all_type(self):
        # 获取类型码
        url = 'https://movie.douban.com/chart'
        html = requests.get(url=url, headers=self.__headers).text
        r_list = re.findall(r'<a href=.*?type_name=(.*?)&type=(.*?)&.*?</a>',html)
        # 存放所有类型和对应类型码大字典
        type_dict = {}
        menu = ''
        for r in r_list:
            type_dict[r[0].strip()] = r[1].strip()
            # 获取input的菜单，显示所有电影类型
            menu += r[0].strip() + '|'
        return type_dict, menu


    def display(self):
        type_dict, menu = self.__get_all_type()
        menu = menu + '\n请做出你的选择：'
        name = input(menu)
        type_number = type_dict[name]
        total = self.__get_total(type_number)
        for begin in range(0,(total + 1),20):
            parmas = {
                'type': type_number,
                'interval_id': '100:90',
                'action': '',
                'start': str(begin),
                'limit': '20'
            }
            self.__parse_html(self.__get_page(parmas))
            time.sleep(random.randint(0,3))
        print('电影数量：%d'%self.__i)

def test():
    DouBanMovieCommentsSpider().display()

if __name__ == '__main__':
    test()
```

# 自动化测试工具Selenium + Webdriver模拟浏览器操作

## selenium介绍

### 简介

> Selenium是一个用于Web应用程序测试的工具。Selenium测试直接运行在浏览器中，就像真正的用户在操作一样。支持的浏览器包括IE（7, 8, 9, 10, 11），[Mozilla Firefox](https://baike.baidu.com/item/Mozilla Firefox/3504923)，Safari，Google Chrome，Opera等。这个工具的主要功能包括：测试与浏览器的兼容性——测试你的应用程序看是否能够很好得工作在不同浏览器和操作系统之上。测试系统功能——创建回归测试检验软件功能和用户需求。支持自动录制动作和自动生成 .Net、Java、Perl等不同语言的测试脚本。
>
> 注意：selenium只是一个工具，必须与第三方浏览器结合才能使用。

### 安装

```python
pip install selenium
```

## phantomjs浏览器

> 无界面浏览器(又称无头浏览器)，在内存中进行页面加载,高效.
>
> PhantomJS的适用范围就是无头浏览器的适用范围。通常无头浏览器可以用于页面自动化，网页监控，网络爬虫等：
>
> - 页面自动化测试：希望自动的登陆网站并做一些操作然后检查结果是否正常。
> - 网页监控：希望定期打开页面，检查网站是否能正常加载，加载结果是否符合预期。加载速度如何等。
> - 网络爬虫：获取页面中使用js来下载和渲染信息，或者是获取链接处使用js来跳转后的真实地址。

## phantomjs、chromedriver、geckodriver安装

> 下载地址:
>
> ​	1、chromedriver : 下载对应版本 http://chromedriver.storage.googleapis.com/index.html 
>
> ​	2、geckodriver https://github.com/mozilla/geckodriver/releases 
>
> ​	3、phantomjs https://phantomjs.org/download.html
>
> 安装：
>
> ​	windows：
>
> ​		1.phantomjs：下载后解压到某目录，直接将其路径添加进系统path环境变量即可。
>
> ​		2.chromedriver、geckodriver ：把解压后得到的chromedriver.exe、GeckoDriver.exe拷贝到python安装目录的Scripts目录下(添加到系统环境变量) 
>
> ​		查看python安装路径: where python
>
> ​	Linux：
>
> ​		1、下载后解压 tar -zxvf geckodriver.tar.gz 
>
> ​		2、拷贝解压后文件到 /usr/bin/ （添加环境变量） sudo cp geckodriver /usr/bin/ 
>
> ​		3、更改权限 sudo -i cd /usr/bin/ chmod 777 geckodriver

## 简单示例：使用selenium+浏览器打开百度首页

```python
from selenium import webdriver

browser = webdriver.Chrome()
browser.get('https://www.baidu.com')
browser.quit()
```

## 浏览器对象方法

### 常用基本方法

```python
加载浏览器驱动： webdriver.Firefox()

打开页面：get()

关闭浏览器：quit()

最大化窗口： maximize_window()

设置窗口参数：set_window_size(600,800)

后退到前一页： back()

前进到后一页： forward()

刷新页面： refresh()

获得title并打印:title
```

### 元素定位方法

```python
单元素定位
    id定位：find_element_by_id()
    name定位：find_element_by_name()
    class定位：find_element_by_class_name()
    tag定位：find_element_by_tag_name()
    link定位：find_element_by_link_text()
    partial link 定位： find_element_by_partial_link_text()
    Xpath定位:
        绝对路径：find_element_by_xpath("绝对路径")
        元素属性：find_element_by_xpath("//unput[@id='kw']")
        层级与属性结合：find_element_by_xpath("//form[@id='loginForm']/ul/input[1]")
        逻辑运算符：find_element_by_xpath("//input[@id='kw' and@class='s_ipt']")

    CSS定位：find_element_by_css_selector(选择器)
多元素定位
    browser.find_elements_by_id('')
    browser.find_elements_by_name('')
    browser.find_elements_by_class_name('')
    browser.find_elements_by_xpath('')
    ... ...
节点对象操作
    ele.send_keys('') # 搜索框发送内容
    ele.click()
    ele.text # 获取文本内容，包含子节点和后代节点的文本内容
    ele.get_attribute('src') # 获取属性值
```

## 键盘事件方法

```python
from selenium.webdriver.common.keys import Keys
browser = webdriver.Chrome()
browser.get('http://www.baidu.com/')
# 1、在搜索框中输入"selenium"
browser.find_element_by_id('kw').send_keys('赵丽颖')
# 2、输入空格
browser.find_element_by_id('kw').send_keys(Keys.SPACE)
# 3、Ctrl+a 模拟全选
browser.find_element_by_id('kw').send_keys(Keys.CONTROL, 'a')
# 4、Ctrl+c 模拟复制
browser.find_element_by_id('kw').send_keys(Keys.CONTROL, 'c')
# 5、Ctrl+v 模拟粘贴
browser.find_element_by_id('kw').send_keys(Keys.CONTROL, 'v')
# 6、输入回车,代替 搜索 按钮
browser.find_element_by_id('kw').send_keys(Keys.ENTER)
```

## 鼠标事件方法

```python
from selenium import webdriver
# 导入鼠标事件类
from selenium.webdriver import ActionChains
driver = webdriver.Chrome()
driver.get('http://www.baidu.com/')
#移动到 设置，perform()是真正执行操作，必须有
element = driver.find_element_by_xpath('//*[@id="u1"]/a[8]')
ActionChains(driver).move_to_element(element).perform()
#单击，弹出的Ajax元素，根据链接节点的文本内容查找
driver.find_element_by_link_text('高级搜索').click()
```

## selenium切换页面

> 页面中点开链接出现新的页面，但是浏览器对象browser还是之前页面的对象

```python
# 获取当前所有句柄（窗口）
all_handles = browser.window_handles
# 切换browser到新的窗口，获取新窗口的对象
browser.switch_to.window(all_handles[1])
```

## iframe子框架

> 网页中嵌套了网页，先切换到iframe子框架，然后再执行其他操作

```python
browser.switch_to.iframe(iframe_element)
```

# 多进程、多线程爬虫技术

- 意义：充分利用计算机CPU的多核资源，同时处理多个应用程序任务，以便提高程序的运行效率。
- 实现方案：多进程、多线程

## 进程(Process)理论基础

### 定义

> - 程序在计算机中的一次运行。
> - 程序是一个可执行文件，以静态的方式占有磁盘空间。
> - 进程是一个动态的过程描述，占有计算机的运行资源，有一定的生命周期。

### 系统如何产生一个进程

> - 用户空间通过调用程序接口或者命令发起请求
> - 操作系统接受用户请求，开始创建进程
> - 操作系统调配计算机资源，确定进程状态等
> - 操作系统将创建的进程提供给用于使用



![linux](F:\老安课程串讲资料\老安精品——全课程&全技术方向资料笔记汇总\老安资料2020新版(Version2.0)\(10)Spider\IO并发编程\img\linux.png)



### 进程基本概念

> - CPU时间片：如果一个进程占有CPU内核则称这个进程在CPU时间片上。
>
> - PCB:进程控制块，在内存中开辟的一块存储空间，用于存放进程的基本信息，也用于系统查找识别进程。
>
> - 进程ID：PID，系统为每个进程分配的一个大于0的证书，作为进程ID。每个进程ID是不可能重复的。
>
> - 父子进程：系统中每一个进程（除了系统初始化进程）都有唯一的父进程，可以有0个或多个子进程。父子进程关系便于进程管理
>
> - 进程状态
>
>   - 三态
>     - 就绪态：进程具备执行条件，等待分配cpu资源
>     - 运行态：进程占有cpu时间片正在运行
>     - 等待态：进程暂时停止运行，让出cpu
>   - 五态（在三态基础上增加）
>     - 新建态：创建一个进程，获取资源的过程
>     - 终止态：进程结束，释放资源的过程
>
> - 状态查看命令：ps -aux  --> STAT列
>
>   S 等待态
>   R 执行态
>   Z 僵尸
>
> - 进程的运行特征
>
>   - 多进程可以更充分使用计算机多核资源
>   - 进程之间的运行互不影响，各自独立
>   - 每个进程拥有独立的空间，各自使用自己的空间资源



![4_3态](F:\老安课程串讲资料\老安精品——全课程&全技术方向资料笔记汇总\老安资料2020新版(Version2.0)\(10)Spider\IO并发编程\img\4_3态.png)



![4_5态](F:\老安课程串讲资料\老安精品——全课程&全技术方向资料笔记汇总\老安资料2020新版(Version2.0)\(10)Spider\IO并发编程\img\4_5态.png)

### 基于fork的多进程

```python
pid = os.fork()
	功能： 创建新的进程
	返回值：整数，如果创建进程失败返回一个负数，如果成功则在原有进程中返回新进程的PID，在新进程中返回0
    
注意:
    子进程会复制父进程全部内存空间，从fork下一句开始执行。
    父子进程各自独立运行，运行顺序不一定。
    利用父子进程fork返回值的区别，配合if结构让父子进程执行不同的内容几乎是固定搭配。
    父子进程有各自特有特征比如PID PCB 命令集等。
    父进程fork之前开辟的空间子进程同样拥有，父子进程对各自空间的操作不会相互影响。
示例代码：
import os
from time import sleep

pid = os.fork()

if pid < 0:
    print("进程创建失败")
elif pid == 0:
    sleep(3)
    print("新的进程")
else:
    sleep(4)
    print("原来的进程")

print("实验完毕")

```

#### 进程相关函数

```python
os.getpid()
	功能： 获取一个进程的PID值
	返回值： 返回当前进程的PID 
os.getppid()
	功能： 获取父进程的PID号
	返回值： 返回父进程PID
os._exit(status)
	功能: 结束一个进程
	参数：进程的终止状态
sys.exit([status])
	功能：退出进程
	参数：整数 表示退出状态
		字符串 表示退出时打印内容
        
代码举例：
"""
获取进程的PID值
"""

import os

pid = os.fork()

if pid < 0:
    print("Error")
elif pid == 0:
    print("Child PID:",os.getpid())
    print("Get Parent PID:",os.getppid())
else:
    print("Get Child PID:",pid)
    print("Parent PID:", os.getpid())
    
"""
进程退出
"""

import os,sys

# os._exit(0)  # 进程退出

sys.exit("Process exit") # 进程退出

print("进程退出")
```

### 孤儿进程与僵尸进程

- 孤儿进程：父进程先于子进程退出，此时子进程成为孤儿进程

  > 特点：孤儿进程会被系统进程收养，此时系统进程就会成为孤儿进程新的父进程，孤儿进程退出该进程会自动处理。

- 僵尸进程：子进程先于父进程退出，父进程有没有处理子进程的退出状态，此时子进程就会成为僵尸进程

  > 特点： 僵尸进程虽然结束，但是会存留部分PCB在内存中，大量的僵尸进程会浪费系统的内存资源。

- 如何避免僵尸进程产生

```python
#使用wait函数处理子进程退出
pid,status = os.wait()
功能：在父进程中阻塞等待处理子进程退出
返回值： pid  退出的子进程的PID
	status  子进程退出状态
    
# 通过信号处理子进程退出
#使用signal模块在父进程创建子进程前写如下语句 ：
import signal
signal.signal(signal.SIGCHLD,signal.SIG_IGN)
#特点：非阻塞，不会影响父进程运行，可以处理所有子进程退出
```

### multiprocessing 模块创建进程

#### 基本语法

```python
Process()
功能 ： 创建进程对象
参数 ： target 绑定要执行的目标函数 
	args 元组，用于给target函数位置传参
	kwargs 字典，给target函数键值传参
```

```python
p.start()
功能 ： 启动进程
```

> 注意:启动进程此时target绑定函数开始执行，该函数作为子进程执行内容，此时进程真正被创建

```python
p.join([timeout])
功能：阻塞等待回收进程
参数：超时时间
```

> 注意
>
> >* 使用multiprocessing创建进程同样是子进程复制父进程空间代码段，父子进程运行互不影响。
> >* 子进程只运行target绑定的函数部分，其余内容均是父进程执行内容。
> >* multiprocessing中父进程往往只用来创建子进程回收子进程，具体事件由子进程完成。
> >* multiprocessing创建的子进程中无法使用标准输入

```python
代码举例1：
"""
multiprocessing 模块创建进程
【1】 将需要子进程执行的事件封装为函数
【2】 通过模块的Process类创建进程对象，关联函数
【3】 通过进程对象调用start启动进程
【4】 通过进程对象调用join回收进程
"""
from time import sleep
import multiprocessing


a = 1

# 进程执行函数
def fun():
    print("开始一个进程")
    sleep(5)
    global a
    print("a = ",a)
    a = 1000
    print("子进程执行结束")


# 创建进程对象
p = multiprocessing.Process(target=fun)

# 启动进程 此时进程诞生 执行函数作为进程的执行内容
p.start()

# 父进程做的
sleep(3)
print("父进程事件")

# 回收进程，防止僵尸进程
p.join(1)
print("==================================")
print("a:",a)


"""
p = os.fork()
if pid == 0:
    fun()
    os._exit()
else:
    os.wait()
"""
```

```python
代码举例2：
"""
process 示例
"""

from multiprocessing import Process
from time import sleep

# 带有参数的进程函数
def worker(sec,name):
    for i in range(3):
        sleep(sec)
        print("I'm %s"%name)
        print("I'm working...")

# 位置传参
# p = Process(target=worker,args=(2,'Lucy'))

# 关键字传参
p = Process(target=worker,args=(2,),kwargs={'name':'Lily'})

p.start()
p.join()

print("======================")
```

```python
代码举例3：
"""
process 示例  创建多个子进程
"""

from multiprocessing import Process
from time import sleep
import os

def th1():
    sleep(3)
    print("吃饭")
    print(os.getppid(),'--',os.getpid())

def th2():
    sleep(2)
    print("睡觉")
    print(os.getppid(),'--',os.getpid())

def th3():
    sleep(4)
    print("打豆豆")
    print(os.getppid(),'--',os.getpid())


jobs = []
for th in  [th1,th2,th3]:
    p = Process(target=th)
    jobs.append(p) # 保留每一个进程对象
    p.start()

for i in jobs:
    i.join()

```

> multiprocessing 模块进程创建流程特点：
>
> 【1】 将需要子进程执行的事件封装为函数
> 【2】 通过模块的Process类创建进程对象，关联函数
> 【3】 可以通过进程对象设置进程信息及属性
> 【4】 通过进程对象调用start启动进程
> 【5】 通过进程对象调用join回收进程

#### 进程对象属性

> p.name  进程名称
>
> p.pid   对应子进程的PID号
>
> p.is_alive() 查看子进程是否在生命周期
>
> p.daemon  设置父子进程的退出关系  
>
> >* 如果设置为True则子进程会随父进程的退出而结束
> >* 要求必须在start()前设置
> >* 如果daemon设置成True 通常就不会使用 join()

```python
代码举例：
"""
进程对象属性
"""

from multiprocessing import Process
import time

def fun():
    for i in range(3):
        print(time.ctime())
        time.sleep(2)

# 创建进程对象
p = Process(target=fun,name = "Tarena")

p.daemon = True # 父进程退出时，它创建的这个子进程也退出

p.start()

# p.name = "Tedu"
print("Name:",p.name)
print("is alive:",p.is_alive())
print("PID:",p.pid)
time.sleep(1)
```

#### 自定义进程类

> 1. 创建步骤
>    【1】 继承Process类
>    【2】 重写`__init__`方法添加自己的属性，使用super()加载父类属性
>    【3】 重写run()方法
>
> 2. 使用方法
>    【1】 实例化对象
>    【2】 调用start自动执行run方法
>    【3】 调用join回收进程

```python
代码举例：
"""
自定义进程类
"""

from multiprocessing import Process


# 自己定义一个进程类
class MyProcess(Process):
    def __init__(self,value):
        super().__init__() # 加载父类的init中的属性
        self.value = value

    # 充分发挥才能，实现你的进程事件
    def fun1(self):
        print("步骤一")

    def fun2(self):
        print("步骤二")

    # 功能启动函数
    def run(self):
        self.fun1()
        self.fun2()

p = MyProcess(2) # 定义进程对象
p.start() # 将run作为进程执行
p.join()

```

#### 进程池

> 1. 必要性
>    【1】 进程的创建和销毁过程消耗的资源较多
>    【2】 当任务量众多，每个任务在很短时间内完成时，需要频繁的创建和销毁进程。此时对计算机压力较大
>    【3】 进程池技术很好的解决了以上问题。
>
> 2. 原理
>
>    创建一定数量的进程来处理事件，事件处理完进	程不退出而是继续处理其他事件，直到所有事件全都处理完毕统一销毁。增加进程的重复利用，降低资源消耗。

**进程池实现**

【1】 创建进程池对象，放入适当的进程

```python	  
from multiprocessing import Pool

Pool(processes)
功能： 创建进程池对象
参数： 指定进程数量，默认根据系统自动判定
```

【2】 将事件加入进程池队列执行

```python
pool.apply_async(func,args,kwds)
功能: 使用进程池执行 func事件
参数： func 事件函数
      args 元组  给func按位置传参
      kwds 字典  给func按照键值传参
返回值： 返回函数事件对象
```

【3】 关闭进程池

```python
pool.close()
功能： 关闭进程池
```

【4】 回收进程池中进程

```python
pool.join()
功能： 回收进程池中进程
```

```python
"""
进程池演示
* 父进程结束，进程池也会销毁
*  执行的事件函数必须在进程池创建之前声明
"""

from multiprocessing import Pool
from time import sleep,ctime

# 进程池事件
def worker(msg):
    sleep(2)
    print(ctime(),'--',msg)

# 创建进程池
pool = Pool(4)

# 向进程池放事件
for i in range(10):
    msg = "Tedu%d"%i
    pool.apply_async(func=worker,args=(msg,))

# 关闭进程池  不能再添加新的事件
pool.close()

# 回收
pool.join()

```

## 线程(Thread)理论基础

### 定义

> 1. 什么是线程
>    【1】 线程被称为轻量级的进程
>    【2】 线程也可以使用计算机多核资源，是多任务编程方式
>    【3】 线程是系统分配内核的最小单元
>    【4】 线程可以理解为进程的分支任务
>
> 2. 线程特征
>    【1】 一个进程中可以包含多个线程
>    【2】 线程也是一个运行行为，消耗计算机资源
>    【3】 一个进程中的所有线程共享这个进程的资源
>    【4】 多个线程之间的运行互不影响各自运行
>    【5】 线程的创建和销毁消耗资源远小于进程
>    【6】 各个线程也有自己的ID等特征

### threading模块创建线程

【1】 创建线程对象

```	  python
from threading import Thread 

t = Thread()
功能：创建线程对象
参数：target 绑定线程函数
     args   元组 给线程函数位置传参
     kwargs 字典 给线程函数键值传参
```

【2】 启动线程

```python
 t.start()
```

【3】 回收线程

```python
 t.join([timeout])
```

```python
demo1:
"""
thread1.py  创建线程演示
步骤 ：同Ｐｒｏｃｅｓｓ用法
1. 封装线程函数
2. 创建线程对象
3. 启动线程
4. 回收线程
"""

from threading import Thread
from time import sleep
import os

a = 1

# 线程函数
def music():
    for i in range(3):
        sleep(2)
        print(os.getpid(),"播放：黄河大合唱")
    global a
    print('a = ',a)
    a = 1000

# 创建线程对象
t = Thread(target=music)

t.start() # 启动线程 将music函数作为线程执行内容

for i in range(4):
    sleep(1)
    print(os.getpid(),"播放:葫芦娃")

t.join() # 回收线程

print("a:",a)

```

```python
demo2:
"""
thread2.py  线程函数传参
"""

from threading import Thread
from time import sleep

# 含有参数的线程函数
def fun(sec,name):
    print("含有参数的线程")
    sleep(sec)
    print("%s执行完毕"%name)

# 创建多个线程
jobs = []
for i in range(5):
    t = Thread(target=fun,args=(2,),kwargs={'name':"T%d"%i})
    jobs.append(t) # 存储线程对象
    t.start()

for i in jobs:
    i.join()
```

### 线程对象属性

>t.name 线程名称
>t.setName()  设置线程名称
>t.getName()  获取线程名称

>t.is_alive()  查看线程是否在生命周期

>t.daemon  设置主线程和分支线程的退出关系
>t.setDaemon()  设置daemon属性值
>t.isDaemon()  查看daemon属性值
>
>>daemon为True时主线程退出分支线程也退出。要在start前设置，通常不和join一起使用。

```python
"""
线程属性
"""

from threading import Thread
from time import sleep

def fun():
    sleep(3)
    print("线程属性测试")

t = Thread(target = fun)

# 在start前设置,分支线程随主线程结束而结束
t.setDaemon(True)

t.start()

t.setName("Tedu")
print("Name:",t.getName())

print("is alive:",t.is_alive())
print("daemon:",t.isDaemon())
```

### 自定义线程类

> 1. 创建步骤
>    【1】 继承Thread类
>    【2】 重写`__init__`方法添加自己的属性，使用super()加载父类属性
>    【3】 重写run()方法
>
> 2. 使用方法
>    【1】 实例化对象
>    【2】 调用start自动执行run方法
>    【3】 调用join回收线程

```python
"""
自定义线程类
"""

from threading import Thread
import time

class MyThread(Thread):
    def __init__(self,song,sec):
        super().__init__()
        self.song = song
        self.sec = sec

    def run(self):
        for i in range(3):
            print("Playing %s : %s"%(self.song,time.ctime()))
            time.sleep(self.sec)

t = MyThread('凉凉',2)
t.start()
t.join()
```

### 同步互斥

#### 线程间通信方法

1. 通信方法

>线程间使用全局变量进行通信


2. 共享资源争夺

* 共享资源：多个进程或者线程都可以操作的资源称为共享资源。对共享资源的操作代码段称为临界区。

* 影响 ： 对共享资源的无序操作可能会带来数据的混乱，或者操作错误。此时往往需要同步互斥机制协调操作顺序。

3. 同步互斥机制

>同步 ： 同步是一种协作关系，为完成操作，多进程或者线程间形成一种协调，按照必要的步骤有序执行操作。

![7_同步](F:\老安课程串讲资料\老安精品——全课程&全技术方向资料笔记汇总\老安资料2020新版(Version2.0)\(10)Spider\IO并发编程\img\7_同步.png)

> 互斥 ： 互斥是一种制约关系，当一个进程或者线程占有资源时会进行加锁处理，此时其他进程线程就无法操作该资源，直到解锁后才能操作。

![7_互斥](F:\老安课程串讲资料\老安精品——全课程&全技术方向资料笔记汇总\老安资料2020新版(Version2.0)\(10)Spider\IO并发编程\img\7_互斥.png)

#### 线程同步互斥方法

- 线程Event

```python
from threading import Event

e = Event()  创建线程event对象

e.wait([timeout])  阻塞等待e被set

e.set()  设置e，使wait结束阻塞

e.clear() 使e回到未被设置状态

e.is_set()  查看当前e是否被设置
```

```python
"""
event 线程同步互斥方法示例
"""

from threading import Event,Thread

s = None # 在线程之间进行通信
e = Event() # 创建event对象

#　线程函数
def yzr():
    print("杨子荣前来拜山头")
    global s
    s = "天王盖地虎"
    e.set()  # 解除主线程阻塞

t = Thread(target=yzr)
t.start()

# 主线程验证信息
print("说对口令就是自己人")
e.wait() # 在主线程使用之前先阻塞
if s == '天王盖地虎':
    print("宝塔镇河妖")
    print("确认过眼神，你是对的人")
else:
    print("打死他，无情啊")

t.join()

```

- 线程锁

```python
from  threading import Lock

lock = Lock()  创建锁对象
lock.acquire() 上锁  如果lock已经上锁再调用会阻塞
lock.release() 解锁

with  lock:  上锁
...
...
	 with代码块结束自动解锁
```

```python
"""
thread_lock.py lock方法解决同步互斥
"""

from threading import Thread,Lock

a = b = 0
lock = Lock() # 创建锁对象

# 线程函数
def value():
    while True:
        lock.acquire()
        if a != b:
            print("a = %d,b = %d"%(a,b))
        lock.release()

t = Thread(target=value)
t.start()

while True:
    lock.acquire() # 上锁
    a += 1
    b += 1
    lock.release() # 解锁

    # with lock:  #上锁
    #     a += 1
    #     b += 1
                # 语句块结束解锁

t.join()
```

#### 死锁及其处理

1. 定义

>死锁是指两个或两个以上的线程在执行过程中，由于竞争资源或者由于彼此通信而造成的一种阻塞的现象，若无外力作用，它们都将无法推进下去。此时称系统处于死锁状态或系统产生了死锁。

![死锁](F:\老安课程串讲资料\老安精品——全课程&全技术方向资料笔记汇总\老安资料2020新版(Version2.0)\(10)Spider\IO并发编程\img\死锁.jpg)

2. 死锁产生条件

***代码示例: day8/dead_lock.py***

>死锁发生的必要条件
>
>>* 互斥条件：指线程对所分配到的资源进行排它性使用，即在一段时间内某资源只由一个进程占用。如果此时还有其它进程请求资源，则请求者只能等待，直至占有资源的进程用毕释放。
>>* 请求和保持条件：指线程已经保持至少一个资源，但又提出了新的资源请求，而该资源已被其它进程占有，此时请求线程阻塞，但又对自己已获得的其它资源保持不放。
>>* 不剥夺条件：指线程已获得的资源，在未使用完之前，不能被剥夺，只能在使用完时由自己释放,通常CPU内存资源是可以被系统强行调配剥夺的。
>>* 环路等待条件：指在发生死锁时，必然存在一个线程——资源的环形链，即进程集合{T0，T1，T2，···，Tn}中的T0正在等待一个T1占用的资源；T1正在等待T2占用的资源，……，Tn正在等待已被T0占用的资源。

>死锁的产生原因
>
>>简单来说造成死锁的原因可以概括成三句话：
>>
>>* 当前线程拥有其他线程需要的资源
>>* 当前线程等待其他线程已拥有的资源
>>* 都不放弃自己拥有的资源


3. 如何避免死锁

死锁是我们非常不愿意看到的一种现象，我们要尽可能避免死锁的情况发生。通过设置某些限制条件，去破坏产生死锁的四个必要条件中的一个或者几个，来预防发生死锁。预防死锁是一种较易实现的方法。但是由于所施加的限制条件往往太严格，可能会导致系统资源利用率。

```python
"""
模仿死锁现象
"""
from threading import Lock,Thread
from time import sleep

# 账户
class Account:
    def __init__(self,id,balance,lock):
        self.id = id
        self.balance = balance # 存款
        self.lock = lock

# 初始化2个账户
Tom = Account('1',5000,Lock())
Abby = Account('2',4000,Lock())

# 转账
def transfer(f,t,amount):
    """
    :param f:  转出
    :param t:  转入
    :param amount: 金额
    """
    f.lock.acquire() # 自己的锁住
    f.balance -= amount
    f.lock.release()  # 账户解锁   不会产生死锁

    sleep(0.1)
    t.lock.acquire() # 对方的账户锁住
    t.balance += amount

    # f.lock.release() # 账户解锁 会产生死锁
    t.lock.release()

t1 = Thread(target=transfer,args=(Tom,Abby,1500))
t2 = Thread(target=transfer,args=(Abby,Tom,500))
t1.start()
t2.start()
t1.join()
t2.join()

print("Tom:",Tom.balance)
print("Abby:",Abby.balance)
```

### Python线程GIL

- python线程的GIL问题 （全局解释器锁）

>什么是GIL ：由于python解释器设计中加入了解释器锁，导致python解释器同一时刻只能解释执行一个线程，大大降低了线程的执行效率。

>导致后果： 因为遇到阻塞时线程会主动让出解释器，去解释其他线程。所以python多线程在执行多阻塞高延迟IO时可以提升程序效率，其他情况并不能对效率有所提升。

>GIL问题建议
>
>* 尽量使用进程完成无阻塞的并发行为
>* 不使用c作为解释器 （Java  C#）

- 结论 ： 在无阻塞状态下，多线程程序和单线程程序执行效率几乎差不多，甚至还不如单线程效率。但是多进程运行相同内容却可以有明显的效率提升。

### 进程线程的区别联系

#### 区别联系

> 1. 两者都是多任务编程方式，都能使用计算机多核资源
> 2. 进程的创建删除消耗的计算机资源比线程多
> 3. 进程空间独立，数据互不干扰，有专门通信方法；线程使用全局变量通信
> 4. 一个进程可以有多个分支线程，两者有包含关系
> 5. 多个线程共享进程资源，在共享资源操作时往往需要同步互斥处理
> 6. 进程线程在系统中都有自己的特有属性标志，如ID,代码段，命令集等。

#### 使用场景

> 1. 任务场景：如果是相对独立的任务模块，可能使用多进程，如果是多个分支共同形成一个整体任务可能用多线程
>
> 2. 项目结构：多种编程语言实现不同任务模块，可能是多进程，或者前后端分离应该各自为一个进程。
>
> 3. 难易程度：通信难度，数据处理的复杂度来判断用进程间通信还是同步互斥方法。

#### 要求

> 1. 对进程线程怎么理解/说说进程线程的差异
> 2. 进程间通信知道哪些，有什么特点
> 3. 什么是同步互斥，你什么情况下使用，怎么用
> 4. 给一个情形，说说用进程还是线程，为什么
> 5. 问一些概念，僵尸进程的处理，GIL问题，进程状态

## 多进程多线程爬虫思路总结

### 多线程爬虫思路梳理

> 1.创建线程队列，将待爬取的URL放入队列中
>
> 2.多个线程从队列中读取URL地址，进行数据抓取
>
> ​	注意：读取URL地址的过程中注意阻塞问题。
>
> ​	原因：一般实现思路是：
>
> ​		1.创建空队列
>
> ​		2.功能方法生成目标URL -- 入队列
>
> ​		3.线程读取URL队列 -- 如果为空 -- 阻塞等待
>
> ​									  -- 如果不为空 -- 非阻塞 -- 读取 -- 执行
>
> ​	如果URL队列为空（即还没有生成的URL入队列），线程从中取不到URL，所以会保持阻塞状态，直至功能函数创建完最终URL并入队列，队列此时不为空，线程从中可以读取到URL地址，则转为非阻塞状态，读取，执行。
>
> ​	而入队列我们采用的是put()方法，线程从队列中读取URL采用get()方法，get读取到一个URL后转入非阻塞状态执行线程，同时会从队列中删除读取到的URL，如果此时队列只有这一个URL，则另一线程需继续保持阻塞状态等待下一条URL入队列。
>
> 3.因为多线程间通信采用共享全局变量，所以为避免互斥，需要将线程加锁。一般在爬虫程序中需要在写入数据的时候进行加锁，避免因互斥造成数据出错。

### 多线程爬虫编码步骤

> 1.__init__()方法中创建队列，需要几个创建几个
>
> 2.__init__()方法中定义线程锁
>
> 3.爬虫类的写入数据方法中，在写入数据步骤前，加锁，写入完毕后，解锁
>
> 4.定义所需的线程事件函数
>
> 5.主函数中创建多线程，传入线程事件函数，执行。

### 案例：采用多线程技术爬取小米应用商店数据

```python
# -*- coding:utf-8 _*-
"""
@version:
author:安伟超
@time: 2020/09/18
@file: demo16_XiaoMiappsSpider_OOP.py.py
@environment:virtualenv
@email:awc19930818@outlook.com
@github:https://github.com/La0bALanG
@requirement:抓取小米应用商店所有应用信息，采用多线程爬取
"""


"""

思路梳理
1.目标:
    百度搜索：小米应用商店 -- 进入官网
    将所有分类下的所有应用的名称及下载链接抓取下来
    
2.思路
    1.分析页面及URL
        1.确认无法直接从页面中获取数据 -- 动态加载
        2.控制台抓包 -- XHR -- response -- 数据存在
        3.确认请求的XHR接口URL:http://app.mi.com/categotyAllListApi?page=0&categoryId=2&pageSize=30
        4.查看并分析查询参数：
            page: 0
            categoryId: 2
            pageSize: 30
        
        多次进入下一页观察查询参数，发现在同一分类下，categoryId及pageSize的参数值为定值，page跟随页数变化
        
        所以可以通过构造page参数实现多页爬取
    
    2.代码实现思路
        1.构造多页请求URL
        2.发请求，请求XHR接口URL，获取response的json数据
        3.解析，写入csv文件
    
    3.多线程思路：
        1、在 __init__(self) 中创建文件对象，多线程操作此对象进行文件写入
            self.f = open('xiaomi.csv','a',newline='')
            self.writer = csv.writer(self.f)
            self.lock = Lock()
        2、每个线程抓取1页数据后将数据进行文件写入，写入文件时需要加锁
            def parse_html(self):
            app_list = []
            for xxx in xxx:
            app_list.append([name,link,typ])
            self.lock.acquire()
            self.wirter.writerows(app_list)
            self.lock.release()
        3、所有数据抓取完成关闭文件
            def main(self):
            self.f.close()

"""


import requests
import time
import csv
import random
import re
from fake_useragent import UserAgent
from lxml import etree
from threading import Lock
from threading import Thread
from queue import Queue



class XiaoMiAppSpider(object):
    '''
    多线程爬取小米应用商店案例
    :return:csv文件


    面向对象思路：
        1.拆分功能细节。整体程序可拆分为:
            1.发请求获得页面
            2.解析页面
            3.持久化存储(写入文件保存)
        2.结合开闭原则，封装功能方法为私有方法，对外提供统一公共接口
        3.采用单例模式：假设本爬虫程序在多个时间、不同情况下多次使用，单例模式实现只创建一个对象，提升性能避免内存占用过高。


    '''

    def __init__(self):
        self.__url = 'http://app.mi.com/categotyAllListApi?page={}&categoryId={}&pageSize=30'
        self.__headers = {
            'User-Agent':UserAgent().random
        }

        #存放所有url的队列
        self.__q = Queue()
        self.__i = 0

        #存放所有id类型的空列表
        self.__id_lists = []

        #打开文件
        self.__f = open('xiaomi.csv','a')
        self.__writer = csv.writer(self.__f)

        #创建锁
        self.__lock = Lock()

    def __get_html(self,url):
        return requests.get(url=url,headers=self.__headers)

    #请求官网获取分类id
    def __get_cate_id(self):
        url = 'http://app.mi.com/'
        html = self.__get_html(url).text
        r_list = re.findall('<a href="/category/(.*?)">(.*?)</a>',html)
        for r in r_list:
            #调用url入队列方法，得到的r为id，拼接为完整URL后入队列
            self.__url_in(r)

    #获取页数：通过获取接口的response的json数据中的counts获取页数
    def __get_pages(self,type_id):
        url = self.__url.format(0,type_id)
        count = self.__get_html(url).json()['count']
        return int(count) // 30 + 1

    #根据获取的页数及类型id拼接最终URL并加入URL队列
    def __url_in(self,r):
        pages = self.__get_pages(r[0])
        for page in range(1,pages):
            url = self.__url.format(page,r[0])
            self.__q.put(url)

    def __parse_html(self,html):

        #存放一页的数据 -- 写入csv文件
        app_list = []
        for app in html['data']:
            # 应用名称 + 链接 + 分类
            name = app['displayName']
            link = 'http://app.mi.com/details?id=' + app['packageName']
            typ_name = app['level1CategoryName']
            app_list.append([name,typ_name,link])
            self.__i += 1
        self.__save_csv(app_list)

    #写入csv文件 注意：写入前加锁，写入完毕解锁
    def __save_csv(self,app_list):

        #加锁
        self.__lock.acquire()

        self.__writer.writerows(app_list)

        #解锁
        self.__lock.release()


    #线程事件函数：get() -- 请求 -- 解析 --  保存数据
    def __get_data(self):
        while True:
            #判断队列是否为空
            if not self.__q.empty():
                url = self.__q.get()
                html = self.__get_html(url).json()

                #调用解析数据方法
                self.__parse_html(html)
                pass
            else:
                break

    #线程主函数
    def __main(self):

        #URL入队列
        self.__get_cate_id()

        #创建多线程
        t_list = []

        for i in range(4):
            t = Thread(target=self.__get_data)
            t_list.append(t)
            t.start()

        #回收线程
        for t in t_list:
            t.join()

        #关闭文件
        self.__f.close()
        print('数量:%d'%self.__i)

    #公共接口
    def display(self):
        self.__main()

def test():
    start = time.time()
    XiaoMiAppSpider().display()
    end = time.time()

    print('执行时间：%.2f'%(end - start))

if __name__ == '__main__':
    test()
```

### 案例：多线程爬虫爬取腾讯招聘职位信息并写入excel文件

```python
# -*- coding:utf-8 _*-
"""
@version:
author:安伟超
@time: 2020/09/19
@file: demo17_TencentJobSpider_OOP.py.py
@environment:virtualenv
@email:awc19930818@outlook.com
@github:https://github.com/La0bALanG
@requirement:多线程抓取腾讯招聘岗位信息存入excel表格
"""

import requests
import time
import json
import random
from openpyxl import Workbook
from fake_useragent import UserAgent
from queue import Queue
from threading import Thread,Lock
from urllib import parse

"""

思路

目标：百度搜索腾讯招聘 - 查看工作岗位，获取：职位名称、工作职责、岗位要求

1.页面及URL分析：
    1.F12控制台查看网页，发现为动态加载数据
    2.F12控制台对XHR抓包，得一级页面json数据地址URL：
        'https://careers.tencent.com/tencentcareer/api/post/Query?timestamp={}&countryId=&cityId=&bgIds=&productId=&categoryId=&parentCategoryId=&attrId=&keyword={}&pageIndex={}&pageSize=10&language=zh-cn&area=cn'Id=&keyword=&pageIndex={}&pageSize=10&language=zh-cn&area=cn
    3.二级页面json数据地址URL:
        'https://careers.tencent.com/tencentcareer/api/post/ByPostId?timestamp={}&postId={}&language=zh-cn'{}&language=zh-cn

2.整体思路
    1.请求接口获取json数据
    2.解析数据拼接URL存入队列
        1.一级页面URL入first队列，对应线程事件处理函数1
        2.二级页面URL入second队列，对应线程事件处理函数2
    3.多个线程从URL队列中读取并请求最终数据
    4.多线程写入excel文件，注意加锁
"""

class SpiderThread(Thread):

    def __init__(self,target=None):
        super().__init__()
        self.target = target

    def run(self):
        self.target()

class TencentJobSpider(object):

    '''



    '''

    def __init__(self):

        #定义一二级页面初始URL
        self.__first_url = 'https://careers.tencent.com/tencentcareer/api/post/Query?timestamp={}&countryId=&cityId=&bgIds=&productId=&categoryId=&parentCategoryId=&attrId=&keyword={}&pageIndex={}&pageSize=10&language=zh-cn&area=cn'
        self.__second_url = 'https://careers.tencent.com/tencentcareer/api/post/ByPostId?timestamp={}&postId={}&language=zh-cn'

        #定义headers
        self.__headers = {
            'User-Agent':UserAgent().random
        }
        #定义一级二级页面对应的URL队列
        self.__first_q = Queue()
        self.__second_q = Queue()

        #创建excel写入实例，并新建sheet
        self.__wb = Workbook()
        self.__ws = self.__wb.create_sheet('job_info')

        #创建锁
        self.__lock = Lock()

        #计数变量
        self.__i = 0

    def __get_html(self,url,headers):
        return requests.get(url=url,headers=headers)

    def __parse_first_page(self):
        '''
        解析一级页面
        目的：拿postid参数拼接二级页面URL
        对应线程事件处理函数1

        :return: 二级页面URL
        '''
        while True:
            if not self.__first_q.empty():
                url = self.__first_q.get()
                html = json.loads(self.__get_html(url,self.__headers).text)
                lts = str(int(time.time()) * 1000)
                for job in html['Data']['Posts']:
                    post_id = job['PostId']
                    s_url = self.__second_url.format(lts,post_id)
                    self.__second_q.put(s_url)
            else:
                break

    def __parse_second_page(self):
        '''
        解析二级页面
        目的：拿最终数据,写入文件
        :return: None
        '''
        while True:
            try:
                url = self.__second_q.get()
                html = json.loads(self.__get_html(url,self.__headers).text)
                # print(html)

                lists = []

                lists.append(html['Data']['RecruitPostName'])
                lists.append(html['Data']['Responsibility'])
                lists.append(html['Data']['Requirement'])

                print('抓取一条信息：%s,开始写入excel...'%lists)

                self.__lock.acquire()
                self.__ws.append(lists)
                self.__i += 1
                print('写入完毕，抓取下一条')
                self.__lock.release()

            except Exception as e:
                break

    def __url_in(self):
        keyword = input('请输入职位关键字：')
        keyword = parse.quote(keyword)
        lts = str(int(time.time()) * 1000)
        total = self.__get_total(keyword)
        print('一共检索到%d页招聘信息;'%total)
        for page in range(1,total+1):
            f_url = self.__first_url.format(lts, keyword, page)
            self.__first_q.put(f_url)

    def __get_total(self,keyword):
        url = self.__first_url.format(str(int(time.time()) * 1000),keyword,1)
        num = int(self.__get_html(url,self.__headers).json()['Data']['Count'])
        if num % 10 == 0:
            total = num // 10
        else:
            total = num // 10 + 1
        return total

    def __event_first(self):
        self.__parse_first_page()

    def __event_second(self):
        self.__parse_second_page()

    def display(self):
        self.__url_in()
        begin = time.time()
        print('即将开始多线程爬取...')
        t1_list = []
        t2_list = []
        for i in range(5):
            t = SpiderThread(target=self.__event_first)
            t1_list.append(t)
            t.start()
            print('一级页面线程T%d开始执行'%i)

        for j in range(5):
            t = SpiderThread(target=self.__event_second)
            t2_list.append(t)
            t.start()
            print('二级页面线程T%d开始执行'%j)

        for t in t1_list:
            t.join()

        for t in t2_list:
            t.join()

        print('爬取总数：%d'%self.__i)
        print('爬取完毕，保存excel表格...')
        end = time.time()
        self.__wb.save('TencentGetJob.xlsx')
        print('保存成功！')
        print('共计用时：%.2f'%(end - begin))



def test():
    TencentJobSpider().display()

if __name__ == '__main__':
    test()
```



# cookie模拟登录

> 会话（Session）跟踪是Web程序中常用的技术，用来**跟踪用户的整个会话**。常用的会话跟踪技术是Cookie与Session。**Cookie通过在客户端记录信息确定用户身份**，**Session通过在服务器端记录信息确定用户身份**。

## cookie及session介绍

### cookie机制

> 在程序中，会话跟踪是很重要的事情。理论上，**一个用户的所有请求操作都应该属于同一个会话**，而另一个用户的所有请求操作则应该属于另一个会话，二者不能混淆。例如，用户A在超市购买的任何商品都应该放在A的购物车内，不论是用户A什么时间购买的，这都是属于同一个会话的，不能放入用户B或用户C的购物车内，这不属于同一个会话。
>
> 而Web应用程序是使用HTTP协议传输数据的。**HTTP协议是无状态的协议。一旦数据交换完毕，客户端与服务器端的连接就会关闭，再次交换数据需要建立新的连接。这就意味着服务器无法从连接上跟踪会话**。即用户A购买了一件商品放入购物车内，当再次购买商品时服务器已经无法判断该购买行为是属于用户A的会话还是用户B的会话了。要跟踪该会话，必须引入一种机制。
>
> Cookie就是这样的一种机制。它可以弥补HTTP协议无状态的不足。在Session出现之前，基本上所有的网站都采用Cookie来跟踪会话。
>
> Cookie意为“甜饼”，是**由W3C组织提出**，最早由Netscape社区发展的一种机制。目前Cookie已经成为标准，所有的主流浏览器如IE、Netscape、Firefox、Opera等都支持Cookie。
>
> 由于HTTP是一种无状态的协议，服务器单从网络连接上无从知道客户身份。怎么办呢？就**给客户端们颁发一个通行证吧，每人一个，无论谁访问都必须携带自己通行证。这样服务器就能从通行证上确认客户身份了。这就是Cookie的工作原理**。
>
> Cookie实际上是一小段的文本信息。客户端请求服务器，如果服务器需要记录该用户状态，就使用response向客 户端浏览器颁发一个Cookie。客户端浏览器会把Cookie保存起来。当浏览器再请求该网站时，浏览器把请求的网址连同该Cookie一同提交给服务 器。服务器检查该Cookie，以此来辨认用户状态。服务器还可以根据需要修改Cookie的内容。

### session机制

> 除了使用Cookie，Web应用程序中还经常使用Session来记录客户端状态。**Session是服务器端使用的一种记录客户端状态的机制**，使用上比Cookie简单一些，相应的也**增加了服务器的存储压力**。
>
> Session是另一种记录客户状态的机制，不同的是Cookie保存在客户端浏览器中，而Session保存在服务器上。客户端浏览器访问服务器的时候，服务器把客户端信息以某种形式记录在服务器上。这就是Session。客户端浏览器再次访问时只需要从该Session中查找该客户的状态就可以了。
>
> 如果说**Cookie机制是通过检查客户身上的“通行证”来确定客户身份的话，那么Session机制就是通过检查服务器上的“客户明细表”来确认客户身份。Session相当于程序在服务器上建立的一份客户档案，客户来访的时候只需要查询客户档案表就可以了。**

## cookie模拟登录适用场景

> 需要登录验证才能访问的页面

## cookie模拟登录实现的三种方法

```python
# 方法1（利用cookie）
	1、先登录成功1次,获取到携带登陆信息的Cookie（处理headers）
	2、利用处理的headers向URL地址发请求
# 方法2(利用requests.get()中cookies参数)
	1、先登录成功1次,获取到cookie,处理为字典
	2、res=requests.get(xxx,cookies=cookies)
# 方法3（利用session会话保持）
	1、实例化session对象
		session = requests.session()
	2、先post : session.post(post_url,data=post_data,headers=headers)
		1、登陆，找到POST地址: form -> action对应地址
		2、定义字典，创建session实例发送请求
		# 字典key ：<input>标签中name的值(email,password)
		# post_data = {'email':'','password':''}
	3、再get : session.get(url,headers=headers)
        
```

# 案例：人人网携带cookie登录(手动抓取)

```python
# -*- coding:utf-8 _*-
"""
@version:
author:安伟超
@time: 2020/09/24
@file: demo18_RenRenLoginSpider_OOP.py.py
@environment:virtualenv
@email:awc19930818@outlook.com
@github:https://github.com/La0bALanG
@requirement:携带cookie登录人人网
"""

import requests
from lxml import etree
from fake_useragent import UserAgent

class RenRenLoginSpider(object):

    '''

    手动登录一次，抓取cookie
    '''

    def __init__(self):
        self.__url = 'http://www.renren.com/975166356/profile'
        self.__headers = {
            'Cookie':'anonymid=kfg4huvsr796dp; depovince=HUN; _r01_=1; JSESSIONID=abcNnIvtJtKrVceQgR9sx; taihe_bi_sdk_uid=2f95a9b367d045acaa5d01f948247f9d; taihe_bi_sdk_session=29ce3835eb24b637346bd140788b3ddf; ick_login=ce3dc1a9-c5ff-4d78-8f9c-fa8d6f878398; t=aedde2d5487361da45e67c6ab2e1ec6d6; societyguester=aedde2d5487361da45e67c6ab2e1ec6d6; id=975166356; xnsid=4250f34e; jebecookies=7cd2ddc3-2852-498d-913e-0127491d7d3b|||||; ver=7.0; loginfrom=null; wp_fold=0',
            'User-Agent':UserAgent().random
        }

    def __get_html(self,url,headers):
        return requests.get(url=url,headers=headers).text

    def __parse_html(self,html):
        dom = etree.HTML(html)
        return dom.xpath('//div[@class="operate_area"]/div[1]/ul/li[1]/span/text()')

    def display(self):
        res = self.__parse_html(self.__get_html(self.__url,self.__headers))
        print(res)

def test():
    RenRenLoginSpider().display()

if __name__ == '__main__':
    test()
```

# 案例：人人网携带cookie登录(抓取cookie处理字典)

```python
# -*- coding:utf-8 _*-
"""
@version:
author:安伟超
@time: 2020/09/24
@file: demo18_RenRenLoginSpider_dicts_OOP.py.py
@environment:virtualenv
@email:awc19930818@outlook.com
@github:https://github.com/La0bALanG
@requirement:携带cookie登录，cookie处理为字典
"""

import requests
from lxml import etree
from fake_useragent import UserAgent



class RenRenLoginSpider(object):

    '''

    抓取cookie，处理为字典
    '''

    def __init__(self):
        self.__url = 'http://www.renren.com/975166356/profile'
        self.__headers = {
            'User-Agent': UserAgent().random
        }

    def __get_cookie_dicts(self):

        cookie_dict = {}
        cookies = 'anonymid=kfg4huvsr796dp; depovince=HUN; _r01_=1; JSESSIONID=abcNnIvtJtKrVceQgR9sx; taihe_bi_sdk_uid=2f95a9b367d045acaa5d01f948247f9d; taihe_bi_sdk_session=29ce3835eb24b637346bd140788b3ddf; ick_login=ce3dc1a9-c5ff-4d78-8f9c-fa8d6f878398; t=aedde2d5487361da45e67c6ab2e1ec6d6; societyguester=aedde2d5487361da45e67c6ab2e1ec6d6; id=975166356; xnsid=4250f34e; jebecookies=7cd2ddc3-2852-498d-913e-0127491d7d3b|||||; ver=7.0; loginfrom=null; wp_fold=0'
        for k in cookies.split('; '):
            key = k.split('=')[0]
            
            value = k.split('=')[1]
            
            cookie_dict[key] = value
        
        return cookies
    
    def __get_html(self):
        cookies = self.__get_cookie_dicts()
        return requests.get(url=self.__url,headers=self.__headers,cookies=cookies).text
    
    def __parse_html(self,html):
        dom = etree.HTML(html)
        return dom.xpath('//div[@class="operate_area"]/div[1]/ul/li[1]/span/text()')

    def display(self):
        res = self.__parse_html(self.__get_html())
        print(res)
        
def test():
    RenRenLoginSpider().display()

if __name__ == '__main__':
    test()

```

# 案例：人人网携带cookie登录(requests处理cookie)

```python
# -*- coding:utf-8 _*-
"""
@version:
author:安伟超
@time: 2020/09/24
@file: demo18_RenRenLogin_requests_cookie_OOP.py.py
@environment:virtualenv
@email:awc19930818@outlook.com
@github:https://github.com/La0bALanG
@requirement:使用requests模块处理
"""

import requests
from lxml import etree
from fake_useragent import UserAgent


class RenRenLoginRequestsSpider(object):
    '''
    原理思路及实现
    # 1. 思路
    requests模块提供了session类,来实现客户端和服务端的会话保持
    # 2. 原理
    1、实例化session对象
    session = requests.session()
    2、让session对象发送get或者post请求
    res = session.post(url=url,data=data,headers=headers)
    res = session.get(url=url,headers=headers)
    # 3. 思路梳理
    浏览器原理: 访问需要登录的页面会带着之前登录过的cookie
    程序原理: 同样带着之前登录的cookie去访问 - 由session对象完成
    1、实例化session对象
    2、登录网站: session对象发送请求,登录对应网站,把cookie保存在session对象中
    3、访问页面: session对象请求需要登录才能访问的页面,session能够自动携带之前的这个cookie,进行请求


    具体步骤

    1、寻找Form表单提交地址 - 寻找登录时POST的地址
    查看网页源码,查看form表单,找action对应的地址: http://www.renren.com/PLogin.do
    2、发送用户名和密码信息到POST的地址
    * 用户名和密码信息以什么方式发送？ -- 字典
    键 ：<input>标签中name的值(email,password)
    值 ：真实的用户名和密码
    post_data = {'email':'','password':''}
    session = requests.session()
    session.post(url=url,data=data)

    '''

    def __init__(self):
        self.__post_url = 'http://www.renren.com/PLogin.do'
        self.__get_url = 'http://www.renren.com/967469305/profile'
        self.__headers = {
            'User-Agent':UserAgent().random
        }
        self.__session = requests.session()
        
        
    def __get_html(self):
        form_data = {
            'email':'xx',
            'password':'xx'
        }
        
        self.__session.post(url=self.__post_url,headers=self.__headers,data=form_data)
        
        return self.__session.get(url=self.__get_url,headers=self.__headers).text
    

    def __parse_html(self,html):
        dom = etree.HTML(html)
        return dom.xpath('//div[@class="operate_area"]/div[1]/ul/li[1]/span/text()')

    def display(self):
        res = self.__parse_html(self.__get_html())
        print(res)

def test():
    RenRenLoginRequestsSpider().display()

if __name__ == '__main__':
    test()

```

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
>

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

# 案例：破解js加密爬取网易云音乐任意vip付费歌曲

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


# 分布式爬虫框架Scrapy——基础概念及应用

# 分布式爬虫框架Scrapy——进阶高级应用

# Fiddler抓包工具

# 移动端APP的数据抓取