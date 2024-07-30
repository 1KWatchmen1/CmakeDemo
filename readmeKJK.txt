1.CmakeDemo:一个源文件
2.CmakeDemo1:两个源文件，一个头文件，CMakeLists.txt用的是一个个添加源文件
3.CmakeDemo2:两个源文件，一个头文件，CMakeLists.txt文件中设置变量，添加本路径下所有源文件
4.CmakeDemo3:子工程中存放功能函数的头文件和源文件生成连接库，根目录下CmakeLists链接该库，注意根目录下也要存放那个头文件，否则库也无法使用
5.CmakeDemo4:注意要在连接库的时候，连接两个库，一个是自己的数学库m，一个是C++的数学库EXTRA_LIBS，这样根据命令行参数的ON/OFF，进行二选一；还有config.h是生成在构建文件夹中的，所以根目录的CMakelists.txt中一定要包含构建文件夹；还有注意config.h.in的写法（# cmakedefine 是 CMake 的一个预处理器指令，用于在 CMake 配置过程中生成特定的宏定义。这种方式通常用于在 CMake 构建系统中生成配置头文件，使得编译器可以使用这些宏来调整代码行为。）
Cmake构建命令：cmake -DUSE_MYMYTH=ON ..	//如果 USE_MYMATH 选项被启用，config.h 文件中将包含 #define USE_MYMATH，否则该宏定义将不会出现在 config.h 中。

