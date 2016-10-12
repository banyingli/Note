#Python学习笔记
[Python教程](http://www.liaoxuefeng.com/wiki/001374738125095c955c1e6d8bb493182103fac9270762a000/)
##安装Python
###Python解释器
##第一个Python程序
###使用文本编辑器
###输入和输出  
**输出**：

	>>> print '100 + 200 =', 100 + 200
	100 + 200 = 300  
**输入**：    

	name = raw_input('please enter your name: ')   
	print 'hello,', name
	
##Python基础  
**Python的语法比较简单，采用 *缩进* 方式：**    

	a = 100 
	if a >= 0: 
		print a 
	else: 
		print -a
		
###数据类型和变量  
* ####数据类型

	整数、浮点数、字符串、布尔型（True, False）、空值（None）、列表、字典等，还可以创建自定义数据类型。 
  *注意点*：  
（1）如果字符串内部有很多换行，用\n写在一行里不好阅读，为了简化，Python允许用`'''...'''`的格式表示多行内容:
  
        print '''line1  
        ...line2  
        ...line3'''     
（2）布尔值可以用`and(&&)`、`or(||)`和`not(!)`运算。    
* ####变量 
 变量名必须是大小写英文、数字和_的组合，且不能用数字开头。

###字符串和编码  
Python提供了ord()和chr()函数，可以把字母和ASCII码对应的数字相互转换：      

    >>> ord('A')   
    65   
    >>> chr(65)   
    'A'  
    
Python在后来添加了对Unicode的支持，以Unicode表示的字符串用u'...'表示,比如：  
  
    >>> print u'中文'   
    中文   
	>>> u'中'   
	u'\u4e2d'    

把u'xxx'转换为UTF-8编码的'xxx'用`encode('utf-8')`方法；  
把UTF-8编码表示的字符串'xxx'转换为Unicode字符串u'xxx'用`decode('utf-8')`方法：  

	>>> u'中文'.encode('utf-8')   
	'\xe4\xb8\xad\xe6\x96\x87'    
	>>> print '\xe4\xb8\xad\xe6\x96\x87'.decode('utf-8')
	中文
	
`len()`函数可以**返回字符串的长度**。  
    
	>>> len('ABC') 
	3 
	>>> len(u'中文') 
	2

当Python解释器读取源代码时，为了让它按UTF-8编码读取，我们通常在文件开头写上这两行：  

	#!/usr/bin/env python   
	# -*- coding: utf-8 -*-    

**格式化字符串**：
在Python中，采用的格式化方式和C语言是一致的，用`%`实现:

	>>> 'Hi, %s, you have $%d.' % ('Michael', 1000000) 
	'Hi, Michael, you have $1000000.'

*常见的占位符有：*  
`%d`	整数  
`%f`	浮点数  
`%s`	字符串  
`%x`	十六进制整数    
其中，`%s`永远起作用，它会把任何数据类型转换为字符串。用`%%`来表示一个字符串%。

格式化整数和浮点数还可以指定是否补0和整数与小数的位数：    

	>>> '%2d-%02d' % (3, 1) 
	' 3-01' 
	>>> '%.2f' % 3.1415926 
	'3.14'

###使用list和tuple
* ####list  
list是一种有序的集合，可以随时添加和删除其中的元素。 list里面的元素的数据类型也可以不同，list元素也可以是另一个list。   
（1）用`len()`函数可以获得list元素的个数  
（2）最后一个元素的索引是`len(classmates) - 1`，除了计算索引位置外，还可以用-1做索引（`classmates[-1]`），直接获取最后一个元素，以此类推，可以获取倒数第2个（`classmates[-2]`）、倒数第3个(`classmates[-3]`)...  
（3）追加元素到末尾:`append('Jack')`  
（4）把元素插入到指定的位置:`insert(1, 'Jack')`    
（5）删除list末尾的元素，用`pop()`方法    
（6）要删除指定位置的元素，用`pop(i)`方法，其中i是索引位置  
  
* ####tuple  
tuple和list非常类似，但是tuple一旦初始化就不能修改,当你定义一个tuple时，在定义的时候，tuple的元素就必须被确定下来。如果要定义一个空的tuple，可以写成`()`;定义一个只有1个元素的tuple要写成`(1,)`。

###条件判断和循环  
* ####条件判断    

		age = 3 
		if age >= 18: 
			print 'adult' 
		elif age >= 6: 
			print 'teenager' 
		else: 
			print 'kid'  
  
* ####循环    

#####for...in循环  

		names = ['Michael', 'Bob', 'Tracy'] 
		for name in names: 
			print name  
Python提供一个range()函数，可以生成一个整数序列，比如range(5)生成的序列是从0开始小于5的整数，range(101)就可以生成0-100的整数序列：    

		sum = 0 
		for x in range(101): 
			sum = sum + x 
		print sum    

  
#####while循环  

	sum = 0 
	n = 99 
	while n > 0: 
		sum = sum + n 
		n = n - 2 
	print sum  
  
如果死循环，可以用`Ctrl+C`退出程序。

###使用dict和set
* ####dict  
Python内置了字典：dict的支持，dict全称dictionary，在其他语言中也称为map，使用键-值（key-value）存储，具有极快的查找速度。  
  
		>>> d = {'Michael': 95, 'Bob': 75, 'Tracy': 85} 
		>>> d['Michael'] 
		95  
如果key不存在，dict就会报错，要避免key不存在的错误，有两种办法，一是通过`in`判断key是否存在，二是通过dict提供的`get`方法，如果key不存在，可以返回None，或者自己指定的value：  

		>>> 'Thomas' in d 
		False
		>>> d.get('Thomas') 
		>>> d.get('Thomas', -1) 
		-1  
注意：返回None的时候Python的交互式命令行不显示结果。  
要删除一个key，用pop(key)方法，对应的value也会从dict中删除：  
  
		>>> d.pop('Bob') 
		75  
		
	**和list比较，dict有以下几个特点：**

1. 查找和插入的速度极快，不会随着key的增加而增加；
2. 需要占用大量的内存，内存浪费多。  

	**而list相反：**

1. 查找和插入的时间随着元素的增加而增加；
2. 占用空间小，浪费内存很少。
  
  	所以，dict是用空间来换取时间的一种方法。    
	  
	要保证hash的正确性，`作为key的对象就不能变`。在Python中，字符串、整数等都是不可变的，因此，可以放心地作为key。而list是可变的，就不能作为key。  



* ####set  
set和dict类似，也是一组key的集合，但不存储value。由于key不能重复，所以，在set中，没有重复的key。

	要创建一个set，需要提供一个list作为输入集合，重复元素在set中自动被过滤：   
 
		>>> s = set([1, 1, 2, 2, 3, 3]) 
		>>> s 
		set([1, 2, 3])  
  
	通过`add(key)`方法可以添加元素到set中，通过`remove(key)`方法可以删除元素：  
  
		>>> s.add(4)  
		>>> s.remove(4)  
  
	set可以看成数学意义上的无序和无重复元素的集合，因此，两个set可以做数学意义上的交集、并集等操作：    

		>>> s1 = set([1, 2, 3]) 
		>>> s2 = set([2, 3, 4]) 
		>>> s1 & s2 
		set([2, 3]) 
		>>> s1 | s2 
		set([1, 2, 3, 4])    
	set和dict的唯一区别仅在于没有存储对应的value，但是，set的原理和dict一样，所以，同样`不可以放入可变对象`，因为无法判断两个可变对象是否相等，也就无法保证set内部“不会有重复元素”。  


* ####再议不可变对象  
对于可变对象，比如list，对list进行操作，list内部的内容是会变化的，比如：     
 
		>>> a = ['c', 'b', 'a'] 
		>>> a.sort() 
		>>> a 
		['a', 'b', 'c']  
而对于不可变对象，比如str：  
  
		>>> a = 'abc' 
		>>> a.replace('a', 'A') 
		'Abc' 
		>>> a 
		'abc'  
  
	所以，对于不变对象来说，调用对象自身的任意方法，也不会改变该对象自身的内容。相反，这些方法会创建新的对象并返回，这样，就保证了不可变对象本身永远是不可变的。

##函数  

[Python内置了很多函数可供调用。](https://docs.python.org/2/library/functions.html
)  可以在交互式命令行通过`help(abs)`查看abs函数的帮助信息。

###调用函数  
调用函数的时候，如果传入的参数数量不对，会报`TypeError`的错误，并且Python会明确地告诉你：abs()有且仅有1个参数，但给出了两个：  
  
	>>> abs(1, 2) 
	Traceback (most recent call last): 
	  File "<stdin>", line 1, in <module> 
	TypeError: abs() takes exactly one argument (2 given)  
  
如果传入的参数数量是对的，但参数类型不能被函数所接受，也会报TypeError的错误，并且给出错误信息：str是错误的参数类型：  
  
	>>> abs('a') 
	Traceback (most recent call last): 
	  File "<stdin>", line 1, in <module> 
	TypeError: bad operand type for abs(): 'str'  
  
比较函数cmp(x, y)就需要两个参数，如果x<y，返回-1，如果x==y，返回0，如果x>y，返回1：  
  
	>>> cmp(1, 2) 
	-1 
	>>> cmp(2, 1) 
	1 
	>>> cmp(3, 3) 
	0  
	
####数据类型转换  
Python内置的常用函数还包括数据类型转换函数，比如`int()`函数可以把其他数据类型转换为整数:  
  
	>>> int('123') 
	123 
	>>> int(12.34) 
	12 
	>>> float('12.34') 
	12.34 
	>>> str(1.23) 
	'1.23' 
	>>> unicode(100) 
	u'100' 
	>>> bool(1) 
	True 
	>>> bool('') 
	False  
  
函数名其实就是指向一个函数对象的引用，完全`可以把函数名赋给一个变量`，相当于给这个函数起了一个“别名”：  
  
	>>> a = abs # 变量a指向abs函数 
	>>> a(-1) # 所以也可以通过a调用abs函数 
	1
	
###定义函数  
在Python中，定义一个函数要使用`def`语句，依次写出函数名、括号、括号中的参数和冒号`:`，然后，在缩进块中编写函数体，函数的返回值用`return`语句返回。  
  
	def my_abs(x): 
		if x >= 0: 
			return x 
		else: 
			return -x  
			
如果没有return语句，函数执行完毕后也会返回结果，只是结果为`None`。`return None`可以简写为`return`。  

####空函数  
如果想定义一个什么事也不做的空函数，可以用`pass`语句：  
  
	def nop(): 
		pass  
`pass`语句什么都不做，用来作为占位符，比如现在还没想好怎么写函数的代码，就可以先放一个`pass`，让代码能运行起来。`pass`还可以用在其他语句里，比如：  
  
	if age >= 18: 
		pass  
缺少了`pass`，代码运行就会有语法错误。

####参数检查    
修改一下my_abs的定义，对参数类型做检查，只允许整数和浮点数类型的参数。数据类型检查可以用内置函数`isinstance`实现：  
  
	def my_abs(x): 
		if not isinstance(x, (int, float)): 
			raise TypeError('bad operand type') 
		if x >= 0: 
			return x 
		else: 
			return -x
####返回多个值  
函数可以返回多个值吗？答案是肯定的。

比如在游戏中经常需要从一个点移动到另一个点，给出坐标、位移和角度，就可以计算出新的新的坐标：  
  
	import math 

	def move(x, y, step, angle=0): 
		nx = x + step * math.cos(angle) 
		ny = y - step * math.sin(angle) 
		return nx, ny

这样我们就可以同时获得返回值：  
  
	>>> x, y = move(100, 100, 60, math.pi / 6) 
	>>> print x, y 
	151.961524227 70.0  
  
但其实这只是一种假象，Python函数返回的仍然是单一值：  
  
	>>> r = move(100, 100, 60, math.pi / 6) 
	>>> print r 
	(151.96152422706632, 70.0)  
	
原来返回值是一个tuple！但是，在语法上，返回一个tuple可以省略括号，而多个变量可以同时接收一个tuple，按位置赋给对应的值，所以，Python的函数返回多值其实就是返回一个tuple，但写起来更方便。

###函数的参数
####默认参数    
由于我们经常计算x2，所以，完全可以把第二个参数n的默认值设定为2：
	  
	def power(x, n=2):   
	s = 1   
	while n > 0:   
		n = n - 1   
		s = s * x   
		return s  
这样，当我们调用`power(5)`时，相当于调用`power(5, 2)`。    

设置默认参数时，有几点要注意：

* 一是必选参数在前，默认参数在后，否则Python的解释器会报错（思考一下为什么默认参数不能放在必选参数前面）；

* 二是如何设置默认参数。    
* **默认参数必须指向不变对象**！    

		def add_end(L=None): 
			if L is None: 
				L = [] 
			L.append('END') 
			return L
  
有多个默认参数时，调用的时候，既可以按顺序提供默认参数，也可以不按顺序提供部分默认参数。当不按顺序提供部分默认参数时，需要把参数名写上。比如调用`enroll('Adam', 'M', city='Tianjin')`，意思是，city参数用传进去的值，其他默认参数继续使用默认值。  
  
####可变参数  
在Python函数中，还可以定义可变参数。顾名思义，可变参数就是`传入的参数个数`是可变的，可以是1个、2个到任意个，还可以是0个。  以数学题为例子，`给定一组数字a，b，c……，请计算a2 + b2 + c2 + ……`，要定义出这个函数，我们必须确定输入的参数。由于参数个数不确定，我们首先想到可以把a，b，c……作为一个list或tuple传进来，这样，函数可以定义如下：  
  
	def calc(numbers): 
		sum = 0 
		for n in numbers: 
			sum = sum + n * n 
		return sum
  
但是调用的时候，需要先组装出一个list或tuple：`calc([1, 2, 3])`or`calc((1, 3, 5, 7))`。如果利用可变参数，调用函数的方式可以简化成这样：

	def calc(*numbers): 
		sum = 0 
		for n in numbers: 
			sum = sum + n * n 
		return sum  
调用该函数时，可以传入任意个参数，包括0个参数：`calc(1, 2)`or`calc()`。如果已经有一个list或者tuple，要调用一个可变参数，Python允许你在list或tuple前面加一个*号，把list或tuple的元素变成可变参数传进去：    

	>>>nums = [1, 2, 3] 
	>>>calc(*nums)  
  
####关键字参数  
关键字参数允许你传入0个或任意个含参数名的参数，这些关键字参数在函数内部自动组装为一个dict。请看示例：  
  
	def person(name, age, **kw): 
		print 'name:', name, 'age:', age, 'other:', kw  
  
在调用该函数时，可以只传入必选参数：  
  
	>>> person('Michael', 30) 
	name: Michael age: 30 other: {}  
也可以传入任意个数的关键字参数：  
  
	>>> person('Adam', 45, gender='M', job='Engineer') 
	name: Adam age: 45 other: {'gender': 'M', 'job': 'Engineer'}  
关键字参数有什么用？它可以扩展函数的功能。比如，在`person`函数里，我们保证能接收到`name`和`age`这两个参数，但是，如果调用者愿意提供更多的参数，我们也能收到。试想你正在做一个用户注册的功能，除了用户名和年龄是必填项外，其他都是可选项，利用关键字参数来定义这个函数就能满足注册的需求。  
  
和可变参数类似，也可以先组装出一个dict，然后，把该dict转换为关键字参数传进去：  
  
	>>> kw = {'city': 'Beijing', 'job': 'Engineer'} 
	>>> person('Jack', 24, **kw) 
	name: Jack age: 24 other: {'city': 'Beijing', 'job': 'Engineer'}  
  
####参数组合  
在Python中定义函数，可以用必选参数、默认参数、可变参数和关键字参数，这4种参数都可以一起使用，或者只用其中某些，但是请注意，**参数定义的顺序必须是：必选参数、默认参数、可变参数和关键字参数。**

比如定义一个函数，包含上述4种参数：  
  
	def func(a, b, c=0, *args, **kw): 
		print 'a =', a, 'b =', b, 'c =', c, 'args =', args, 'kw =', kw  
在函数调用的时候，Python解释器自动按照参数位置和参数名把对应的参数传进去。  
  
	>>> func(1, 2) 
	a = 1 b = 2 c = 0 args = () kw = {} 
	>>> func(1, 2, c=3) 
	a = 1 b = 2 c = 3 args = () kw = {} 
	>>> func(1, 2, 3, 'a', 'b') 
	a = 1 b = 2 c = 3 args = ('a', 'b') kw = {} 
	>>> func(1, 2, 3, 'a', 'b', x=99) 
	a = 1 b = 2 c = 3 args = ('a', 'b') kw = {'x': 99}  
通过一个tuple和dict，你也可以调用该函数：  
  
	>>> args = (1, 2, 3, 4) 
	>>> kw = {'x': 99} 
	>>> func(*args, **kw) 
	a = 1 b = 2 c = 3 args = (4,) kw = {'x': 99}  
所以，对于任意函数，都可以通过类似`func(*args, **kw)`的形式调用它，
无论它的参数是如何定义的。  

####小结

Python的函数具有非常灵活的参数形态，既可以实现简单的调用，又可以传入非常复杂的参数。

默认参数一定要用不可变对象，如果是可变对象，运行会有逻辑错误！

要注意定义可变参数和关键字参数的语法：

`*args`是可变参数，args接收的是一个`tuple`；

`**kw`是关键字参数，kw接收的是一个`dict`。

以及调用函数时如何传入可变参数和关键字参数的语法：

可变参数既可以直接传入：`func(1, 2, 3)`，又可以先组装`list或tuple`，
再通过`*args`传入：`func(*(1, 2, 3))`；

关键字参数既可以直接传入：`func(a=1, b=2)`，又可以先组装`dict`，
再通过`**kw`传入：`func(**{'a': 1, 'b': 2})`。

使用`*args`和`**kw`是Python的习惯写法，当然也可以用其他参数名，但最好使用习惯用法。
###递归函数  
计算阶乘n! = 1 x 2 x 3 x ... x n，用递归的方式写出来就是：  
  
	def fact(n): 
		if n==1: 
			return 1 
		return n * fact(n - 1)  
使用递归函数需要注意防止栈溢出。在计算机中，函数调用是通过栈（stack）这种数据结构实现的，
每当进入一个函数调用，栈就会加一层栈帧，每当函数返回，栈就会减一层栈帧。
由于栈的大小不是无限的，所以，递归调用的次数过多，会导致栈溢出。  

解决递归调用栈溢出的方法是通过**尾递归**优化，事实上尾递归和循环的效果是一样的，所以，把循环看成是一种特殊的尾递归函数也是可以的。

尾递归是指，在函数返回的时候，调用自身本身，并且，**return语句不能包含表达式**。这样，编译器或者解释器就可以把尾递归做优化，使递归本身无论调用多少次，都只占用一个栈帧，不会出现栈溢出的情况。

上面的`fact(n)`函数由于`return n * fact(n - 1)`引入了乘法表达式，所以就不是尾递归了。要改成尾递归方式，需要多一点代码，主要是要把每一步的乘积传入到递归函数中：  
  
	def fact(n): 
		return fact_iter(1, 1, n) 
	
	def fact_iter(product, count, max): 
		if count > max: 
			return product 
		return fact_iter(product * count, count + 1, max)  
  
可以看到，`return fact_iter(product * count, count + 1, max)`仅返回递归函数本身，`product * count和count + 1`在函数调用前就会被计算，不影响函数调用。  
  
遗憾的是，大多数编程语言没有针对尾递归做优化，Python解释器也没有做优化，所以，
即使把上面的fact(n)函数改成尾递归方式，也会导致栈溢出。

有一个针对尾递归优化的`decorator`，可以参考源码：

http://code.activestate.com/recipes/474088-tail-call-optimization-decorator/

我们后面会讲到如何编写decorator。现在，只需要使用这个@tail_call_optimized，
就可以顺利计算出fact(1000)
##高级特性
###切片  
取一个list或tuple的部分元素是非常常见的操作。Python提供了切片（Slice）操作符，
能大大简化这种操作。对应上面的问题，取前3个元素，用一行代码就可以完成切片：  
  
	>>> L = ['Michael', 'Sarah', 'Tracy', 'Bob', 'Jack']  
	>>> L[0:3] 
	['Michael', 'Sarah', 'Tracy']  
`L[0:3]`表示，从索引0开始取，直到索引3为止，但不包括索引3。如果第一个索引是0，还可以省略：`L[:3]`。它同样支持倒数切片，倒数第一个元素的索引是`-1`。：  
  
	>>> L[-2:] 
	['Bob', 'Jack'] 
	>>> L[-2:-1] 
	['Bob']  
切片操作十分有用。我们先创建一个0-99的数列：  
  
	>>> L = range(100)  
	>>> L[10:20] #前11-20个数
	[10, 11, 12, 13, 14, 15, 16, 17, 18, 19]  
	>>> L[:10:2] #前10个数，每两个取一个
	[0, 2, 4, 6, 8]  
	>>> L[::5] #所有数，每5个取一个
	[0, 5, 10, 15, 20, 25, 30, 35, 40, 45, 50, 55, 60, 65, 70, 75, 80, 85, 90, 95]  
什么都不写，只写[:]就可以原样复制一个list：`L[:]`  
  
tuple也是一种list，唯一区别是tuple不可变。因此，tuple也可以用切片操作，
只是操作的结果仍是tuple：  
	  
	>>> (0, 1, 2, 3, 4, 5)[:3] 
	(0, 1, 2)  
字符串'xxx'或Unicode字符串u'xxx'也可以看成是一种list，每个元素就是一个字符。
因此，字符串也可以用切片操作，只是操作结果仍是字符串：  
  
	>>> 'ABCDEFG'[:3] 
	'ABC' 
	>>> 'ABCDEFG'[::2] 
	'ACEG'
###迭代  
如果给定一个list或tuple，我们可以通过for循环来遍历这个list或tuple，这种遍历我们称为迭代（Iteration）。Python的for循环不仅可以用在list或tuple上，还可以作用在其他可迭代对象上。    

**dict的迭代：**  
  
	>>> d = {'a': 1, 'b': 2, 'c': 3} 
	>>> for key in d: 
	... 	print key 
	...  
因为dict的存储不是按照list的方式顺序排列，所以，**迭代出的结果顺序很可能不一样**。

默认情况下，dict迭代的是key。如果要迭代value，可以用`for value in d.itervalues()`，如果要同时迭代key和value，可以用`for k, v in d.iteritems()`。  
  
**字符串的迭代：**  
  
	>>> for ch in 'ABC': 
	... 	print ch 
	...  
  
**如何判断一个对象是可迭代对象呢？**方法是通过`collections`模块的`Iterable`类型判断：  
  
	>>> from collections import Iterable 
	>>> isinstance('abc', Iterable) # str是否可迭代 
	True 
	>>> isinstance([1,2,3], Iterable) # list是否可迭代 
	True 
	>>> isinstance(123, Iterable) # 整数是否可迭代 
	False  
  
**如果要对list实现类似Java那样的下标循环怎么办？**Python内置的`enumerate`函数可以把一个list变成索引-元素对，这样就可以在for循环中同时迭代索引和元素本身：  
  
	>>> for i, value in enumerate(['A', 'B', 'C']): 
	... 	print i, value 
	... 
	0 A 
	1 B 
	2 C
###列表生成式  
生成`list [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]`可以用`range(1, 11)`。  

要生成`[1x1, 2x2, 3x3, ..., 10x10]`可以用`[x * x for x in range(1, 11)]`，把要生成的元素`x * x`放到前面，后面跟for循环，就可以把list创建出来。    

for循环后面还可以加上`if`判断，这样我们就可以筛选出仅偶数的平方：`[x * x for x in range(1, 11) if x % 2 == 0]`。  
还可以使用两层循环，可以生成全排列：  
  
	>>> [m + n for m in 'ABC' for n in 'XYZ'] 
	['AX', 'AY', 'AZ', 'BX', 'BY', 'BZ', 'CX', 'CY', 'CZ']  #生成list
例如，列出当前目录下的所有文件和目录名，可以通过一行代码实现：  
  
	>>> import os # 导入os模块，模块的概念后面讲到 
	>>> [d for d in os.listdir('.')] # os.listdir可以列出文件和目录  
  
for循环其实可以同时使用两个甚至多个变量，比如`dict的iteritems()`可以同时迭代key和value：  
  
	>>> d = {'x': 'A', 'y': 'B', 'z': 'C' } 
	>>> for k, v in d.iteritems(): 
	... 	print k, '=', v 
	... 
	y = B 
	x = A 
	z = C  
  
把一个list中所有的字符串(使用内建的`isinstance`函数可以判断一个变量是不是字符串)变成小写:  
  
	>>> L = ['Hello', 'World', 18, 'Apple', None]  
	>>> [s.lower() for s in L if isinstance(s, str)]
###生成器  
通过列表生成式，我们可以直接创建一个列表。但是，受到内存限制，列表容量肯定是有限的。而且，创建一个包含100万个元素的列表，不仅占用很大的存储空间，如果我们仅仅需要访问前面几个元素，那后面绝大多数元素占用的空间都白白浪费了。

所以，如果列表元素可以按照某种算法推算出来，那我们是否可以在循环的过程中不断推算出后续的元素呢？这样就不必创建完整的list，从而节省大量的空间。在Python中，这种一边循环一边计算的机制，称为生成器（Generator）。

要创建一个generator，有很多种方法。第一种方法很简单，只要把一个列表生成式的[]改成()，就创建了一个generator：  
  
	>>> L = [x * x for x in range(10)] 
	>>> L 
	[0, 1, 4, 9, 16, 25, 36, 49, 64, 81] 
	>>> g = (x * x for x in range(10)) 
	>>> g 
	<generator object <genexpr> at 0x104feab40>  
创建`L`和`g`的区别仅在于最外层的`[]`和`()`，L是一个list，而g是一个generator。如果要一个一个打印出来，可以通过generator的`next()`方法。
##函数式编程
###高阶函数    
把函数作为参数传入，这样的函数称为高阶函数，函数式编程就是指这种高度抽象的编程范式。  

**变量可以指向函数**    
  
	>>> f = abs 
	>>> f(-10) 
	10  
说明变量`f`现在已经指向了`abs`函数本身。  

**函数名也是变量**    
函数名是什么呢？函数名其实就是指向函数的变量！对于abs()这个函数，完全可以把函数名abs看成变量，它指向一个可以计算绝对值的函数！  
  
	>>> abs = 10 
	>>> abs(-10) 
	Traceback (most recent call last): 
	File "<stdin>", line 1, in <module> 
	TypeError: 'int' object is not callable  
把abs指向10后，就无法通过abs(-10)调用该函数了！因为abs这个变量已经不指向求绝对值函数了！

当然实际代码绝对不能这么写，这里是为了说明函数名也是变量。要恢复abs函数，请重启Python交互环境。  

**传入函数**  
既然变量可以指向函数，函数的参数能接收变量，那么一个函数就可以接收另一个函数作为参数，这种函数就称之为高阶函数。  
  
	def add(x, y, f): 
		return f(x) + f(y)  
	>>> add(-5, 6, abs) 
	11
####map/reduce  
#####map  

`map()`函数接收两个参数，一个是函数，一个是序列，map将传入的函数依次作用到序列的每个元素，并把结果作为新的list返回。  
比如我们有一个函数`f(x)=x*x`，要把这个函数作用在一个list `[1, 2, 3, 4, 5, 6, 7, 8, 9]`上，就可以用map()实现如下：  
  
	>>> def f(x): 
	... 	return x * x 
	... 
	>>> map(f, [1, 2, 3, 4, 5, 6, 7, 8, 9]) 
	[1, 4, 9, 16, 25, 36, 49, 64, 81]  
把这个list所有数字转为字符串：
  
	>>> map(str, [1, 2, 3, 4, 5, 6, 7, 8, 9]) 
	['1', '2', '3', '4', '5', '6', '7', '8', '9']  
#####reduce 
`reduce`把一个函数作用在一个序列[x1, x2, x3...]上，这个函数必须接收两个参数，reduce把结果继续和序列的下一个元素做累积计算，其效果就是：`reduce(f, [x1, x2, x3, x4]) = f(f(f(x1, x2), x3), x4)`    

如果要把序列`[1, 3, 5, 7, 9]`变换成整数`13579`（假设Python没有提供int()函数），reduce就可以派上用场：  
  
	def char2num(s): 
		return {'0': 0, '1': 1, '2': 2, '3': 3, '4': 4, '5': 5, '6': 6, '7': 7, '8': 8, '9': 9}[s] 
	def str2int(s): 
		return reduce(lambda x,y: x*10+y, map(char2num, s))  
#####练习  
利用map()函数，把用户输入的不规范的英文名字，变为首字母大写，其他小写的规范名字。输入：['adam', 'LISA', 'barT']，输出：['Adam', 'Lisa', 'Bart']:  
  
	>>> def upperFirstChar(s):
	...     return s[0].upper()+s[1:]
	...   
	>>> map(upperFirstChar,['adam', 'LISA', 'barT'])
	['Adam', 'Lisa', 'Bart'] 
  
编写一个prod()函数，可以接受一个list并利用reduce()求积:  
  
	>>> def prod(l):
	...     return reduce((lambda x,y:x*y),l)
	... 
	>>> prod([1,2,3,4])
	24
####filter  
`filter()`函数用于过滤序列。  
和`map()`类似，`filter()`也接收一个函数和一个序列。和map()不同的时，filter()把传入的函数依次作用于每个元素，然后根据返回值是`True`还是`False`决定保留还是丢弃该元素。  
例如，在一个list中，删掉偶数，只保留奇数，可以这么写：  
  
	def is_odd(n): 
		return n % 2 == 1 
	filter(is_odd, [1, 2, 4, 5, 6, 9, 10, 15]) 
	# 结果: [1, 5, 9, 15]
####sorted  
Python内置的`sorted()`函数就可以对list进行排序：  
  
	>>> sorted([36, 5, 12, 9, 21]) 
	[5, 9, 12, 21, 36]  
此外，sorted()函数也是一个高阶函数，它还可以接收一个比较函数来实现**自定义的排序**。比如，如果要倒序排序，我们就可以自定义一个reversed_cmp函数：  
  
	def reversed_cmp(x, y): 
		if x > y: 
			return -1 
		if x < y: 
			return 1 
		return 0  
	>>> sorted([36, 5, 12, 9, 21], reversed_cmp) 
	[36, 21, 12, 9, 5]  
**注意：**默认情况下，对字符串排序，是按照`ASCII`的大小比较的，由于`'Z' < 'a'`，结果，大写字母Z会排在小写字母a的前面。
###返回函数
###匿名函数
###装饰器
###偏函数
##模块
###使用模块
###安装第三方模块
###使用__future__
##面向对象编程
###类和实例
###访问限制
###继承和多态
###获取对象信息
##面向对象高级编程
###使用__slots__
###使用@property
###多重继承
###定制类
###使用元类
##错误、调试和测试
###错误处理
###调试
###单元测试
###文档测试
##IO编程
###文件读写
###操作文件和目录
###序列化
##进程和线程
###多进程
###多线程
###ThreadLocal
###进程 vs. 线程
###分布式进程
##正则表达式
##常用内建模块
###collections
###base64
###struct
###hashlib
###itertools
###XML
###HTMLParser
##常用第三方模块
###PIL
##图形界面
##网络编程
###TCP/IP简介
###TCP编程
###UDP编程
##电子邮件
###SMTP发送邮件
###POP3收取邮件
##访问数据库
###使用SQLite
###使用MySQL
###使用SQLAlchemy
##Web开发
###HTTP协议简介
###HTML简介
###WSGI接口
###使用Web框架
###使用模板
##协程
###gevent
##实战
###Day 1 - 搭建开发环境
###Day 2 - 编写数据库模块
###Day 3 - 编写ORM
###Day 4 - 编写Model
###Day 5 - 编写Web框架
###Day 6 - 添加配置文件
###Day 7 - 编写MVC
###Day 8 - 构建前端
###Day 9 - 编写API
###Day 10 - 用户注册和登录
###Day 11 - 编写日志创建页
###Day 12 - 编写日志列表页
###Day 13 - 提升开发效率
###Day 14 - 完成Web App
###Day 15 - 部署Web App
###Day 16 - 编写移动App