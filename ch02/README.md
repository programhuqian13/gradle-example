# gradle-example
gradle example

##ch02进行快捷的任务定义
		task hello << {
		    println 'Hello world!'
		}
	doLast 被替换成了 ‘<<’