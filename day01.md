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
