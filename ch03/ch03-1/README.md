# gradle-example
gradle example
	
##ch03构建脚本代码
	#ch03-1	
	task upper << {
	    String someString = 'mY_nAmE'
	    println "Original: " + someString
	    println "Upper case: " + someString.toUpperCase()
	}
	这里定义了一个字符串类型的变量，someString，进行相应的调用。  运用了toUpperCase()，这个方法是进行将字符串进行大写显示