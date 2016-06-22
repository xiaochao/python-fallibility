### python元组修改
* 元组是个不可变对象，所以元组的值是不能修改的，示例代码如下：

		>>> a=(0,)
		>>> a[0]+=1
		Traceback (most recent call last):
  		  File "<stdin>", line 1, in <module>
		TypeError: 'tuple' object does not support item assignment
* 尝试修改元组元素的值，结果抛了异常，这是正常的。再看一个示例

		>>> x = ([],)
		>>> x
		([],)
		>>> x[0] += [1]
		Traceback (most recent call last):
  		  File "<stdin>", line 1, in <module>
		TypeError: 'tuple' object does not support item assignment
		>>> x
		([1],)
* 这地方抛了异常，说元素值不能被修改，但是实际情况是，元素的值被修改了。我们来看一下，汇编层面，这段代码都做了啥。

		>>> import dis
		>>> dis.dis(compile('x[0] += [1]', '<string>', 'exec'))
  		  1           0 LOAD_NAME                0 (x)
              		  3 LOAD_CONST               0 (0)
              		  6 DUP_TOPX                 2
              		  -- put x[0] on the stack --
              		  9 BINARY_SUBSCR            
             		  10 LOAD_CONST               1 (1)
             		  13 BUILD_LIST               1
              		  -- do the "+=" --
             		  16 INPLACE_ADD
             		  17 ROT_THREE           
              		  -- store new value in x[0] --
             		  18 STORE_SUBSCR
             		  19 LOAD_CONST               2 (None)
             		  22 RETURN_VALUE 
* 可以看出，汇编层面，先是执行了+=这个操作，由于元素0的值是个list，是个可变对象，所以这时候，元素0变成了[1],最后，把元素0赋值给元素0，发生了异常，但由于元素0存放的指针地址，赋值前后地址是一样的，所以这地方的赋值成功与否，值都是一样的，所以异常是元组抛出的，但修改值是list完成的。
* 想要不抛出这个异常，x[0].extends([1])，这样就只是对元素0的list操作，而不会对元组操作。 