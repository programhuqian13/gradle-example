# gradle-example
gradle example

##ch04-2 任务依赖
	task taskX(dependsOn: 'taskY') << {
    	println 'taskX'
	}
	task taskY << {
    	println 'taskY'
	}
	
###taskX 到 taskY 的依赖在 taskY 被定义之前就已经声明了. 这一点对于我们之后讲到的多任务构建是非常重要的