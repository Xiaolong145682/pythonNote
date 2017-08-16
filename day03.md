## 知识点
* if分支语句的用法
* while循环语句的用法
* for循环语句和range的用法
* break,continue和pass的用法
### Python的缩进风格
* 终止行就是终止语句，也就是说每一行结束表示一个语句的结束，一般不会用分号。虽然我们也可以像c语言一样在语句结束加上分号然后继续下一条语句，但是我们不建议这样。同样如果一条语句在一行没有写完可以用 ‘\’ 符号进行分隔。
* 在Python中所有的复合语句（也就是语句中嵌套语句）都有相同的一般形式，就是首行以冒号结尾，首行的下一行嵌套代码以缩进标识。
* 缩进的结束就是代码快的结束。代码块在其他编程语言（c java 等）中通常用花括号作为区分。但是在Python中省略了这样的标识。在Python中用缩进的级别表示代码块。这是语法的规范，通常不同的代码快缩进为一个‘Tab’ ，而且在Python中缩进的错误为语法错误
* Python语句在默认情况下是顺序执行的。
### if分支语句
* 简单的if语句
```python
    if True/False :
        语句块
    
    if True/False :
        语句块1
    else:
        语句块2
```
* 阶梯形式与嵌套形式
```python
#阶梯
   if True/False :
        语句块1
    elif True/False:
        语句块2
    elif True/False:
        语句块3
        ...
        ...
    else:
        语句块n
＃嵌套
    if True/False:
        if True/False:
            语句
        else：
            语句
    else：
        if True/False:
            语句
        else：
            语句
```
* 类似余三目运算符
```python
#如果y是真，返回x，否则返回z
x if y else z 
```
### while循环语句
```python
#条件为假时跳出循环
    while True/False:
        语句块
＃while ... else ... 形式
    while True/False:
        语句块
    else:
        语句块
```
### for循环和range的用法
* for循环
```python
    for 变量 in  列表：
        语句块
#加上else的形式
    for 变量 in  列表：
        语句块
    else：
        语句块
```
* range()生成列表
```python
>>> range(1,5) #代表从1到5(不包含5)
[1, 2, 3, 4]
>>> range(1,5,2) #代表从1到5，间隔2(不包含5)
[1, 3]
>>> range(5) #代表从0到5(不包含5)
[0, 1, 2, 3, 4]
```
* for循环生成列表
```python
>>> [i for i in [1,2,3,4,5]] 
>>> [1,2,3,4,5]
```
### 辅助语句之break,continue,pass,return,zip和map
#### break:用于从循环体内跳出循环体，即提前结束循环
#### continue:结束本次循环,接着判定下一次是否执行循环
#### pass:pass语句在Python中起到了一个占位的作用，当语句块中没有内容的时候语法规则是不允许什么都不写的，这时可以用pass语句占位。
#### return:return语句表示一个函数的结束，如果语句块在一个函数中，那么如果执行到return那么函数将会立即返回，即整个函数直接执行完毕。
#### zip和map
* zip:python2 和　python3 都支持
* map:仅python2支持
* 功能和用法：
```python
>>>L1[1,2,3,4]
>>>L2[10,20,30,40]
>>>list(zip(L1,L2))
[(1,10),(2,20),(3,30),(4,40)]
```
用上述方式将两个列表合成了一个列表，其中每一个元素分别是之前两个列表成对出现的。如果两个列表的长度不一样时使用zip函数会自动以较短的为准，而使用map时则会为较短的序列用None补齐
* zip用法补充：
```python
#以实现for循环的并行遍历
for (x,y) in zip(L1,L2):
    print(x,y,'--',x + y)

    1 10 -- 11
    2 20 -- 22
    3 30 -- 33
    4 40 -- 44
#用zip函数生成字典
>>> keys = ['spam','eggs','toast']
>>> vals = [1,3,5]
>>> list(zip(keys,vals))
 [('spam', 1), ('eggs', 3), ('toast', 5)]
>>> D = {}
>>> for (k,v) in zip(keys,vals): D[k] = v
>>> D
 {'eggs': 3, 'spam': 1, 'toast': 5}

```
