# c基础

slug: c
status: Published
tags: java
summary: c语言
type: Post

## 一些教程

makefile

## makefile 中一条语句这样： .c.o： gcc -c -o $*.o $<

```
.c.o:
这句话的意思就是 %.o : %.c
也就是说，所有的.o文件，依赖于对应的.c文件
比如有三个a.c b.c c.c
那么就会有 a.o b.o c.o
a.o : a.c
b.o : b.c
c.o : c.c
这是makefile依赖的一种简写方法。makefile的依赖关系有很多种写法。这是其中一种。
```

## 十进制-二进制

```
要把一个十进制数转换为二进制数，可以使用以下步骤：
将十进制数除以 2，得到商和余数。
把余数记录下来，然后把商作为新的十进制数重复第一步，直到商为 0。
把记录的余数倒序排列起来，就是这个十进制数对应的二进制数。
例如，将十进制数 19 转换为二进制数：
19 ÷ 2 = 9 余 19 ÷ 2 = 4 余 14 ÷ 2 = 2 余 02 ÷ 2 = 1 余 01 ÷ 2 = 0 余 1
所以 19 的二进制数为 10011。
```

## 常用工具

CodeBlocks - 下载带 mingw 的安装文件，100 多 M 大小

vscode -

clion -

cfree -

devc++ -

## c 使用

- 编译过程
    - `gcc -E main.c -o main.i` 预处理:对代码宏展开
    - `gcc -S main.i -o main.s` 编译 ->汇编
    - `gcc -c main.s -o main.o` 汇编 ->二进制
    - `gcc main.o -o hello` 链接，成为可执行文件
- `gcc` linux 生成.out windows 为.exe
- `puts "hello"` 不带格式打印
- `printf("Name: %s\n", name);` %s 输入字符串、%d 整数、%f 浮点数、%c 字符
    - 返回值为字符数量
- `scanf("%d", &num);` 从标准输入读取
- `std::cout << "hello" <<std::endl;`
- `&str`str 内存地址
- `abort();` // 调用 abort()函数，人为引发 SIGABRT 信号
- `~ResourceHolder(){ 释放资源 }` 析构函数，只能有一个，释放资源的作用
- `__LINE__`
    - 当前行号,预定义宏，不用导入直接用
    - `__FILE__`文件名
    - `__DATE__`编译日期
    - `_WIN64` 表示当前为 64 位系统
- `virtual 返回类型 函数名(参数列表) = 0;` 纯虚函数,无实现，派生类必须实现该函数
- `volatile` 当一个变量被多个线程同时访问时，使用 volatile 可以确保对该变量的修改对其他线程是可见的
- 操作符
    - `&x`表示取变量 x 的地址
    - ``解引用操作符，获取指针指向的对象的值
    - `>`用于访问指针指向的对象的成员
    - `sizeof()` 获取对变量或类型的占字节数
    - `typedef int Age` 将 int 类型取个别名为 Age
- 指针
    - `int * p = &num` 指针 p 记录 num 的地址
    - `sizeof(int*)` 获取指针占位，32 位 4 字节，64 位 8 字节
    - `int * a`空指针指向编号为 0 的地址，不能操作
    - `int *pointer; *pointer = 42;`// 野指针：未初始化的指针，试图给未初始化的指针赋值
    - `int& r = i` 引用变量，r 和 i 引用同一块内存空间，相当于同一个变量不同名称
- 其他
    - `a << 2` 左移，相当于`a * 2`
    - `a >> 2` 右移，相当于 `a / 2`
    - `0b1011` 0b 开头的表示为二进制数
    - `0x` 0x 开头为十六进制
- ip 地址和网络地址 IP 地址用于标识和寻址网络中的具体设备，而网络地址则表示划分网络的标识符。IP 地址是设备的独特标识，而网络地址是为了确定特定网络而划分的标识。
- 掩码

```
我们希望将该二进制数的第3位（从右到左）设置为0，其他位保持不变。我们可以创建一个掩码，只有第3位设置为0，其他位都是1，然后将掩码与原始数进行逻辑与运算。这将导致第3位被强制设置为0，而其他位保持不变。
  // 原始二进制数
       int binary = 0b10110101;
       // 控制特定位的掩码
       int mask = ~(1 << 2);  // 第3位 (从右到左) 置零
       // 应用掩码
       int result = binary & mask;
       System.out.println("Result: " + Integer.toBinaryString(result));

```

- `函数模板`
- 两个值交换
    
    ```
    加减法交换
     a = a + b;
      b = a - b;
      a = a - b;
    
    异或运算交换
      a = a ^ b;
      b = a ^ b;
      a = a ^ b;
    ```
    

a = a ^ b;：将变量 a 和 b 的值进行异或操作，并将结果赋给 a。异或操作的特性是，对于同一个位，如果两个操作数相应位上的数值相同，则该位结果为 0；如果两个操作数相应位上的数值不同，则该位结果为 1。因此，通过异或操作，a 中存储了 a 和 b 值的异或结果。

b = a ^ b;：将变量 a 和上一步中得到的 a ^ b 进行异或操作，并将结果赋给 b。这个步骤实际上是在将异或结果与原始的 b 进行异或操作，即 a ^ b ^ b，由于异或操作满足交换律和结合律，所以结果是 a ^ 0，即 a 的值。因此，现在 b 中存储了原始的 a 的值。

a = a ^ b;：将上一步中得到的 b（原始的 a 的值）和现在的 a 进行异或操作，并将结果赋给 a。这一步实际上是将 a ^ b ^ a 进行异或操作，最终结果是 b ^ 0，即 b 的值。因此，现在 a 中存储了原始的 b 的值。

void swap(int *p1, int* p2) { *p1 =* p1 ^ *p2;* p2 = *p1 ^* p2; *p1 =* p1 ^ *p2; }

```

```c
// 函数模板
template <typename T>
T getMax(T a, T b) {
  return (a > b) ? a : b;
}
```

- union、struct、class
    - 结构体适合用于表示有不同数据类型的组合对象，每个成员独立存储和访问。
    - 联合适合用于在同一内存位置存储不同类型的数据，各成员共享存储空间。
    - 类是一种更高级的数据结构，可以封装数据和行为，提供更丰富的功能。

### 笔记

C:Files2022.2.5++.exe

- 找到 cmake.exe 设为环境变量
- cmake –build cmake-build-debug –target untitled -j 22

### vscode使用
- 新建文件main.cpp
```
#include <bits/stdc++.h>
using namespace std;
signed main(){
    cout << "hello" << endl;
}
```
- vscode默认命令行位powershell ，有问题,需改为cmd;
    - 点击vscode命令行右边+ 下拉菜单改为cmd
- 执行 g++ main.cpp a.exe
`#define int int64_t` 定义int为64位整数

### 开源库
- https://github.com/mstorsjo/fdk-aac 开源AAC编码器里音质最好的
- https://www.antisip.com/download/exosip2/ 
- https://opus-codec.org/release/stable/2019/04/12/libopus-1_3_1.html
- 

https://github.com/ty6815/AvStackDocs/tree/52c1e04511d3c0908b7028c47566debb63202ae9/stream%20protocol/gb28181/%E5%9B%BD%E6%A0%87%E4%BF%A1%E4%BB%A4%E6%8A%93%E5%8C%85%E7%A4%BA%E4%BE%8B

- #pragma once 为了避免同一个文件被include多次
