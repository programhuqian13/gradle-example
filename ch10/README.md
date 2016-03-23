# gradle-example
gradle example

##ch10 使用方法
	Gradle 能很好地衡量你编写脚本的逻辑能力. 首先要做的是如何提取一个方法
	task checksum << {
	    fileList('antFile').each {File file ->
	        ant.checksum(file: file, property: "cs_$file.name")
	        println "$file.name Checksum: ${ant.properties["cs_$file.name"]}"
	    }
	}
	
	task loadfile << {
	    fileList('antFile').each {File file ->
	        ant.loadfile(srcFile: file, property: file.name)
	        println "I'm fond of $file.name"
	    }
	}
	
	File[] fileList(String dir) {
	    file(dir).listFiles({file -> file.isFile() } as FileFilter).sort()
	}
	结果：
		I'm fond of file1.txt
		I'm fond of file2.txt
		I'm fond of file3.txt
	这种方法可以在多项目构建的子项目之间共享