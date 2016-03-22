# gradle-example
gradle example

##ch05 动态任务

	4.times { counter ->
	    task "task$counter" << {
	        println "I'm task number $counter"
	    }
	}
	
###定义一个counter进行循环得到任务  这里动态的创建了 task0, task1, task2, task3