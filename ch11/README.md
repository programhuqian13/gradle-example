# gradle-example
gradle example


##ch11 默认任务

	Gradle 允许在脚本中定义一个或多个默认任务.
	defaultTasks 'clean','run'

	task clean << {
		println "default cleaning!"
	}
	
	task run << {
		println "default running!"
	}
	
	task other << {
		println "other task running!"
	}
	结果：
	default cleaning!
	default running!