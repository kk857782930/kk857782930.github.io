# 在LINUX上生成可供NDK引用的三方库

### 预置条件

有cmake

````
$ cmake -version
cmake version 3.22.1

CMake suite maintained and supported by Kitware (kitware.com/cmake).
````

下载ohos.toolchain.cmake (文件中有附带)

将ohos.toolchain.cmake 放置在 ~/ 下随意目录下

这里我将它放在~/Work/ohos_cmake 下![image-20251022161102401](C:\Users\kejm\AppData\Roaming\Typora\typora-user-images\image-20251022161102401.png)



### 构建三方库

在代码目录下新建build 目录和CMakeLists.txt 

````
touch CMakeLists.txt
mkdir build 
````

![image-20251022161313021](C:\Users\kejm\AppData\Roaming\Typora\typora-user-images\image-20251022161313021.png)

其中**lddf_src**放置 源文件和头文件 

CMakeLists.txt 如下：

````
# the minimum version of CMake.
cmake_minimum_required(VERSION 3.5.0)
project(lddf)

set(NATIVERENDER_ROOT_PATH ${CMAKE_CURRENT_SOURCE_DIR})



# 添加头文件.h目录，告诉cmake去这里找到代码引入的头文件，lddf_src可以改为你创建的代码目录
include_directories(${NATIVERENDER_ROOT_PATH}
                    ${NATIVERENDER_ROOT_PATH}/include
                    ${NATIVERENDER_ROOT_PATH}/lddf_src)


# 源文件
file(GLOB lddfsrc_SOURCES "lddf_src/*.c")

# 编译 lddf_src 动态库
add_library(lddf_src SHARED ${lddfsrc_SOURCES})

````



执行指令 ：

````
cd build

cmake ..

cmake -DOHOS_STL=c++_shared -DOHOS_ARCH=x86_64 -DOHOS_PLATFORM=OHOS -DCMAKE_TOOLCHAIN_FILE=~/Work/ohos_cmake/ohos.toolchain.cmake ..

# 其中 -DOHOS_ARCH=x86_64 可以改成你想要生成的ABI，如果你想要生成 arm64-v8a 改成 -DOHOS_ARCH=arm64-v8a 即可
# ~/Work/ohos_cmake/ohos.toolchain.cmake 改成你放置ohos.toolchain.cmake的地址

make
````

![image-20251022163728354](C:\Users\kejm\AppData\Roaming\Typora\typora-user-images\image-20251022163728354.png)

生成的liblddf_src.so 即为可用的so



(测试x86_64模拟器可以使用 ，没有测试arm64-v8a)







