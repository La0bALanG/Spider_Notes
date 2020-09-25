# **<font face="楷体" size=6 color='blue'>Python爬虫笔记1:环境搭建</font>**

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

----


[TOC]



# 爬虫环境搭建

## Anaconda3安装及配置

- **Anaconda3下载**
  
  > 下载地址： [Anaconda3](https://mirrors.tuna.tsinghua.edu.cn/anaconda/archive/).

  Linux版选择：**Anaconda3-5.3.1-Linux-x86_64.sh**
  
- **Anaconda3安装**
  
  终端下运行：
  
```python
  bash Anaconda3-5.3.1-Linux-x86_64.sh
```

  安装过程一路傻瓜式**回车** or **yes**

  *注意*：安装Anaconda3结束前会提示你是否安装**Microsoft Visual studio Code**，此处根据个人喜好选择性安装即可。

- **本地Python环境配置**
  
  安装完成后进行测试，动终端，输入**python3**，回车，查看本机python环境，如下：
  
  
  
  ![在这里插入图片描述](https://img-blog.csdnimg.cn/20200507150149981.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2F3YzE5OTMwODE4,size_16,color_FFFFFF,t_70)
  
  

  显示仍然使用的是Ubuntu自带Python环境，所以需要进行一下手动配置。
  
  启动终端，使用vim编辑器打开根目录下配置文件.bashrc，命令如下：
  
  ```python
  **sudo vim ~/.bashrc**
  ```
  
  ![在这里插入图片描述](https://img-blog.csdnimg.cn/20200507150054835.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2F3YzE5OTMwODE4,size_16,color_FFFFFF,t_70)
  
  在文末添加一行代码如下：
  
  ```python
  **export PATH="==/home/anwc/anaconda3==/bin:$PATH"**（标记部分为你的**本机Anaconda路径**）	
  ```
  
  最后在终端输入：
  
  ```python
  source ~/.bashrc
  ```
  
  运行一下即可。


## Chrome浏览器插件安装及配置

> 注意：Chrome浏览器插件需要**FQ**上Google进行下载安装，自行解决**FQ**后继续：

进入Chrome应用商店，依次搜索`Proxy-Switch0mega`、`JSONView`、`XPath Helper`进行安装，安装后即可在开发者工具里看到这三个插件，如图：

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200507152230549.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2F3YzE5OTMwODE4,size_16,color_FFFFFF,t_70)

下面简单说下**Proxy-Switch0mega的安装及配置**：

1. 点击浏览器右上角插件图标：
   <img src="https://img-blog.csdnimg.cn/20200507152408540.png" alt="在这里插入图片描述" style="zoom: 33%;" />
   点击选项；
2. 进入后看到如下界面：
   ![在这里插入图片描述](https://img-blog.csdnimg.cn/20200507152512775.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2F3YzE5OTMwODE4,size_16,color_FFFFFF,t_70)
3. 选择左下角的新建情景模式，进入后如图：
   ![在这里插入图片描述](https://img-blog.csdnimg.cn/2020050715261614.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2F3YzE5OTMwODE4,size_16,color_FFFFFF,t_70)
4. 情景名称随意，输入后点击创建，如图：
   ![在这里插入图片描述](https://img-blog.csdnimg.cn/20200507152829799.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2F3YzE5OTMwODE4,size_16,color_FFFFFF,t_70)
   至此，基本配置完成。



## Fiddler安装及证书配置

> Linux下不能直接使用fiddler，需要先安装mono-conplete

终端输入命令：

```python
sudo apt-get install mono-complete
```

如下（测试本机已安装，故不运行仅展示）：

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200507154932927.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2F3YzE5OTMwODE4,size_16,color_FFFFFF,t_70)

安装大约需要几分钟；

安装完毕后，点击下方链接下载`fiddler Linux`版，此为zip压缩包；

> **Linux版fiddler下载地址**：链接: [link](https://pan.baidu.com/s/1VGoNvZ8vfecvr77X36StQQ).提取码：ov99

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

> Linux下MySQL5.7诟病百出，已经不建议使用，那么如何在Linux下安装MySQL8.0呢？
>

- **将MySQL APT存储库添加到系统的软件存储库列表中**
  进入[MySQL官网](https://dev.mysql.com/downloads/repo/apt/)查看版本号：
  ![在这里插入图片描述](https://img-blog.csdnimg.cn/20200507162702783.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2F3YzE5OTMwODE4,size_16,color_FFFFFF,t_70)
  图片中红框标识出来的就是最新版本号，复制此版本号；
  
- 使用**wget**进行下载：
  
  ~~~python
  wget https://dev.mysql.com/get/mysql-apt-config_0.8.15-1_all.deb
  ~~~

  将下载好的文件使用**dpkg**命令进行安装：
  
  ~~~python
sudo dpkg -i mysql-apt-config_0.8.15-1_all.deb
  ~~~

  中间弹窗直接点击OK；
  然后更新一下存储库信息：
  
~~~python
  sudo apt-get update
~~~


- **使用APT安装MySQL**
  
  （*注意*：如果不执行以上步骤直接进行APT安装，则安装的是MySQL5.7版本）
命令：
  
  ~~~python
  sudo apt-get install mysql-server
  ~~~
~~~
  
其中两个弹窗:
  
第一个是确认密码（这一步一定要设置数据库密码）
  
另一个是选择加密方式，工具较新选第一个，较老选第二个
  
- **开放远程访问**
  为了方便后期使用可视化图形界面操作数据库，这里需要开放一下远程访问权限。
  1.连接到数据库；

  ~~~python
  mysql -uroot -p
~~~

  输入密码进入；

2.查看数据库中mysql表；

  ~~~python
  show databases;
  ~~~

3.选择当前使用数据库为mysql；

  ~~~python
  use mysql;
  ~~~

4.查看权限：

  ~~~python
  select host, user, authentication_string, plugin from user;
  ~~~

5.更改加密方式（******为你自己设置的密码）：

  ~~~python
  ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY '******';
  ~~~

6.开放远程访问权限（授权远程连接）：

  ~~~python
  ALTER USER 'root'@'%' IDENTIFIED BY '123456' PASSWORD EXPIRE NEVER;
  
  GRANT ALL PRIVILEGES ON *.* TO 'root'@'%' WITH GRANT OPTION;
  
  ALTER USER 'root'@'%' IDENTIFIED WITH mysql_native_password BY '123456';
  ~~~

7.刷新权限：

  ~~~python
  flush privileges;
  ~~~

## MongoDB安装及配置

首先检查一下本机是否安装MongoDB：

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200507165848927.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2F3YzE5OTMwODE4,size_16,color_FFFFFF,t_70)

确认未安装，执行**APT**命令进行安装MongoDB：

~~~python
sudo apt-get install mongodb
~~~

如下图：

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200507170104699.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2F3YzE5OTMwODE4,size_16,color_FFFFFF,t_70)

安装完毕后简单测试一下：

输入命令：

~~~python
mongo
mongod
~~~

出现下图所示：

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200507170247711.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2F3YzE5OTMwODE4,size_16,color_FFFFFF,t_70)

已经能够正常进入MongoDB界面，安装成功。

## Redis安装及配置

使用**APT**命令安装Redis数据库：

~~~python
sudo apt-get install redis-server
~~~

安装完毕后测试：

~~~python
redis-cli
~~~

至此安装成功。
接下来对redis进行基本配置：
进入 /etc/redis 下的redis.conf配置文件：

~~~python
sudo vi /etc/redis/redis.conf
~~~

如下图所示：

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200507171000652.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2F3YzE5OTMwODE4,size_16,color_FFFFFF,t_70)

找到**bind 127.0.0.1**,将其注释掉即可；

继续下拉，找到**requirepass foobared**,如图：

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200507171128647.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2F3YzE5OTMwODE4,size_16,color_FFFFFF,t_70)

这里就是设置redis的连接密码，将其解除注释，并修改**foobared**为任意自己想要设置的密码即可；

修改完毕后，输入：

~~~python
:wq
~~~

保存，关闭窗口，然后输入：

~~~python
sudo service redis restart
~~~

重启一下redis服务即可。

在设置完毕redis连接密码后，如果仍然以无密码状态登录，当你做任何操作时，会提示你没有权限，此时只需要退出redis再重新进入：

~~~python
redis-cli -a yourpassword
~~~

即可恢复正常使用，如下图：

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200507171707858.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2F3YzE5OTMwODE4,size_16,color_FFFFFF,t_70)

# Python爬虫常用库的安装及配置

> Python爬虫常用库有很多，在这里只介绍几个比较常见的库的安装。
>

## pip包管理工具安装

Linux下常用的Python库大部分都是通过pip3包管理工具进行安装的，所以在安装这些库之前，我们先安装pip3：

~~~python
sudo apt-get install python3-pip
~~~

测试本机已安装，故不作图片演示；
安装完毕之后查看下版本号：

~~~python
pip3 --version
~~~

确认为pip3即可：

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200507172130584.png)

