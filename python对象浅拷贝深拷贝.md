### python对象浅拷贝深拷贝
* 所谓浅拷贝就是对引用的拷贝，所谓深拷贝就是对对象的资源的拷贝。示例代码：

		>>> temp = [1,2]
		>>> nt = temp
		>>> id(temp)
		4446894128
		>>> id(nt)
		4446894128
		>>> nt = temp[:]
		>>> id(nt)
		4447468144
		>>> nt = list(temp)
		>>> id(nt)
		4447634064
		>>> import copy
		>>> nt = copy.copy(temp)
		>>> id(nt)
		4447635360

* 直接赋值很好理解, nt的id显然应该和temp是一致的, 但是通过切片的方式或者工厂函数以及通过 copy 函数创建的对象有着不同的id. 实际上通过 切片 , 工厂函数 或者 copy 函数的方式来拷贝对象, 就是一种 浅拷贝 . 浅拷贝只拷贝父对象.那为什么内存地址会变了，是因为切片的方式或者工厂函数以及通过 copy都创建了一个新对象，区别于temp对象，所以内存地址变了。

		In [12]: obj = ['name',['age',18]]
		In [13]: a=obj[:]
		In [14]: b=list(obj)
		In [15]: for x in obj,a,b:
   		   ....:         print id(x)
      	   ....:
		4415437424
		4415437712
		4415435768
		In [16]: a[0] = 'lisi'
		In [17]: b[0] = 'zhangsan'
		In [18]:
		In [18]: print a
		['lisi', ['age', 18]]
		In [19]: print b
		['zhangsan', ['age', 18]]
		In [20]:
		In [20]: a[1][1] = 25
		In [21]:
		In [21]: print a
		['lisi', ['age', 25]]
		In [22]: print b
		['zhangsan', ['age', 25]]
* 在这个例子中, 修改a和b的名字都不会互相影响, 单只是修改了a的年龄, 为什么就改变b中的年龄呢?

* 实际上, 我们创建的a与b都是从obj对象的浅拷贝, obj中第一个元素是字符串属于不可变类型(immutable), 第二个元素是列表属于可变类型(mutable). 因此我们进行拷贝对象时, 字符串被显示拷贝重新创建了一个字符串, 而列表只是复制引用, 所以改变列表的元素会影响所有引用对象.

* 这个时候深拷贝就登场了. 之前例子中出现过 copy 这个模块, 这个模块中除了出现过了 copy 方法来做浅拷贝之外, 还有一个方法 deepcopy , 这个方法就可以对一个对象做深拷贝.

		In [12]: import copy
		In [13]: obj = ['name',['age',18]]
		In [14]: a = copy.deepcopy(obj)

		In [15]: b = copy.deepcopy(obj)

		In [16]: a[1][1] = 23

		In [17]: b[1][1] = 25

		In [18]: a
		Out[18]: ['name', ['age', 23]]

		In [19]: b
		Out[19]: ['name', ['age', 25]]

		In [20]: obj
		Out[20]: ['name', ['age', 18]]


