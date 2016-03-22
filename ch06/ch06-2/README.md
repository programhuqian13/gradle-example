# gradle-example
gradle example

##ch06 使用已经存在的任务
###ch06-2通过API访问一个任务 - 加入行为
		task hello << {
		    println 'Hello Earth'
		}
		hello.doFirst {
		    println 'Hello Venus'
		}
		hello.doLast {
		    println 'Hello Mars'
		}
		hello << {
		    println 'Hello Jupiter'
		}
		结果：  Hello Venus
			  Hello Earth
			  Hello Mars
			  Hello Jupiter
			  
		doFirst和doLast 可以被执行许多次，他们分别可以在任务动作列表的开始和结束加入动作。