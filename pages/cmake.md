# cmake
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


## cmake编译运行
```
编写CMakeLists.txt

cmake_minimum_required(VERSION 3.10)
project(h264_parser)

set(CMAKE_CXX_STANDARD 11)

add_executable(h264_parser test.cpp)

---------------
cmake .
make
--------------------
windows没make，三种方法代替
 安装 MinGW，mingw32-make 
 使用 Visual Studio 自带的 MSBuild.exe
 使用 CMake 生成 Visual Studio 项目，用它打开

```

## g++
`g++ -o test test.cpp` 

- 问题1：报错undefined reference to `WinMain'
    - ,Windows 程序需要有一个名为 WinMain 的入口函数
```
方式1 
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

int simplest_h264_parser(char *url) {
    // 实现解析 H.264 文件的逻辑
    printf("Parsing H.264 file: %s\n", url);
    return 0;
}

int main(int argc, char *argv[]) {
    if (argc < 2) {
        printf("Usage: %s <h264_file>\n", argv[0]);
        return 1;
    }

    simplest_h264_parser(argv[1]);
    return 0;
}
方式2
int WINAPI WinMain(HINSTANCE hInstance, HINSTANCE hPrevInstance, LPSTR lpCmdLine, int nCmdShow) {
    // 程序逻辑
    return 0;
}

```
- ./test "sintel.h264" 或windows：test.exe "sintel.h264"
    
## 资料
- https://github.com/leixiaohua1020/simplest_mediadata_test rtp/h264解析好的例子