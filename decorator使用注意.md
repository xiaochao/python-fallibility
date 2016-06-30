### decorator使用注意
* 写一个decorator的时候，最好在实现之前加上functools的wrap，它能保留原有函数的名称和docstring，例如：

		from functools import wraps  
		def my_decorator(f):  
    		@wraps(f)    # 最好加上这一句  
    		def wrapper(*args, **kwds):  
        		print 'Calling decorated function'  
        		return f(*args, **kwds)  
    		return wrapper  
 
		@my_decorator  
		def example():  
    		"""Docstring"""  
    		print 'Called example function'  
			print example.__name__, example.__doc__  
			
* 程序运行之后的输出是

		example Docstring  
* 如果去掉了 @wraps(f) 这一行，得到的结果会是这样的
		
		wrapper None  