爬虫常用库的安装：

~~~python
pip3 install requests selenium beautifulsoup4 pyquery pymongo redis flask django jupyter
~~~

其实诸如redis等我们之前已经安装过了，jupyter也已经在安装Anaconda3的时候自动安装好了。

## 其他常用Python库安装

### **pymysql**

~~~python
pip3 install pymysql
~~~

### **lxml**

~~~python
sudo pip3 install lxml
~~~

### **scrapy**

首先安装依赖，依次执行以下命令安装所需依赖库：

~~~python
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

~~~python
pip3 install Scrapy
~~~

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200508103216573.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2F3YzE5OTMwODE4,size_16,color_FFFFFF,t_70)

验证是否安装成功：终端输入命令：

~~~python
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

- 在线安装
  - 下载插件 - google访问助手
  - 安装插件 - google访问助手: Chrome浏览器-设置-更多工具-扩展程序-开发者模式-拖拽(解压后的插件文件夹)
  - 在线安装其他插件 - 打开google访问助手 - google应用商店 - 搜索插件 - 添加即可

- 离线安装
  - 下载插件 - xxx.crx 重命名为 xxx.zip
  - 输入地址: chrome://extensions/   打开- 开发者模式
  - 拖拽 插件(或者解压后文件夹) 到浏览器中
  - 重启浏览器，使插件生效

## **爬虫常用插件**

- google-access-helper : 谷歌访问助手,可访问 谷歌应用商店
- Xpath Helper: 轻松获取HTML元素的xPath路径
     开启/关闭: Ctrl + Shift + x
- JsonView: 格式化输出json格式数据
- Proxy SwitchyOmega: Chrome浏览器中的代理管理扩展程序