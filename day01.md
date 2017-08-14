## python的安装
### windows下的安装[详情参考百度](https://jingyan.baidu.com/article/7908e85c78c743af491ad261.html)
1. [进入Python官网](https://www.python.org/downloads/)下载安装包，看好自己的机器是64为的还是32位的;
2. 下载好了python安装包后双击python安装包，选择install  just for me，点击下一步;
3. 选择python安装的路径一般都安装在c盘，点击next下一步;
4. 选择python索要安装的文件 默认全部安装，点击next;
5. 稍等一小会儿会就会安装成功;
6. 后点击finsh安装完成;
7. 右键我的电脑 选择属性;
8. 选择高级系统配置，点击高级;
9. 点击环境变量，选择path路径;
10. 然后双击 把刚刚安装python时选择的路径放在path路径里面 注意最后面的分号要填写;
11. 然后在cmd命令行下键入 python -V   就能得到python的版本信息了 安装完成．

### Linux下的安装
1. [进入Python官网](https://www.python.org/downloads/)下载安装包,注意下载后压缩包是以.taz结尾的压缩包
2. 解压压缩包
```
sudo tar -xvf Python-3.6.2.taz
```
3. 进入到解压后的Python-3.6.2目录下，输入ls指令会看到一推的文件和文件夹，别慌，先找到configure,执行它
```
sudo ./configure
```
4. 上面的文件执行完成后会生成一个Makefile文件，有了它以后就可以执行以下操作：
```
//make实际上编译你的源代码，并生成执行文件。
sudo make

sudo make install
```
5. 执行完以上的步骤python就算安装完了，查看版本号若发现还是原来的版本号，别慌，看第六步
6. 首先查看python的安装位置
```
//查看安装位置
which python3 
/usr/local/bin/python3

//进入到该目录下
cd /usr/local/bin

//执行你所安装的python版本
python3.6
```
## python语言的特点及应用
### python的特点
1. 开放性
2. python是一门面向对象的语言，模块，变量，函数都看作是对象．
3. 很好的快平台性，可以很容易的和多种编程语言衔接（比如c c++ java），所以我们也称python位胶水语言
4. 简单好上手，性价比高
### python的应用场合
1. web服务器编程
2. 数据挖掘
3. 自然语言处理
4. 自动化测试（人工智能）
## python变量的特点
### 标识符命名规则
标识符是由程序员按照命名规则自行定义的词法符号，用于定义宏名、变量名、函数名和自定义类型名等。python的命名规则如下：
```
1) 标识符由一个或多个字母、数字或下划线组成
2) 标识符的第一个字符必须是字母或下划线
3) 标识符不能与关键字相同
4) python 语言是严格区分大小写的
```
但是在python的标识符命名中还有一些默认规则
```
1) 以单一下划线开头的变量名（_x）不会被from module import *语句导入
2) 前后双下划线的变量（__x__）为系统的默认变量
3) 前面两个下划线开头的变量（__x）为类的私有变量
```
### 变量的初始化和使用
* 使用前必须赋值（初始化）
* hon属于弱类型变量 ： 对象有类型变量无类型，变量就相当于一个对象的标签
* thon 中变量和常量是分开存放的，当把变量重新赋值的时候即变量存放的地址发生了改变。不用的常量仍然在内存中，有自动的垃圾处理机制，如果没有变量绑定这个常量则自动会被处理也可以通过del来处理，全局变量也随进程消亡

### 运算符及优先级
![](https://nts.newbieol.com/static/k7/Python_2/class-001/img/logical1.png)

### python的关键字
```python
循环判断
if elif else for while break continue

逻辑判断
and or not is in

函数模块类
from import as def pass lambda return calss

异常
try except finally raise

其他
del gloabal with assert yield
True False None nonlocal --->3.x
exec print               --->2.x
```
