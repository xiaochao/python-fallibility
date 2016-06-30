### While 1比While True快

	import timeit
 
	def while_one():
    	i = 0
    	while 1:
        	i += 1
        	if i == 10000000:
            	break
 
	def while_true():
    	i = 0
    	while True:
        	i += 1
        	if i == 10000000:
            	break
 
	if __name__ == "__main__":
    	w1 = timeit.timeit(while_one, "from __main__ import while_one", number=3)
    	wt = timeit.timeit(while_true, "from __main__ import while_true", number=3)
    	print "while one: %s\nwhile_true: %s" % (w1, wt)

	执行结果：
	while one: 1.37000703812
	while_true: 2.07638716698

* 可以看出wihle 1的执行时间约为while True的2/3。
* 由于Python2中，True/False不是关键字，因此我们可以对其进行任意的赋值，这就导致程序在每次循环时都需要对True/False的值进行检查；而对于1，则被程序进行了优化，而后不会再进行检查。

		import dis
 
		def while_one():
    		while 1:
        		pass
 
		def while_true():
    		while True:
        		pass
 
		if __name__ == "__main__":
    		print "while_one\n"
    		dis.dis(while_one)
    
    		print "while_true\n"
    		dis.dis(while_true)
  
* 执行结果

		while_one
 
  		  6           0 SETUP_LOOP               3 (to 6)
 
    	  7     >>    3 JUMP_ABSOLUTE            3
  		  		>>    6 LOAD_CONST               0 (None)
              		  9 RETURN_VALUE        
  		  while_true
 
  		  10          0 SETUP_LOOP              10 (to 13)
  		  		>>    3 LOAD_GLOBAL              0 (True)
              		  6 POP_JUMP_IF_FALSE       12
 
 		  11          9 JUMP_ABSOLUTE            3
        		>>   12 POP_BLOCK           
        		>>   13 LOAD_CONST               0 (None)
                     16 RETURN_VALUE
                     
* 可以看出，正如上面所讲到的，在while True的时候，字节码中多出了几行语句，正是这几行语句进行了True值的检查。