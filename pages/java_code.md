# java_code

slug: java_code
status: Published
tags: java
type: Post

## 配置环境变量

```
JAVA_HOME=C:\Program Files\Java\jdk1.8.0_31
PATH=%JAVA_HOME%\bin;
CLASSPATH=.;%JAVA_HOME%\lib\dt.jar;%JAVA_HOME%\lib\tools.jar;
```

## java 简单实现 udp 和 tcp

[https://www.cnblogs.com/liyuhui-Z/p/7794829.html](https://www.cnblogs.com/liyuhui-Z/p/7794829.html)

## collections.singetonList()应用场景

```
     String init[] = { "One", "Two", "Three", "One", "Two", "Three" };

        List list1 = new ArrayList(Arrays.asList(init));

        list1.remove("One");  //只会移除第一个元素
        list1.add("One");
       // list1.removeAll("One");    这样写是不对的，因为removeAll中 需要的是Collection类型的
        List1 value: [Two, Three, One, Two, Three, One]

             用以下方法可移除所有的"One"：
      List list1 = new ArrayList(Arrays.asList(init));
        list1.removeAll(Collections.singleton("One"));
        The SingletonList is :[Two, Three, Two, Three]

singletonList()这个方法主要用于只有一个元素的优化，减少内存分配，无需分配额外的内存，可以从SingletonList内部类看得出来,由于只有一个element,因此可以做到内存分配最小化，相比之下ArrayList的DEFAULT_CAPACITY=10个
```

## Socket 长连接客户端和服务端

```
package com.socket;

import java.io.IOException;
import java.io.InputStreamReader;
import java.io.OutputStreamWriter;
import java.io.PrintWriter;
import java.io.Reader;
import java.net.Socket;
import java.nio.CharBuffer;

/**
 * Socket长连接 客户端
 */
public class Client03 {
    private String host = "127.0.0.1";
    private int port = 5055;

    /**
     * 数据发送线程
     */
    class SendThread implements Runnable {
        private Socket socket;

        public SendThread(Socket socket) {
            this.socket = socket;
        }

        public void run() {
            while (true) {
                try {
                    PrintWriter pw = new PrintWriter(new OutputStreamWriter(
                            socket.getOutputStream()));
                    pw.write("this is client");
                    pw.flush();
                    Thread.sleep(2000);
                } catch (Exception e) {
                    e.printStackTrace();
                }
            }
        }
    }

    /**
     * 数据接收线程
     */
    class ReceiveThread implements Runnable {
        private Socket socket;

        public ReceiveThread(Socket socket) {
            this.socket = socket;
        }

        public void run() {
            while (true) {
                try {
                    Reader reader = new InputStreamReader(
                            socket.getInputStream());
                    CharBuffer charBuffer = CharBuffer.allocate(8192);
                    @SuppressWarnings("unused")
                    int charIndex = -1;
                    while ((charIndex = reader.read(charBuffer)) != -1) {
                        charBuffer.flip();
                        System.out
                                .println("client--> " + charBuffer.toString());
                    }
                } catch (IOException e) {
                    e.printStackTrace();
                }
            }
        }
    }

    private void start() {
        try {
            Socket socket = new Socket(host, port);// 创建Socket
            new Thread(new SendThread(socket)).start();// 启动读线程
            new Thread(new ReceiveThread(socket)).start();// 启动收线程
        } catch (Exception e) {
            e.printStackTrace();
        }
    }

    public static void main(String[] args) {
        new Client03().start();
    }

}

package com.socket;

import java.io.IOException;
import java.io.InputStreamReader;
import java.io.OutputStreamWriter;
import java.io.Reader;
import java.io.Writer;
import java.net.ServerSocket;
import java.net.Socket;
import java.nio.CharBuffer;

/**
 * Socket长连接 服务端
 */
public class Server03 {

    private ServerSocket serverSocket;
    private Socket socket;
    private int port = 5055;

    private void start() throws Exception {
        serverSocket = new ServerSocket(port);
        while (true) {
            socket = serverSocket.accept();
            new Thread(new SocketThread(socket)).start();// 多线程阻塞
        }
    }

    /**
     * 处理socket连接s
     */
    class SocketThread implements Runnable {
        private Socket socket;
        private String temp = "";

        public SocketThread(Socket socket) {
            this.socket = socket;
        }

        @SuppressWarnings("unused")
        public void run() {
            try {
                Reader reader = new InputStreamReader(socket.getInputStream());
                Writer writer = new OutputStreamWriter(socket.getOutputStream());
                CharBuffer charBuffer = CharBuffer.allocate(1024);
                int readIndex = -1;
                while ((readIndex = reader.read(charBuffer)) != -1) {
                    charBuffer.flip();
                    temp += charBuffer.toString();
                    System.out.println("server-->" + temp);
                    writer.write("this is server");
                    writer.flush();

                }
            } catch (IOException e) {
                e.printStackTrace();
            } finally {
                if (socket != null) {
                    if (!socket.isClosed()) {
                        try {
                            socket.close();
                        } catch (IOException e) {
                            e.printStackTrace();
                        }
                    }
                }

            }
        }

    }

    public static void main(String[] args) {
        Server03 s = new Server03();
        try {
            s.start();
        } catch (Exception e) {
            e.printStackTrace();
        }
    }

}

```

## 删除指定文件夹下的所有文件和子文件夹

```

delAllFile("/mnt/sdcard/ftp/");

//删除文件夹
public static void delFolder(String folderPath) {
    try {
        delAllFile(folderPath); //删除完里面所有内容
        String filePath = folderPath;
        filePath = filePath.toString();
        java.io.File myFilePath = new java.io.File(filePath);
        myFilePath.delete(); //删除空文件夹
    } catch (Exception e) {
        e.printStackTrace();
    }
}

public static boolean delAllFile(String path) {
    boolean flag = false;
    File file = new File(path);
    if (!file.exists()) {
        return flag;
    }
    if (!file.isDirectory()) {
        return flag;
    }
    String[] tempList = file.list();
    File temp = null;
    for (int i = 0; i < tempList.length; i++) {
        if (path.endsWith(File.separator)) {
            temp = new File(path + tempList[i]);
        } else {
            temp = new File(path + File.separator + tempList[i]);
        }
        if (temp.isFile()) {
            temp.delete();
        }
        if (temp.isDirectory()) {
            delAllFile(path + "/" + tempList[i]);//先删除文件夹里面的文件
            delFolder(path + "/" + tempList[i]);//再删除空文件夹
            flag = true;
        }
    }
    return flag;
}

```

## 排序

```
//冒泡排序

class test

{
int[] arr={1,222,14,6,83,3,576};
for(int x=0;x<arr.length-1;x++){
for(int y=0;y<arr.length-x-1;y++){
if(arr[y]>arr[y+1]){
int temp=arr[y];
arr[y]=arr[y+1];
arr[y+1]=temp;
}

选择排序

for(int x=0;x<arr.length-1;x++){
for(int y=x+1;y<arr.length;y++){
if(arr[x]>arr[y]){//从小到大。
int temp=arr[x];
arr[x]= arr[y];
arr[y]=temp;
}

快速排序：
```

## 取随机数

```

    1. /*
    2. import java.util.Random;
    3. public class test{
    4. public static void main(String[] args){
    5. Random xx=new Random();
    6. int number=xx.nextInt(10);
    7. System.out.println(number);
    8. }
    9. }
    10. */
    11. public class test{
    12. public static void main(String[] args);{
    13. int number=(int)(Math.random()*10);//Math 算数的意思
    14. System.out.println(number);
    15. }
    16. }

Random注意大小写

10到20之间
int max=20;
        int min=10;
        Random random = new Random();

        int s = random.nextInt(max)%(max-min+1) + min;
        System.out.println(s);
```

## 集合去重复

```

package collection;

import java.util.ArrayList;
import java.util.Iterator;

public class Demo {
public static void main(String[] args) {
ArrayList a1 = new ArrayList();
a1.add("hello");
a1.add("hello");
a1.add("world");
a1.add("world");
ArrayList a2 = new ArrayList();
Iterator it = a1.iterator();
while(it.hasNext()){
String s = (String)it.next();
if(!a2.contains(s)){
a2.add(s);
}
}
for(int x =0;x<a2.size();x++){
String ss = (String)a2.get(x);
System.out.println(ss);
}
}
}
```

## 三种遍历集合的方法

```

public class Demo {
public static void main(String[] args) {
List list = new ArrayList();
list.add("hello");
list.add("world");

list.add("java");
//list.set(1,"123");
//System.out.println(list.indexOf("hello"));
//System.out.println(list.get(0));
//System.out.println(list.subList(0,1));
ListIterator lt = list.listIterator();
while(lt.hasNext()){
String s = (String)lt.next();
System.out.println(s);
}
for(int x =0;x<list.size();x++){
String s1 = (String)list.get(x);
System.out.println(s1);
}
Iterator its = list.iterator();
while(its.hasNext()){
String s2 = (String)its.next();
System.out.println(s2);
}
}
}
```

## map 集合遍历的方式

```
//map集合遍历的方式
Map<String,String> map=new HashMap<String, String>();
map.put("1", "a");
map.put("2", "b");
map.put("3", "c");
//方式一:

             Set<String> set = map.keySet();
             for (String s : set) {
                    String ss = map.get(s);
                    System.out.println(s + "--" + ss);

             }
//方式二:

             Set<Map.Entry<String, String>> set = map.entrySet();
                    for(Map.Entry<String, String> m :set){
                           String a = m.getKey();
                           String b = m.getValue();
                           System.out.println(a+"--"+b);

                    }
```

## 数组逆序

```
/*
数组元素逆序 (就是把元素对调)
分析：
A:定义一个数组，并进行静态初始化。
B:思路
把0索引和arr.length-1的数据交换
把1索引和arr.length-2的数据交换
...
只要做到arr.length/2的时候即可。
*/
class ArrayTest3 {
public static void main(String[] args) {
//定义一个数组，并进行静态初始化。
int[] arr = {12,98,50,34,76};
//逆序前
System.out.println("逆序前：");
printArray(arr);
//逆序后
System.out.println("逆序后：");
//reverse(arr);
reverse2(arr);
printArray(arr);
}
/*
需求：数组逆序
两个明确：
返回值类型：void (有人会想到应该返回的是逆序后的数组，但是没必要，因为这两个数组其实是同一个数组)
参数列表：int[] arr
public static void reverse2(int[] arr) {
for(int start=0,end=arr.length-1; start<=end; start++,end--) {
int temp = arr[start];
arr[start] = arr[end];
arr[end] = temp;
}
}
//遍历数组
public static void printArray(int[] arr) {
System.out.print("[");
for(int x=0; x<arr.length; x++) {
if(x == arr.length-1) { //这是最后一个元素
System.out.println(arr[x]+"]");
}else {
System.out.print(arr[x]+", ");
}
}
}

}
```

## 99 乘法表

```
class test{
public static void main(String[] args){
for(int x=1;x<=9;x++){
for(int y=1;y<=x;y++){
System.out.print(y+"*"+x+"="+y*x+"\t");
}System.out.println();
}
}

}
```

## array 和 io 复制

```
package play;

import java.io.BufferedReader;
import java.io.FileReader;
import java.io.IOException;
import java.util.ArrayList;
public class Demo{
public static void main(String[] args) throws IOException {
BufferedReader br = new BufferedReader(new FileReader("a.txt"));
ArrayList<String> al = new ArrayList<String>();
String line = null;
while((line= br.readLine())!=null){
al.add(line);
}br.close();
for(String s :al){
System.out.println(s);
}
}
}

package play;
import java.io.BufferedWriter;
import java.io.FileWriter;
import java.io.IOException;
import java.util.ArrayList;
public class Demo{
public static void main(String[] args) throws IOException {
ArrayList<String> al = new ArrayList<String>();
al.add("hello");
al.add("123");
BufferedWriter bw = new BufferedWriter(new FileWriter("abc.txt"));
for(String s :al){
bw.write(s);
bw.newLine();
bw.flush();
}bw.close();
}
}

```

## 复制文件并改名

```
package practice;

import java.io.BufferedInputStream;
import java.io.BufferedOutputStream;
import java.io.File;
import java.io.FileInputStream;
import java.io.FileOutputStream;
import java.io.FilenameFilter;
import java.io.IOException;

public class Search {
public static void main(String[] args) throws IOException {
File srcFolder =  new File("d:\\copy");
File destFolder = new File("e:\\copy");
//遍历目录内容到FIle数组
File[] fileArray =srcFolder.listFiles(new FilenameFilter(){
public boolean accept(File dir,String name){
return new File(dir,name).isFile()&&name.endsWith(".java");
}
});
//判断目标文件夹是否存在，不存在创建
if(!destFolder.exists()){
destFolder.mkdir();
}
//遍历目录内符合条件的文件
for(File file :fileArray){
String name = file.getName();
File newFile = new File(destFolder,name);
BufferedInputStream bis = new BufferedInputStream(new FileInputStream(file));
BufferedOutputStream bos = new BufferedOutputStream(new FileOutputStream(newFile));
byte[] bys = new byte[1024];
int len = 0;
while((len = bis.read())!=-1){
bos.write(bys,0,len);
bos.flush();
}bos.close();
bis.close();
}
File[] destFileArray = destFolder.listFiles();
for(File file:destFileArray){
String name = file.getName();
String newName = name.replace(".java",".jad");
File newFile = new File(destFolder,newName);
file.renameTo(newFile);
}
}
}

```

## 数组写入文本

```
/*
 * 需求：在ArrayList里面存储了3个字符串元素，请把这三个元素写入文本文件。并在每个元素后面加入换行。
 *
 * 数据源：
 *  ArrayList
 * 目的地：
 *  BufferedWriter
 */
public class ArrayListDemo {
public static void main(String[] args) throws IOException {
ArrayList<String> array = new ArrayList<String>();
array.add("hello");
array.add("world");
array.add("java");
BufferedWriter bw = new BufferedWriter(new FileWriter("array.txt"));
//遍历集合
for(String str : array){
bw.write(str);
bw.newLine();
bw.flush();
}
bw.close();
}

}
```

## 字符流复制文本

```
FileWriter fw = new FileWriter("e:\\hello.txt");

  FileReader fr = new FileReader("a.txt");

  char[] chs = new char[1024];
  int len = 0;
  while((len = fr.read(chs))!=-1){

  fw.write(chs,0,len);
  }fr.close();

  fw.close();
```

## 字节流

```
package practice;

import java.io.FileInputStream;
import java.io.FileOutputStream;
import java.io.IOException;
public class Search {
public static void main(String[] args) throws IOException{
// FileOutputStream fos = new FileOutputStream("aaa.txt");
// FileInputStream fis = new FileInputStream("a.txt");
// int by = 0;
// while((by=fis.read())!=-1){
// fos.write(by);
// }
FileOutputStream fos = new FileOutputStream("aaa.txt");
FileInputStream fis = new FileInputStream("a.txt");
byte[] bys  = new byte[1024];
int len = 0;
while((len = fis.read(bys))!= -1){
fos.write(bys,0,len);
}
}
}
```

## 字节流复制 mp4

```
package play;

import java.io.FileInputStream;
import java.io.FileOutputStream;
import java.io.IOException;
public class Demo{
public static void main(String[] args) throws IOException {
FileInputStream fis = new FileInputStream("java.swf");
FileOutputStream fos = new FileOutputStream("hello world.swf");
byte[] bytes = new byte[1024];
int len = 0;
while((len=fis.read(bytes))!=-1){
fos.write(bytes,0,len);
}
fos.close();
fis.close();
}
}

package play;

import java.io.FileInputStream;
import java.io.FileOutputStream;
import java.io.IOException;
public class Demo{
public static void main(String[] args) throws IOException {
FileInputStream fis = new FileInputStream("java.swf");
FileOutputStream fos = new FileOutputStream("hello.swf");
int b = 0;
while((b=fis.read())!=-1){
fos.write(b);
}
fos.close();
fis.close();
}
}

```

## 数组的（折半查找）二分查找

```
数组的一般查找
    1. class test
    2. {
    3. public static void main(String[] args){
    4. int[] arr={2,4,6,8,3,0,9};
    5. int index=getIndex(arr,0);
    6. System.out.println(index);//index是打印查找出的角标号
    7. }

            1. //定义功能，获取key第一次出现在数组中的位置；
        1.   public static int getIndex(int[] arr,int key){
    8. for(int x=0;x<arr.length;x++){
    9. if(arr[x]==key)
    10. return x;
    11. }return -1;//没有找到角标就返回-1
    12. }
    13. }

    1.
class test
    2.
{
    3.
public static void main(String[] args){
    4.
int[] arr={2,5,6,7,9,34,56,78};
    5.
int index=halfSearch(arr,34);
    6.
System.out.println(index);
    7.
}
    8.
//折半查找：必须是有序的数组
    9.
//定义功能，获取key第一次出现在数组中的位置；
    10.
public static int halfSearch(int[] arr,int key){
    11.
int min,max,mid;
    12.
min =0;
    13.
max=arr.length-1;
    14.
mid=(max+min)/2;
    15.
while(arr[mid]!=key){
    16.
if(key>arr[mid])
    17.
min=mid+1;
    18.
else if(key<arr[mid])
    19.
max=mid-1;
    20.
mid = (max+min)/2;
    21.
}return mid;
    22.
}
    23.
public static int getIndex(int[] arr,int key){
    24.
for(int x=0;x<arr.length;x++){
    25.
if(arr[x]==key)
    26.
return x;
    27.
}return -1;//没有找到角标就返回-1
    28.
}
    29.
}
```

## 数组静态初始化 常见问题

```

    1.
        1. int arr[] =new int[2];
        2. int[] arr =new int[2];
        3. //以上两种方式都一样的效果。
        4. int[] arr = new int[]{1,3,4,7,9};// 用大括号的形式标示出数组中元素的内容。中括号不要写长度
        5. int[] arr = {1,3,4,7,9};//此为上述函数的简化形式

        1. int[] arr = new int[3];
        2. System.out.println(arr[3]);
        3. //操作时，访问到了数组中不存在的角标。运行不正常。
        4. arr = null;
        5. System.out.println(arr[1]);
        6. //空指针异常：当引用没有任何指向值为null的情况，该引用还在操作实体。

        1. //数组的操作；
        2. //获取数组中的元素,通常会用到遍历。 经常用for循环。
        3. int[] arr = new int[3];
        4. int[] arr= {3.4.6.1.9};
        5. //数组中有一个属性可以直接获取数组元素的个数；length
        6. //使用方式：数组名称.length =
        7. System.out.println("length="+arr.length);
        8. for(int x=0; x<arr.length; x++);
        9. System.out.println("arr["+0+"]="+arr[0]+";");// arr[0]=0;

```

## 小数点后保留两位

```
java保留两位小数的方法：
方式一：
四舍五入
double   f   =   111231.5585;
BigDecimal   b   =   new   BigDecimal(f);
double   f1   =   b.setScale(2,   BigDecimal.ROUND_HALF_UP).doubleValue();
保留两位小数
方式二：
java.text.DecimalFormat   df   =new   java.text.DecimalFormat("#.00");
df.format(要格式化的数字);
例：new java.text.DecimalFormat("#.00").format(3.1415926)
#.00 表示两位小数 #.0000四位小数 以此类推...
方式三：
double d = 3.1415926;
String result = String .format("%.2f");
%.2f %. 表示 小数点前任意位数   2 表示两位小数 格式后的结果为f 表示浮点型
```

## string 转为 utf-8

```
str = new String(str.getBytes("gbk"),"utf-8");
```

## 枚举

**用法一：常量**

```
在JDK1.5 之前，我们定义常量都是： public static fianl…. 。现在好了，有了枚举，可以把相关的常量分组到一个枚举类型里，而且枚举提供了比常量更多的方法。

public enum Color {
  RED, GREEN, BLANK, YELLOW
}
```

**用法二：switch**

```
JDK1.6之前的switch语句只支持int,char,enum类型，使用枚举，能让我们的代码可读性更强。

enum Signal {
    GREEN, YELLOW, RED
}
public class TrafficLight {
    Signal color = Signal.RED;
    public void change() {
        switch (color) {
        case RED:
            color = Signal.GREEN;
            break;
        case YELLOW:
            color = Signal.RED;
            break;
        case GREEN:
            color = Signal.YELLOW;
            break;
        }
    }
}

```

**用法三：向枚举中添加新方法**

```

如果打算自定义自己的方法，那么必须在enum实例序列的最后添加一个分号。而且 Java 要求必须先定义 enum 实例。

public enum Color {
    RED("红色", 1), GREEN("绿色", 2), BLANK("白色", 3), YELLO("黄色", 4);
    // 成员变量
    private String name;
    private int index;
    // 构造方法
    private Color(String name, int index) {
        this.name = name;
        this.index = index;
    }
    // 普通方法
    public static String getName(int index) {
        for (Color c : Color.values()) {
            if (c.getIndex() == index) {
                return c.name;
            }
        }
        return null;
    }
    // get set 方法
    public String getName() {
        return name;
    }
    public void setName(String name) {
        this.name = name;
    }
    public int getIndex() {
        return index;
    }
    public void setIndex(int index) {
        this.index = index;
    }
}

```

**用法四：覆盖枚举的方法**

```
下面给出一个toString()方法覆盖的例子。

public enum Color {
    RED("红色", 1), GREEN("绿色", 2), BLANK("白色", 3), YELLO("黄色", 4);
    // 成员变量
    private String name;
    private int index;
    // 构造方法
    private Color(String name, int index) {
        this.name = name;
        this.index = index;
    }
    //覆盖方法
    @Override
    public String toString() {
        return this.index+"_"+this.name;
    }
}

```

**用法五：实现接口**

```
所有的枚举都继承自java.lang.Enum类。由于Java 不支持多继承，所以枚举对象不能再继承其他类。

public interface Behaviour {
    void print();
    String getInfo();
}
public enum Color implements Behaviour{
    RED("红色", 1), GREEN("绿色", 2), BLANK("白色", 3), YELLO("黄色", 4);
    // 成员变量
    private String name;
    private int index;
    // 构造方法
    private Color(String name, int index) {
        this.name = name;
        this.index = index;
    }
    //接口方法
    @Override
    public String getInfo() {
        return this.name;
    }
    //接口方法
    @Override
    public void print() {
        System.out.println(this.index+":"+this.name);
    }
}

```

**用法六：使用接口组织枚举**

```
public interface Food {
    enum Coffee implements Food{
        BLACK_COFFEE,DECAF_COFFEE,LATTE,CAPPUCCINO
    }
    enum Dessert implements Food{
        FRUIT, CAKE, GELATO
    }
}

```

**用法七：关于枚举集合的使用**

```

java.util.EnumSet和java.util.EnumMap是两个枚举集合。EnumSet保证集合中的元素不重复；EnumMap中的key是enum类型，而value则可以是任意类型。关于这个两个集合的使用就不在这里赘述，可以参考JDK文档。

```

原文[https://zhuanlan.zhihu.com/p/37661900](https://zhuanlan.zhihu.com/p/37661900)

## 反射

```

获取class三种方法:
person p = new Person();
Class c = p.getClass();
Class c1 = Person.class;
Class c2 = Class.forName("Person");

获取带参构造方法并使用
Class c = Person.class;
Constructor o = c.getConstructor(String.class);
 Object obj = o.newInstance("123");

获取无参构造方法并使用
Class c = Person.class;
Constructor o = c.getConstructor();
 Object obj = o.newInstance();

获取私有的构造方法
Constructor o = c.getDeclaredConstructor(String.class);
 o.setAccessible(true);
 Object obj = o.newInstance("123");

```

```
反射得到jar包方法的需要的参数列表：
Class libClazz = dexClassLoader.loadClass("com.hdos.idCardUartDevice.publicSecurityIDCardLib");
// 调用Class的 newInstance()方法，创建Class的对象 dynamic
// Dynamic 是 dex文件中之前的一个接口类
myLib = (MyLib) libClazz.newInstance();
List<String> list = new ArrayList<>();
Method[] methods = libClazz.getMethods();
for (int i = 0; i < methods.length; i++) {
String name = methods[i].getName();
Class<?>[] parameterTypes = methods[i].getParameterTypes();
list.add(name);

}
```

### 反射库：

[https://github.com/jOOQ/jOOR](https://github.com/jOOQ/jOOR)

使用方法： [https://www.jianshu.com/p/e327caff92d0](https://www.jianshu.com/p/e327caff92d0)

### 代码实例

**简单用代码演示一下反射的一些操作!**

1.创建一个我们要使用反射操作的类 `TargetObject`：

```
package cn.javaguide;

public class TargetObject {
    private String value;

    public TargetObject() {
        value = "JavaGuide";
    }

    public void publicMethod(String s) {
        System.out.println("I love " + s);
    }

    private void privateMethod() {
        System.out.println("value is " + value);
    }
}
```

2.使用反射操作这个类的方法以及参数

```
package cn.javaguide;

import java.lang.reflect.Field;
import java.lang.reflect.InvocationTargetException;
import java.lang.reflect.Method;

public class Main {
    public static void main(String[] args) throws ClassNotFoundException, NoSuchMethodException, IllegalAccessException, InstantiationException, InvocationTargetException, NoSuchFieldException {
        /**
         * 获取TargetObject类的Class对象并且创建TargetObject类实例
         */
        Class<?> tagetClass = Class.forName("cn.javaguide.TargetObject");
        TargetObject targetObject = (TargetObject) tagetClass.newInstance();
        /**
         * 获取所有类中所有定义的方法
         */
        Method[] methods = tagetClass.getDeclaredMethods();
        for (Method method : methods) {
            System.out.println(method.getName());
        }
        /**
         * 获取指定方法并调用
         */
        Method publicMethod = tagetClass.getDeclaredMethod("publicMethod",
                String.class);

        publicMethod.invoke(targetObject, "JavaGuide");
        /**
         * 获取指定参数并对参数进行修改
         */
        Field field = tagetClass.getDeclaredField("value");
        //为了对类中的参数进行修改我们取消安全检查
        field.setAccessible(true);
        field.set(targetObject, "JavaGuide");
        /**
         * 调用 private 方法
         */
        Method privateMethod = tagetClass.getDeclaredMethod("privateMethod");
        //为了调用private方法我们取消安全检查
        privateMethod.setAccessible(true);
        privateMethod.invoke(targetObject);
    }
}

```

输出内容：

```
publicMethod
privateMethod
I love JavaGuide
value is JavaGuide
```

### 反射机制优缺点

- **优点：** 运行期类型的判断，动态加载类，提高代码灵活度。
- **缺点：** 1,性能瓶颈：反射相当于一系列解释操作，通知 JVM 要做的事情，性能比直接的 java 代码要慢很多。2,安全问题，让我们可以动态操作改变类的属性同时也增加了类的安全隐患。

### 反射的应用场景

**反射是框架设计的灵魂。**

在我们平时的项目开发过程中，基本上很少会直接使用到反射机制，但这不能说明反射机制没有用，实际上有很多设计、开发都与反射机制有关，例如模块化的开发，通过反射去调用对应的字节码；动态代理设计模式也采用了反射机制，还有我们日常使用的 Spring／Hibernate 等框架也大量使用到了反射机制。

举例：

1. 我们在使用 JDBC 连接数据库时使用 `Class.forName()`通过反射加载数据库的驱动程序；
2. Spring 框架的 IOC（动态加载管理 Bean）创建对象以及 AOP（动态代理）功能都和反射有联系；
3. 动态配置实例的属性；
4. ……

**推荐阅读：**

- [Java 反射使用总结](https://zhuanlan.zhihu.com/p/80519709)
- [Reflection：Java 反射机制的应用场景](https://segmentfault.com/a/1190000010162647?utm_source=tuicool&utm_medium=referral)
- [Java 基础之—反射（非常重要）](https://blog.csdn.net/sinat_38259539/article/details/71799078)

## 基础

8 种基础数据类型： 整数：byte short int long，浮点：float double 布尔：boolean 字符：char

String a= “111”，a 在栈，111 在方法区。 堆和栈： 堆区:存储的全部是对象 栈区:栈中只保存基础数据类型的对象和自定义对象的引用(不是对象) 方法区:包含所有的 class 和 static 变量

equalsIgnoreCase(): “A”.equalsIgnoreCase(“a”) 为 true 忽略大小写比较

数据类型转换： byte[] getBytes() char[] toCharArray() static String copyValueOf(char[] chs) static String valueOf(char[] chs) static String valueOf(int i) String toLowerCase() String toUpperCase() String concat(String str)

compareTo 比较两个数，返回值 int ，=0 两个相等。 判断字符串大小的依据是根据它们在字典中的顺序决定的。

## Java 中判断字符串是否为数字的五种方法

[https://www.iteye.com/blog/javapub-666544](https://www.iteye.com/blog/javapub-666544)