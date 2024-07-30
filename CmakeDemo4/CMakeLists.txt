# CMake 最低版本号要求
cmake_minimum_required (VERSION 2.8)

# 项目信息
project (Demo4)

# config.h.in 是一个模板文件，它包含变量占位符，比如 @VAR@。
# config.h 是最终生成的配置头文件，包含替换后的内容。
# PROJECT_SOURCE_DIR 是项目的源代码目录。
# PROJECT_BINARY_DIR 是 CMake 构建目录。
# 加入一个配置头文件，用于处理 CMake 对源码的设置
configure_file (
  "${PROJECT_SOURCE_DIR}/config.h.in"
  "${PROJECT_BINARY_DIR}/config.h"
  )
# 添加构建目录到包含路径，config.h生成在构建文件夹
include_directories("${PROJECT_BINARY_DIR}")

# 是否使用自己的 MathFunctions 库,默认启用，引号中是选项的描述，第一个是选项的名称，在 CMake GUI 或通过命令行，用户可以选择启用或禁用 USE_MYMATH 选项。
option (USE_MYMATH
       "Use provided math implementation" ON)

# 是否加入 MathFunctions 库
# include_directories 添加头文件搜索路径。
# add_subdirectory (math) 告诉 CMake 构建 math 子目录中的内容。
# set (EXTRA_LIBS ${EXTRA_LIBS} MathFunctions) 将 MathFunctions 库添加到链接库列表中。
if (USE_MYMATH)
  include_directories ("${PROJECT_SOURCE_DIR}/math")
  add_subdirectory (math)  
  set (EXTRA_LIBS ${EXTRA_LIBS} MathFunctions)
endif (USE_MYMATH)



# 查找当前目录下的所有源文件
# 并将名称保存到 DIR_SRCS 变量
aux_source_directory(. DIR_SRCS)

# 指定生成目标
add_executable(Demo ${DIR_SRCS})
target_link_libraries (Demo  ${EXTRA_LIBS} m)
