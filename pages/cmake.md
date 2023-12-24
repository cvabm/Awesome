# cmake

slug: cmake
status: Published
tags: c
type: Post

`cmake_minimum_required(VERSION 3.22.1)`

`project("learncapp")`

`add_library(${CMAKE_PROJECT_NAME} SHARED` 

`native-lib.cpp)`

`target_link_libraries(${CMAKE_PROJECT_NAME}      android        log)`

```java

android studio直接运行生成debug的.so包
app/build/intermediates/cxx/Debug/414w3855/obj/arm64-v8a/liblearncapp.so

通过gradle assembleRelease生成release包
app/build/intermediates/cxx/RelWithDebInfo/1g5d115f/obj/arm64-v8a/liblearncapp.so

release包会剥离调试信息、启动更多优化，所以生成的包体积小一些

```