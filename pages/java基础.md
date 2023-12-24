# java基础

slug: java_base
status: Published
tags: java
summary: java基础
type: Post

[[toc]]

- `深拷贝` java 使用 clone 或者序列化 反序列化 执行会生成一个新对象
- `浅拷贝`两个指针 指向同一个地址

## 泛型

**作用**

1、类型的参数化，就是可以把类型像方法的参数那样传递。 2、泛型使编译器可以在编译期间对类型进行检查以提高类型安全，减少运行时由于对象类型不匹配引发的异常。

**常见使用定义**

```
 E — Element，常用在java Collection里，如：List<E>,Iterator<E>,Set<E>
 K,V — Key，Value，代表Map的键值对
 N — Number，数字
 T — Type，类型，如String，Integer等等
```

**泛型类**

```
//定义
class Point<T>{// 此处可以随便写标识符号
    private T x ;
    private T y ;
    public void setX(T x){//作为参数
        this.x = x ;
    }
    public void setY(T y){
        this.y = y ;
    }
    public T getX(){//作为返回值
        return this.x ;
    }
    public T getY(){
        return this.y ;
    }
};
//IntegerPoint使用
Point<Integer> p = new Point<Integer>() ;
p.setX(new Integer(100)) ;
System.out.println(p.getX());

//FloatPoint使用
Point<Float> p = new Point<Float>() ;
p.setX(new Float(100.12f)) ;
System.out.println(p.getX());
```

**多泛型变量定义** 在之前的 T 后增加 U 类型

```
class MorePoint<T,U> {
    private T x;
    private T y;

    private U name;

    public void setX(T x) {
        this.x = x;
    }
    public T getX() {
        return this.x;
    }
    public void setName(U name){
        this.name = name;
    }

    public U getName() {
        return this.name;
    }
}
//使用
MorePoint<Integer,String> morePoint = new MorePoint<Integer, String>();
morePoint.setName("harvic");
Log.d(TAG, "morPont.getName:" + morePoint.getName());
```

## 万物基于 object

类默认继承于 object，所以看不到基本类 File 的继承关系

![https://raw.githubusercontent.com/cvabm/FigureBed/master/img/45645654756.png](https://raw.githubusercontent.com/cvabm/FigureBed/master/img/45645654756.png)

![https://raw.githubusercontent.com/cvabm/FigureBed/master/img/56457567567.png](https://raw.githubusercontent.com/cvabm/FigureBed/master/img/56457567567.png)

![https://raw.githubusercontent.com/cvabm/FigureBed/master/img/34645756.png](https://raw.githubusercontent.com/cvabm/FigureBed/master/img/34645756.png)

## long 除以 long 舍掉小数的问题

```
long a = 123;
long b = 12345;
System.out.println( a *1.0f/ b );
解决方法：把其中一个数转为float即可
```

### AtomicInteger

在 Java 语言中，++i 和 i++操作并不是线程安全的，在使用的时候，不可避免的会用到 synchronized 关键字。 而 AtomicInteger 则通过一种线程安全的加减操作接口。 主要用于在高并发环境下的高效程序处理,来帮助我们简化同步处理.

```
 AtomicInteger atomicInteger = new AtomicInteger(123);
        System.out.println(atomicInteger.addAndGet(1));
输出：124
```

## 查看 JAR 包的 JDK 版本

### 方法 1: 使用 UltraEdit 查看 java class 文件

java 开发过程中经常会有这样的疑问：对于某个依赖 jar，它支持的 jdk 版本是多少？这种问题通过搜索引擎通常很难找到准确答案，下面给出一种方便准确的方法来查看某个依赖 jar 对应的 jdk 版本号：

**step 1.  解压缩依赖 jar**

依赖 jar 被解压缩得到许多 class 文件；

**step 2.  下载安装 UltraEdit 软件**

**step 3.  使用 UltraEdit 打开解压缩的任意一个 class 文件**

示例如下：

![https://upload-images.jianshu.io/upload_images/13578911-7d3a69039c3ad58b.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1200/format/webp](https://upload-images.jianshu.io/upload_images/13578911-7d3a69039c3ad58b.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1200/format/webp)

只看第一行数据，前面 8 个字节 CA FE BA BE 是固定的，之后 4 个字节 00 00 是次版本号，次版本号后面的 4 个字节**00 32  是 jdk 的版本号**，如我这里使用的是 jdk1.6

jdk 版本号对应关系如下：

![https://upload-images.jianshu.io/upload_images/13578911-eae05d912b91f378.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1200/format/webp](https://upload-images.jianshu.io/upload_images/13578911-eae05d912b91f378.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1200/format/webp)

图 1-1.   jdk 版本号对应关系

---

### 方法 2: javap 反编译命令查看 jdk 版本

以依赖 jar oraclle driver （ojdbc6 为例）：

root#  **javap -verbose OracleClob.class**

Classfile /root/Downloads/ojdbc6/oracle/jdbc/OracleClob.class

Last modified Jul 3, 2014; size 401 bytes

MD5 checksum dfe69528ea779ae04c68ca59248a8ab1

Compiled from “OracleClob.java”

public interface oracle.jdbc.OracleClob extends java.sql.Clob

minor version: 0

**major version: 50**

……

通过查看图 1-1，50 对应的 jdk 版本为 jdk1.6。