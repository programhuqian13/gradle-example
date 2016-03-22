# gradle-example
gradle example

##ch04-1 任务依赖
	task hello << {
		println 'Hello world!'
	}

	task intro(dependsOn: hello) << {
	    println "I'm Gradle"
	}
###intro 依赖于 hello, 所以执行 intro 的时候 hello 命令会被优先执行来作为启动 intro 任务的条件.