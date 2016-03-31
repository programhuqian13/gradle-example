# gradle-example
gradle example

#grandle命令行适用 

##ch13 多任务调用
	你可以以列表的形式在命令行中一次调用多个任务. 例如 gradle compile test 命令会依次调用 compile 和 test 任务, 它们所依赖的任务也会被调用. 这些任务只会被调用一次, 无论它们是否被包含在脚本中:即无论是以命令行的形式定义的任务还是依赖于其它任务都会被调用执行
	task compile << {
		println "compling source"
	}
	
	task compileTest (dependsOn: compile) << {
		println "compling unit tests"
	}
	
	task test(dependsOn: [compile,compileTest]) << {
		println "running unit tests"
	}
	
	task dist(dependsOn: [compile,test]) << {
		println "building the distribution"
	}
	
	由于每个任务仅会被调用一次,所以调用gradle test test与调用gradle test效果是相同的
	结果：
	:compile
	compling source
	:compileTest
	compling unit tests
	:test
	running unit tests
	:dist
	building the distribution
	
	相关命令：
	-x：进行排除某些任务
	如：gradle dist -x test
	结果：
	:compile
	compling source
	:dist
	building the distribution
	
	test 任务并没有被调用,即使它是 dist 任务的依赖. 同时 test 任务的依赖任务 compileTest 也没有被调用,而像 compile 被 test 和其它任务同时依赖的任务仍然会被调用
	
##失败后继续执行构建
	默认情况下，只要有任务调用失败，Gradle就会中断执行，但是这样会使调用的过程更快，但是后面的错误信息没有办法发现，可以使用--continue选项在一次调用中尽可能多的发现所有问题。
	采用--continue选项，Gradle会调用每一个任务以及它们依赖的任务。而不是一旦出现错误就会中断执行。所有的错误信息都会在最后被列出来。
	一旦某个任务执行失败，那么所有依赖于该任务的子任务都不会被调用。
	
##简化任务名
	当你试图调用某个任务的时候, 你并不需要输入任务的全名. 只需提供足够的可以唯一区分出该任务的字符即可。
	如：gradle di 和上面的gradle dist是一样的效果。
	:compile
	compling source
	:compileTest
	compling unit tests
	:test
	running unit tests
	:dist
	building the distribution
	或者简化驼峰方式的任务名
	如:gradle cT 和gradle compileTest效果一样
	:compile
	compling source
	:compileTest
	compling unit tests
	
	简化后你仍然可以使用-x参数.进行排除某些任务。

##选择执行构建
	调用grandle命令时，默认情况下总是会构建当前目录下的文件，可以使用 -b 参数选择其他目录的构建文件，并且当你使用此参数时，setting.gradle将不会生效。在文件夹中创建一个subdir,文件下面创建文件myproject.gradle文件。
	
	task hello << {
		println "using build file '$buildFile.name' in '$buildFile.parentFile.name'"
	}
	
	运行结果：gradle -q -b subdir/myproject.gradle hello
	using build file 'myproject.gradle' in 'subdir'
	
	另外，可以使用 -p 参数来指定构建的目录，例如在多项目构建中可以使用 -p 来代替 -b 参数
	
	-b 参数用以指定脚本具体所在位置, 格式为 dirpwd/build.gradle.
	-p 参数用以指定脚本目录即可.
	
##获取构建信息
###项目列表
	执行gradle project命令会为你列出子项目名称列表。
	description 属性来指定这些描述信息：为项目添加描述信息
	如：
	description = "this is a test "
	显示结果：
	
	------------------------------------------------------------
	Root project - this is a test
	------------------------------------------------------------
	
	Root project 'ch13' - this is a test
	No sub-projects
	
###任务列表
	执行 gradle tasks 命令会列出项目中所有任务. 这会显示项目中所有的默认任务以及每个任务的描述.
	------------------------------------------------------------
	All tasks runnable from root project - this is a test
	------------------------------------------------------------
	
	Build Setup tasks
	-----------------
	init - Initializes a new Gradle build. [incubating]
	wrapper - Generates Gradle wrapper files. [incubating]
	
	Help tasks
	----------
	buildEnvironment - Displays all buildscript dependencies declared in root project 'ch13'.
	components - Displays the components produced by root project 'ch13'. [incubating]
	dependencies - Displays all dependencies declared in root project 'ch13'.
	dependencyInsight - Displays the insight into a specific dependency in root project 'ch13'.
	help - Displays a help message.
	model - Displays the configuration model of root project 'ch13'. [incubating]
	projects - Displays the sub-projects of root project 'ch13'.
	properties - Displays the properties of root project 'ch13'.
	tasks - Displays the tasks runnable from root project 'ch13'.
	
	Other tasks
	-----------
	dist
	可以用 --all 参数来收集更多任务信息. 这会列出项目中所有任务以及任务之间的依赖关系
	------------------------------------------------------------
	All tasks runnable from root project - this is a test
	------------------------------------------------------------
	
	Build Setup tasks
	-----------------
	init - Initializes a new Gradle build. [incubating]
	wrapper - Generates Gradle wrapper files. [incubating]
	
	Help tasks
	----------
	buildEnvironment - Displays all buildscript dependencies declared in root project 'ch13'.
	components - Displays the components produced by root project 'ch13'. [incubating]
	dependencies - Displays all dependencies declared in root project 'ch13'.
	dependencyInsight - Displays the insight into a specific dependency in root project 'ch13'.
	help - Displays a help message.
	model - Displays the configuration model of root project 'ch13'. [incubating]
	projects - Displays the sub-projects of root project 'ch13'.
	properties - Displays the properties of root project 'ch13'.
	tasks - Displays the tasks runnable from root project 'ch13'.
	
	Other tasks
	-----------
	dist
	    compile
	    compileTest
	    test

###获取任务具体信息
	执行 gradle help --task someTask 可以显示指定任务的详细信息. 或者多项目构建中相同任务名称的所有任务的信息
	获取任务帮助
	gradle -q help --task libs的输出结果
	Detailed task information for cT

	Path
	     :compileTest
	
	Type
	     Task (org.gradle.api.Task)
	
	Description
	     -
	
	Group
     -

###获取依赖列表
	执行 gradle dependencies 命令会列出项目的依赖列表, 所有依赖会根据任务区分,以树型结构展示出来
	
	虽然输出结果很多, 但这对于了解构建任务十分有用, 当然你可以通过 --configuration 参数来查看 指定构建任务的依赖情况
	
###查看特定依赖
	执行 gradle dependencyInsight 命令可以查看指定的依赖。
	
	dependencyInsight 任务是'Help'任务组中的一个. 这项任务需要进行配置才可以使用. Report 查找那些在指定的配置里特定的依赖.
	如果用了Java相关的插件, 那么 dependencyInsight 任务已经预先被配置到'compile'下了. 你只需要通过 '--dependency' 参数来制定所需查看的依赖即可. 如果你不想用默认配置的参数项你可以通过'--configuration'参数来进行指定
###获取项目属性列表
	执行 gradle properties 可以获取项目所有属性列表.
###构建日志
	--profile 参数可以收集一些构建期间的信息并保存到 build/reports/profile 目录下. 并且会以构建时间命名这些文件.
	如果采用了 buildSrc, 那么在 buildSrc/build 下同时也会生成一份日志记录记录.
	