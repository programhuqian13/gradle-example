# gradle-example
gradle example

##ch06 使用已经存在的任务
###ch06-1 当任务创建之后, 它可以通过API来访问
	通过API访问一个任务 - 加入一个依赖
	4.times { counter ->
	    task "task$counter" << {
	        println "I'm task number $counter"
	    }
	}
	task0.dependsOn task2, task3
	你可以给一个已经存在的任务加入行为.
	结果：
		I'm task number 2
		I'm task number 3
		I'm task number 0