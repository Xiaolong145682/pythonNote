## 多任务编程
* 多任务编程：并行运行这些相互独立的子任务
* 目的：并行处理可以大幅度地提升整个任务的效率
## 进程
计算机程序只不过是磁盘中可执行的，二进制（或其它类型）的数据。它们只有在被读取到内存中，被操作系统调用的时候才开始它们的生命期。``进程``（有时被称为重量级进程）是程序的一次执行。每个进程都有自己的地址空间，内存，数据栈以及其它记录其运行轨迹的辅助数据（在linux系统下记录在PCB当中）。操作系统管理在其上运行的所有进程，并为这些进程公平地分配时间。在进程中存在父子进程的关系。init进程是系统的起始进程。
### 进程和程序的区别
程序是静态的，它是一些保存在磁盘上的指令的有序集合，没有任何执行的概念进程是一个动态的概念，它是程序执行的过程，包括创建，调度和消完进程是程序执行和资源管理的最小单位．
### 进程分类
* 交互进程：该类进程是由shell控制和运行的．交互进程既可以在前台运行，也可以在后台运行.
* 批处理进程：该类进程不属于某个终端，它被提交到一个队列中以便顺序执行．
* 守护进程：该类进程在后台运行，它一般在Linux启动时开始执行，系统关闭时才结束．
### 进程状态
* 运行态：此时进程或者正在运行，或者准备运行。
* 等待态：此时进程在等待一个事件的发生或某种系统资源。分为可中断和不可中断
* 停止态：此时进程被中止。
* 死亡态：这是一个已终止的进程，但还在进程向量数组中占有结构空间。

### 进程状态标识
```python
D:    不可中断的静止
R:    正在执行中
S:    阻塞状态
T:    暂停执行
Z:    不存在
<:    高优先级的进程 
N:    低优先级的进程 
L:    有内存分页分配并锁在内存中
PID:  唯一地标识一个进程
```
### linux下常用进程命令
```python
ps aux 　查看系统中的进程
top     动态显示系统的进程
nice    按用户指定的优先级运行进程
renice  改变正在进行进程的优先级
kill    向进程发出信号
```
### 线程
* 线程（有时被称为轻量级进程）跟进程有些相似，不同的是，所有的线程运行在同一个进程中，共享相同的运行环境。我们可以想像成是在主进程或“主线程”中并行运行的“迷你进程”。
* 由于进程的地址空间是私有的，因此在进程间上下文切换时，系统开销比较大。为了提高系统的性能，许多操作系统规范里引入了轻量级进程的概念，被称为线程。在同一个进程中创建的线程共享该进程的地址空间。在Linux中线程和进程都参与统一的调度。
* 一个进程中的多个线程即共享这个进程的资源，同时又有自己的私有资源：
```
共享进程资源                         私有的资源

可执行的指令                         线程ID (TID)                        
全局数据                             PC(程序计数器)和相关寄存器
进程中打开的文件描述符               堆栈
信号处理函数                         局部变量
当前工作目录                         返回地址
用户ID                               执行状态和属性
用户组ID                             信号掩码和优先级
```
### 创建进程
#### 使用os模块创建进程
* 因为Python的os模块包含普遍的操作系统功能。如果你希望你的程序能够与平台无关的话，这个模块是尤为重要的。因为这个模块生成的一些操作都是和底层系统相关。在这里以linux操作系统为例学习下如何使用OS模块来创建新的进程。
* 在os模块中很多操作都可以产生新的进程:
    * 新建进程用os.fork函数．但它只在POSIX系统上可用，在windows版的python中，os模块没有定义os.fork函数。相反，windows程序员用多线程编程技术来完成并发任务;
    * 用os.system 和 os.exec函数族来执行系统命令和其它程序。os.system使用shell来执行系统命令，然后在命令结束之后把控制权返回给原始进程；os.exec函数族在执行完命令后不将控制权返回给调用进程。它会接管python进程，pid不变。这两个函数支持unix和windows平台;
    * os.popen()函数可执行命令，并获得命令的stdout流。函数要取得两个参数，一个是要执行的命令，另一个是调用函数所用的模式，如“r"只读模式。os.popen2()函数执行命令，并获得命令的stdout流和stdin流
#### subprocess－－－－－－－创建附加进程
#### multiprocessing-----------------更方便的管理进程
* 要创建第二个进程，最简单的方法是用一个目标函数实例化一个Process对象，并调用start()让它工作：
```python
import multiprocessing

def worker():
    '''worker function'''
    print('worker')
    return

if __name__ == '__main__'
    jobs = []
    for i in range(5):
        p = multiprocess.Process(target = worker)
        jobs.append(p)
        p.start()
```
### 僵尸进程
* 孤儿进程：一个父进程退出，而它的一个或多个子进程还在运行，那么那些子进程将成为孤儿进程。孤儿进程将被init进程(进程号为1)所收养，并由init进程对它们完成状态收集工作。
* 僵尸进程：一个进程创建子进程，如果子进程退出，而父进程并没有获取子进程的状态信息，那么子进程的进程描述符仍然保存在系统中。这种进程称之为僵尸进程。僵尸进程会浪费一定的系统资源。
* 如何避免僵尸的产生：
    * 父亲先死，儿子活着，此时儿子寄养在init下，init是它的养父
    * 儿子先死，父亲活着，但是父亲对子进程退出信号做了相应的处理，收尸，就不会产生僵尸进程

#### 处理僵尸进程方法
1. 使用os.wait()或者os.waitpid()函数。 
2. 创建二级子进程然后让一级子进程用sys.exit()推出，让二级子进程成为孤儿。 
3. 使用信号处理的方式或略子进程推出信号
### 守护进程
守护进程，也就是通常所说的Daemon进程，是系统中的后台服务进程。它是一个生存期较长的进程，通常独立于控制终端并且周期性的执行某种任务或等待处理某些发生的事件守护进程常常在系统启动时开始运行，在系统关闭时终止。
守护进程能够突破这种限制，它从开始运行，直到整个系统关闭才会退出。如果想让某个进程不会因为用户或终端的变化而受到影响，就必须把这个进程变成一个守护进程。
#### 实现守护进程
```python

```
