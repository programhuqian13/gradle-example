# gradle-example
gradle example

##ch01
	###构建脚本定义了一个独立的 task,
		task hello {
		    doLast {
		        println 'Hello world!'
		    }
		}
	这个任务就是打印出Hello world!，执行命令为 gradle -q hello ，-q是不会生成 Gradle 的日志信息
