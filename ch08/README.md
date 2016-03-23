# gradle-example
gradle example

##ch08 自定义任务属性
	给任务加入自定义属性
	task myTask {
    	ext.myProperty = "myValue"
	}
	
	task printTaskProperties << {
	    println myTask.myProperty
	}
	给任务加自定义属性是没有限制的