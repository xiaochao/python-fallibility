### is和==的区别
在python中，is表示比较两个对象的对象类型id是否一致，==比较的是两个对象的值是否相等，对于python的内建对象来说，==返回True的时候，is也返回True，示例代码如下：

	>>> a = 1
	>>> b = 1
	>>> a is b
	True

	>>> a == b
	True

	>>> c = 257
	>>> d = 257
	>>> c == d
	True

	>>> c is d
	False

	>>> e = -6
	>>> f = -6
	>>> e is f
	False

	>>> e == f
	True
python缓存了-5 到 256的对象, 所以在这个之间的相同的数, is返回的都会是 True , 但是2个对象不在这个区间所以 is 返回的是 False , 但是 == 总是返回 True .

字符串也有缓存, 对只含有 字母 , 数字 , 下划线 组成的字符串来说, 相同的字符串 is 和 == 返回的是 True，如果包含了其他字符, 则 is 返回 False , == 为 True，示例代码如下：

	>>> a = 'hello'
	>>> b = 'hello'
	>>> a is b
	True

	>>> a == b
	True
	
	>>> a = '!a'
	>>> b = '!a'
	>>> a is b
	False
	
	>>> a = 'hello world'
	>>> b = 'hello world'
	>>> a is b
	False
	
	>>> a = '!a'
	>>> b = '!a'
	>>> a is b
	False

	>>> a = 'hello world'
	>>> b = 'hello world'
	>>> a is b
	False
当然，python还有个特殊的字符串对象，'nan'，看个例子。

	>>> a = float('nan')
	>>> a is a
	True
	>>> a == a
	False
	>>> a
	nan
	>>> type(a)
	<type 'float'>
is返回True是因为a是float类型，所以is返回True，而a的具体的值是不确定的，只是个代表，代表是最小数。随意==返回时false。