# gradle-example
gradle example

##ch09 调用 Ant 任务
	task loadfile << {
	    def files = file('../antLoadfileResources').listFiles().sort()
	    files.each { File file ->
	        if (file.isFile()) {
	            ant.loadfile(srcFile: file, property: file.name)
	            println " *** $file.name ***"
	            println "${ant.properties[file.name]}"
	        }
	    }
	}
	Ant 任务是Gradle的一等公民，Gradle通过Groovy出色的集成了Ant任务，Groovy自带了一个AntBuilder，相比于从一个build.xml文件中使用Ant任务，在Gradle里使用Ant任务更为方便和强大。
	结果：
	 *** file1.txt ***
	asda
	 *** file2.txt ***
	asdasd
	 *** file3.txt ***
	asdasd