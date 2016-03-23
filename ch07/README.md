# gradle-example
gradle example

##ch07 短标记法
###当成构建脚本的属性来访问一个任务
	task hello << {
	    println 'Hello world!'
	}
	hello.doLast {
	    println "Greetings from the $hello.name task."
	}
	name 是任务的默认属性, 代表当前任务的名称, 这里是 hello
	这使得代码易于读取， 特别是当使用了由插件（如编译）提供的任务时尤其如此.  doLast 后面不要加上<<