# NDK开发 (生成三方库)

### 1.新建项目

![image-20251021153156790](C:\Users\kejm\AppData\Roaming\Typora\typora-user-images\image-20251021153156790.png)

![image-20251021153235180](C:\Users\kejm\AppData\Roaming\Typora\typora-user-images\image-20251021153235180.png)

##### 一定要使用 4.1.0！ (尝试了使用5.0.0，调试多次无法生成正确的动态库，故使用4.1.0)

### 2.配置

##### 打开build-profile.json5

![image-20251021153439428](C:\Users\kejm\AppData\Roaming\Typora\typora-user-images\image-20251021153439428.png)

##### 在"externalNativeOptions": 添加 ：

```
"abiFilters": ["arm64-v8a", "x86_64"],
```

### 3.添加代码

##### 在cpp目录下放置要生成的代码目录，可以将头文件放在一起或者新建一个include目录放置在其中

![image-20251021153805018](C:\Users\kejm\AppData\Roaming\Typora\typora-user-images\image-20251021153805018.png)

### 4.修改CMakeLists.txt

```
# the minimum version of CMake.
cmake_minimum_required(VERSION 3.5.0)
project(lddf_02)

set(NATIVERENDER_ROOT_PATH ${CMAKE_CURRENT_SOURCE_DIR})



# 添加头文件.h目录，包括cpp，cpp/include，告诉cmake去这里找到代码引入的头文件
include_directories(${NATIVERENDER_ROOT_PATH}
                    ${NATIVERENDER_ROOT_PATH}/include
                    ${NATIVERENDER_ROOT_PATH}/lddf_src)


# 源文件
file(GLOB lddfsrc_SOURCES "lddf_src/*.c")

# 编译 lddf_src 动态库
add_library(lddf_src SHARED ${lddfsrc_SOURCES})


```

### 5.生成动态链接库

![image-20251021154139693](C:\Users\kejm\AppData\Roaming\Typora\typora-user-images\image-20251021154139693.png)

##### 点击构建HAP

![image-20251021154229757](C:\Users\kejm\AppData\Roaming\Typora\typora-user-images\image-20251021154229757.png)

`build/default/intermediates/cmake/default/obj/x86_64/liblddf_src.so`  

##### 为生成的动态链接库

### 6.将动态链接库放置其他项目

在其他项目中新建一个文件`thrid_party`,以及子目录`your_lib`

子目录中包含`include` 和 `libs`

![image-20251021154719695](C:\Users\kejm\AppData\Roaming\Typora\typora-user-images\image-20251021154719695.png)

##### include要包含头文件，libs中包含运行环境(真机为arm64-v8a 本地模拟器为 x86_64), 其中包含要引用的三方库

##### 更改CMakeList

```
# the minimum version of CMake.
cmake_minimum_required(VERSION 3.5.0)
project(Use_liblddf)

set(NATIVERENDER_ROOT_PATH ${CMAKE_CURRENT_SOURCE_DIR})

if(DEFINED PACKAGE_FIND_FILE)
    include(${PACKAGE_FIND_FILE})
endif()

# 包含头文件
include_directories(${NATIVERENDER_ROOT_PATH}
                    ${NATIVERENDER_ROOT_PATH}/include
                    ${NATIVERENDER_ROOT_PATH}/thrid_party/lddf/include)

add_library(entry SHARED napi_init.cpp)

target_link_libraries(entry PUBLIC libace_napi.z.so)

# 链接三方库
target_link_libraries(entry PUBLIC ${NATIVERENDER_ROOT_PATH}/thrid_party/lddf/libs/${OHOS_ARCH}/liblddf_src.so)
```

##### 即可运行