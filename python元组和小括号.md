### python元组和小括号
示例代码：

	>>> a = ()
	>>> type(a)
	<type 'tuple'>
	>>> a = (1)
	>>> type(a)
	<type 'int'>
	>>> a
	1
	>>> a = 1,	
	>>> a
	(1,)
	>>> type(a)
	<type 'tuple'>
* 可以看出a=(1)后，a是个int，而且值是1，小括号了？为什么不是tuple？
* 在python中，tuple和小括号没直接关系，只是在打印显示的时候，用小括号来表示,而真正表示tuple是逗号，有没有括号没关系，所以，如果在编程的时候，不小心在变量后加了逗号，python是不会报错的，他会把变量当做tuple去处理，程序也就跑飞了。