# 若忆（RuoYi）

## 概述
若忆（RuoYi）是夕月阁开发的在线或离线的代码测试的核心运行模块，提供代码自动编译，自动测试，并支持根据自定义的脚本自动生成测试数据，可以很好地工作在OJ系统中。

## 主要功能
若忆主要支持以下需求：

*	对多语言支持，至少支持目前常见的编程语言，如 *C* ，*C++* ，*Java* 等。
*	支持对控制台程序自动对代码进行编译连接，然后测试其时间和空间运行性能，并自动导入测试用例，并和输出测试用例进行比较。
*	支持对上交代码的实现性限制，即可以限制不能使用某些库或某些函数，可以限制代码实现的语句数或行数。
*	支持若忆脚本自动测试用例生成，并根据参考源码生成的程序自动获取对应的输出用例，和测试对象进行对比，从而实现 *每次测试的用例都是无法预计的* 。
*	支持整文件编译，也支持部分函数填充，即可以实现代码的一部分。
*	支持SDK编译，即提供开发SDK，并由用户在此SDK基础上开发，然后在此基础上进行对战类项目。

## RuoYi Filter 代码检查模块
代码检查模块主要检查用户提交的代码的合法性，比如是否使用了不安全的系统函数，是否会对系统进行破坏，以及是否不符合题目的限制要求（对函数、库、实现语句数之类的限制）等。

## RuoYi Builder 代码编译模块
代码编译模块主要就是根据用户提交的代码和指定的语言生成目标可执行程序。使用语法应该如下。

	ruoyi_builder (-s source)[-m mode][(-l language)][(-d destName)]

* _source_ : 源代码文件名，支持相对路径。如果路径中存在空白字符或特殊字符的话需要用双引号引起来。
* _mode_ : 编译模式，主要有以下三种编译模式：
	* _whole_ 全编译模式，即提供的代码是完整的源程序，对其直接编译成可执行的控制台程序。
	* _fragment_ 部分编译模式，需要用 -f fragFile 参数指定一个或多个主体文件，输入的文件将根据一定的规则填入到主体文件中进行编译并生成可执行的控制台程序。
	* _sdk_ 自环境模式，会根据自身提供的一些环境参数编译程序，并按照要求生成目标可识别的代码。这部分的内容到后面有待于进一步补充。
* _language_ : 编译器语言，如果不指定这个参数，就根据提交源程序的扩展名来选择编译器。
* _destName_ : 生成的可执行程序的位置，如果不指定这个参数，则代表在同一个目录下生成和源文件同名的目标文件。

## RuoYi Judger 结果审查模块
结果审查模块则是利用生成号的可执行程序，利用生成好的测试用例作为输入，并和生成好的测试用例进行输出比较，同时比较起时间和空间上是否满足要求，并给出评分结果。

## RuoYi Script 测试脚本模块
测试脚本是一种特殊的测试数据生成脚本，在执行结果审查之前可以通过测试脚本模块随机生成输入用例和输出用例，用来进行结果比较。
