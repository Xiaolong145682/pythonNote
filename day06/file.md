# 文件系统
## 文件
* 文件是计算机中非常重要的东西，在Python里把文件视作一种类型的对象，类似之前学习过的其它类型。文件包括普通的文本，图片，音频，视频等，在linux操作系统中还有“一切皆文件”的说法，也就是说所有的东西都被保存在文件中。所以文件对象不仅可以用来访问普通的磁盘文件, 而且也可以访问任何其它类型抽象层面上的“文件”。
* 在linux下文件共有七种，块设备文件，字符设备文件，目录，普通文件，链接文件，套接字文件和管道文件。
## 文件操作
### 打开关闭文件
#### open()方法打开文件
```python
fd = open(file_name,access_mode,buffering)
功能：打开一个文件，返回一个文件流对象
参数：file_name－－－－－－文件名；
     access_mode－－－－－打开文件的方式，如果不写，默认为＇r＇;
          文件模式                        操作
          r                    以读方式打开 文件必须存在
          w                    以写方式打开
                               文件不存在则创建，存在清空原有内容 
          a                    以追加模式打开 
          r+                   以读写模式打开 文件必须存在
          w+                   以读写模式打开文件
                               不存在则创建，存在清空原有内容
          a+                   以读写模式打开 追加模式
          rb                   以二进制读模式打开 同r
          wb                   以二进制写模式打开 同w
          ab                   以二进制追加模式打开 同a
          rb+                  以二进制读写模式打开 同r+
          wb+                  以二进制读写模式打开 同w+
          ab+                  以二进制读写模式打开 同a+
      buffering－－－－－该参数为：０，表示无缓冲
                                ＞１，表示直接指明缓冲区大小
                                不写或＜０，表示使用系统默认提供的缓冲机制
返回值：成功则返回文件流对象，失败得到IOError                                
```
* 流（stream）:所有的I/O操作仅是简单的从程序移进或者移出，这种字节流就称为流．
* 在sys模块中，系统已经默认打开的三个流：
```python
标准输入————sys.stdin
标准输出————sys.stdout
标准错我————sys.stderr
```
* 缓冲及其作用：系统自动的在内存中为每一个正在使用的文件开辟一个缓冲区，从内存向磁盘输出数据必须先送到内存缓冲区，装满缓冲区在一起送到磁盘中去。从磁盘中读数据，则一次从磁盘文件将一批数据读入到内存缓冲区中，然后再从缓冲区逐个的将数据送到程序的数据区。
#### 关闭文件
* close()方法：
```python
fd = open("file.txt","w+")

fd.close() #关闭了一个流
```
* with ... as ...:
with生成的对象在语句块结束后会自动处理，所以也就不需要close了，但是这个流只能在with语句块内使用。
```python
with open('file','r+') as f:
    f.__doc__
```
### 读取文件
1. read([size]):
```
方法用来直接读取字节到字符串中，最多读取给定数目个字节。如果没有给定size参
数（默认值为-1）或者size值为负，文件将被读取直至末尾。文件过大时候建议在non
-blocking模式下使用
```
2. readline([size]):
```
方法读取打开文件的一行(读取下个行结束符之前的所有字节)。然后整行，包括行
结束符，作为字符串返回。和 read() 相同，它也有一个可选的 size 参数，默认为 
-1，代表读至行结束符。如果提供了该参数，那么在超过size个字节后会返回不完整
的行。
```
3. readlines([size]):
```
方法并不像其它两个输入方法一样返回一个字符串。它会读取所有(剩余的)行然后把
它们作为一个字符串列表返回。它的可选参数sizhint代表返回的最大字节大小。如果
它大于 0，那么返回的所有行应该大约有sizhint字节（可能稍微大于这个数字，因为
需要凑齐缓冲区大小）。
```
### 写入文件
```python
#复制文件
fd1 = open("mytest.html","a+")
fd2 = open("test.html","a+")

l = fd2.readlines()
print l
fd1.writelines(l)

fd1.close()
fd2.close()

```
1.　write():
```
功能与 read() 和 readline() 相反。它把含有文本数据或二进制数据块的
字符串写入到文件中去。
```
2. writelines():
```
和 readlines() 一样，writelines()方法是针对列表的操作，它接受一个字符串列表
作为参数，将它们写入文件。行结束符并不会被自动加入，所以如果需要的话，你必
须在调用writelines()前给每行结尾加上行结束符。
```
### 其他操作
#### 缓冲区刷新
```python
#手动刷新缓冲区
fd.flush()
```
#### 文件位置偏移
* 文件位置：当我们打开一个文件进行操作时系统会自动生成一个记录，记录中描述了我们对文件到一些列操作．其中包括每次操作到的文件位置．
* seek():该方法可以在文件中移动文件指针到不同的位置
```python
fd.seek(offset,[whence])
功能：移动文加位置
参数：offset字节代表相对于莫个位置偏移量．可以是负数表示向前移动
     whence是基准位置，默认值为０，代表从文件开头算起
                            １，代表从当前位置算起，
                            ２，代表从文件末尾算起
                            
```
#### 文件内容迭代
在Python2.2中，我们引进了迭代器和文件迭代，这使得一切变得完全不同，文件对象成为 了它们自己的迭代器，这意味着用户不必调用 read*()方法就可以在for循环中迭代文件的每一行。另外我们也可以使用迭代器的next方法，file.next()可以用来读取文件的下一行。和其它迭代器一样，Python也会在所有行迭代完成后引发StopIteration 异常。
```python
>>>f = open('file')

>>>for line in f:
     print(line)
>>>f.next()
```
### 查看文件信息
```python
>>> import os

>>> file_stat = os.stat('file')

>>> file_stat
>>> os.stat_result(st_mode=33204, st_ino=135235, st_dev=2053, st_nlink=1,
  st_uid=1000, st_gid=1000, st_size=12, st_atime=1464256496, st_mtime=1464256509, st_ctime=1464256509)
```


