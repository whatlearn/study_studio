## CMakeLists使用方法

[CMake官方文档](https://cmake.org/cmake/help/v3.7/manual/cmake-commands.7.html)

##### 1. 确定cmake编译的最小版本

``` cmake
#为项目设置最低要求的 cmake 版本
cmake_minimum_required(VERSION major.minor[.patch[.tweak]]
                       [FATAL_ERROR])
                       
cmake_minimum_required(VERSION 3.7)
```

##### 2. 设置项目名称

``` cmake
#为整个项目设置名称、版本和启用语言
project(<PROJECT-NAME> [LANGUAGES] [<language-name>...])
project(<PROJECT-NAME>
        [VERSION <major>[.<minor>[.<patch>[.<tweak>]]]]
        [LANGUAGES <language-name>...])
        
project(VSSafety VERSION 0.0.1 LANGUAGES "CXX“)
```

##### 3. 确定头文件引用目录

``` cmake
#将包含目录添加到构建的项目中
include_directories([AFTER|BEFORE] [SYSTEM] dir1 [dir2 ...])

include_directories(SYSTEM "include" "../include")
```

##### 4. 确定引用链接库目录

``` cmake
#指定链接器将在该目录下查找库
link_directories(directory1 directory2 ...)

link_directories("../lib")
```

##### 5. 确定引用链接库名

``` cmake
#给目标文件指定链接或其依赖项时要使用的库或标志
#target目标文件必须已通过命令在当前目录中创建
target_link_libraries(<target>
                      <PRIVATE|PUBLIC|INTERFACE> <item>...
                     [<PRIVATE|PUBLIC|INTERFACE> <item>...]...)
                     
add_library(VSSsfety SHAERD ${SRC_LIST})
add_executable(VSSafetyExe main.cpp)
target_link_libraries(VSSafetyExe  VSSafety
        libsqlite3.so.0.8.6
        pthread)
```

##### 6. 引用静态链接库的方法

``` cmake
#添加需要链接的库文件目录-注意这里是全路径
#指定以后在当前目录或下面通过命令创建的任何目标时要使用的链接库或标志
link_libraries([item1 [item2 [...]]]
               [[debug|optimized|general] <item>] ...)
               
link_libraries("/usr/local/lib/libssl.so")
add_library(VSSsfety SHAERD ${SRC_LIST})
add_executable(VSSafetyExe main.cpp)
```

##### 7. 查找目录中的所有源文件

``` cmake
#查找directory目录中的所有源文件 保存到variable变量中
#不能迭代遍历子目录下的源文件，需要多次使用
#automatic（au） search（x） source directory 
aux_source_directory(<dir> <variable>)

aux_source_directory(src SRC_LIST)
aux_source_directory(src/gb35114 SRC_LIST)
```

##### 8. 巧妙使用Marco宏

``` cmake
#嵌套使用宏 增加宏的选项
set(CMAKE_CXX_FLAGS "-std=c++11 ${CMAKE_CXX_FLAGS}")
```

##### 9. 增加编译选项

``` cmake
add_defin
```



##### 11. 打印输出消息

``` cmake
#输出cmake过程中消息
message([<mode>] "message to display" ...)

message(STATUS ${PROJECT_SOURCE_DIR})
```

