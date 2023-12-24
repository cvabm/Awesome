# java_decompile

slug: java_decompile
status: Published
tags: java
type: Post

[[toc]]

# 反编译

[mogua](https://mogua.co/)

[http://www.javadecompilers.com/](http://www.javadecompilers.com/)

[https://www.decompiler.com/](https://www.decompiler.com/)

## 调试 smali

1、[Apktool](https://github.com/iBotPeaches/Apktool)

2、Android studio 安装[smaliidea 插件](https://bitbucket.org/JesusFreke/smalidea/downloads/)

File -> Settings -> Plugins - Install plugin from disk

3、Android studio 搜索插件安裝 java2smali

(生成的 smali 代码可直接拷贝使用）

`build - Compile to smali` 没生成可多点几次

4、开始操作：

- `java -jar apktool d test.apk` 反编译
- 进入 test 文件夹，编辑 AndroidManifest.xml，在 Application 标签里面加上 android:debuggable=“true”
- `java -jar apktool b test -o new.apk` 回编译
- `dx-signer.jar` 签名
- android studio 打开 test 文件夹
- Run -> Edit Configurations - Remote
- 手机打开此 app，Studio 点击 Attach debugger to process，即可看到此 app 进程
- 加断点即可 debug

## 签名工具

[https://github.com/dingxiangtech/dx-signer](https://github.com/dingxiangtech/dx-signer)

android 逆向工具集合

[https://github.com/Juude/droidReverse](https://github.com/Juude/droidReverse)

## 其他

[https://github.com/google/android-classyshark](https://github.com/google/android-classyshark)

[https://github.com/skylot/jadx](https://github.com/skylot/jadx)

[https://sourceforge.net/projects/jadx/files/?source=navbar](https://sourceforge.net/projects/jadx/files/?source=navbar)

解压后：bin jadx-gui-bat ，打开即可

## 字节码编辑工具

https://github.com/Col-E/Recaf

## 修改 jar 包代码、字节码

第一种方式（直接替换 class 文件）

```
譬如修改libwebrtc.jar内的HardwareVideoEncoderFactory.class
1、在android studio内新建工程 - 包名必须和libwebrtc.jar一致，为org.webrtc；
2、新建HardwareVideoEncoderFactory.java文件；
3、将HardwareVideoEncoderFactory.class反编译后的代码拷贝到上述.java文件内，
然后按需进行修改；
之后进行build； 即可在app/build/intermediates/javac/debug/classes/org/webrtc/找到编译后的.class
4、改libwebrtc.jar后缀改为.zip解压后，将上述生成的.class文件替换，将目录重新压缩后，再改为.jar即可

注：反编译可用android studio自带

```

第二种方式（javassist） 官网

[http://www.javassist.org/](http://www.javassist.org/)

```
这种方式直接修改.class文件，不用编译

譬如修改libwebrtc.jar内的Camera2Session.class

1、新建工程，将下载好的javassist-3.22.0-GA.jar引入

新建Test.java

package org;
import javassist.ClassPool;
import javassist.CtClass;
import javassist.CtMethod;

public class Test {

    public static void main(String[] args) {
        try {
            ClassPool pool = ClassPool.getDefault();
            pool.insertClassPath("C:/libwebrtc.jar");//加载指定路径下的库。如果此库已被引入项目中，可以省略这一步
            CtClass cc = pool.get("org.webrtc.Camera2Session");//加载指定的类
            CtMethod method = cc.getDeclaredMethod("findCaptureFormat");//取得需要修改的方法

            method.insertAt(340, "if(bestSize.width==320&& bestSize.height ==240){\n" +
                    "                bestSize.height=180;\n" +
                    "            }");

            cc.writeFile("C:/test");//保存到指定位置，执行完这一步后就会在指定目录生成你需要的 class 文件
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}

2、C:/test生成的Camera2Session.class替换原始的即可

注：1、insertAt()的行数是原始.java文件内的行数对应

```

第三种方式（http://set.ee/jbe/）

还未用过、待续

## 反编译.so 文件

使用 IDA_Pro 工具

[https://www.cnblogs.com/whycxb/p/9143896.html](https://www.cnblogs.com/whycxb/p/9143896.html)

## .so 文件查看函数

```jsx
linux
nm -D xxx.so
objdump -tT xxx.so
```