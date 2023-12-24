# android studio

slug: android_studio
status: Published
tags: 开发工具
summary: 使用教程
type: Post

[[toc]]

## 搜索中文

```
搜索idea里的中文：匹配中文字符的正则表达式： [\u4e00-\u9fa5]
```

## 运行 main 方法

```
高版本需修改.idea - gradle.xml
GradleProjectSettings 内添加<option name="delegatedBuild" value="false" />

1. new scratch file - java （ctrl+alt+shift+insert ）
2. 右键 - Run Scratch.main()

```

## android studio 设置代理

打开 Android Studio，通过 File =》 Setting =》Appearance & Behavior =》System Setting =》 Http Proxy 打开 Http Proxy 配置页面

http 、端口 1081，点击 check connection 即可

## 功能配置

profiler 性能分析[https://www.jianshu.com/p/b035e2a11dd8](https://www.jianshu.com/p/b035e2a11dd8)

Network Profiler 检查网络流量

[https://developer.android.com/studio/profile/network-profiler?hl=zh-CN](https://developer.android.com/studio/profile/network-profiler?hl=zh-CN)

Android studio 美化

[https://meedamian.com/post/deuglifying-android-studio/?hi](https://meedamian.com/post/deuglifying-android-studio/?hi)

## studio 彻底删除 svn 中的项目

```
打开我们的工程目录，定位到.idea目录下，

找到vcs.xml使用记事本打开，

将VCS=“svn”改    =“”即可

然后，彻底清理项目中的 .svn 文件：

然后我们再使用android studio工具栏中得VCS工具即可重新share到subversion了。
```

## studio 快捷键(win)

```
收起/展开代码块  ctrl + 减号
横屏和竖屏切换 o
unitTest：ctrl +shift +f10
隐藏所有除了代码以外的窗口 ctrl +shfit +f12

查看类和接口被哪些子类实现的快捷键

如果你使用的是Android Studio中默认的快捷键方案的话，我们通过查看
“File”->”settings” ->”keymap” ->在快速搜索栏中输入“imp”
可以看出快捷键是 Ctrl+alt +B 或者同时按住ctrl +alt +鼠标左键

遍历集合：对象.for ,对象.fori ,.forr 反向,  数字.for

判空： 对象.null  , 非空： 对象.nn

if: 任何判断的语句.if

分屏：双击shift 输入split ，选择split vertically

ctrl +alt +t  ：快速加入try catch

inn --- 插入判空
fori  插入循环
ctrl + e  查找最近打开的文件
alt + enter  插入构造函数
输入toast ：选择create a new 。。。 即可

快速生成点击事件
android:onClick="click"/>   选择click 按anlt + enter

alt+s :在javabean中按下，复制json字段进去，可自动创建。

ctrl + alt + home 快速打开相关联的文件

alt +f1 打开当前文件所在文件夹

psvm：快速插入main方法
sout：快速输入打印方法

---

Alt+回车 导入包,自动修正
Ctrl+N   查找类
Ctrl+Shift+N 查找文件
Ctrl+Alt+L  格式化代码
Ctrl+Alt+O 优化导入的类和包
Alt+Insert 生成代码(如get,set方法,构造函数等)
Ctrl+E或者Alt+Shift+C  最近更改的代码
Ctrl+R 替换文本
Ctrl+F 查找文本
Ctrl+Shift+Space 自动补全代码
Ctrl+空格 代码提示
Ctrl+Alt+Space 类名或接口名提示
Ctrl+P 方法参数提示
Ctrl+Shift+Alt+N 查找类中的方法或变量
Alt+Shift+C 对比最近修改的代码

Shift+F6  重构-重命名
Ctrl+Shift+先上键
Ctrl+X 删除行
Ctrl+D 复制行
Ctrl+/ 或 Ctrl+Shift+/  注释（// 或者 ）
Ctrl+J  自动代码
Ctrl+E 最近打开的文件
Ctrl+H 显示类结构图
Ctrl+Q 显示注释文档
Alt+F1 查找代码所在位置
Alt+1 快速打开或隐藏工程面板
Ctrl+Alt+ left/right 返回至上次浏览的位置
Alt+ left/right 切换代码视图
Alt+ Up/Down 在方法间快速移动定位
Ctrl+Shift+Up/Down 代码向上/下移动。
F2 或Shift+F2 高亮错误或警告快速定位

代码标签输入完成后，按Tab，生成代码。
选中文本，按Ctrl+Shift+F7 ，高亮显示所有该文本，按Esc高亮消失。
Ctrl+W 选中代码，连续按会有其他效果
选中文本，按Alt+F3 ，逐个往下查找相同文本，并高亮显示。
Ctrl+Up/Down 光标跳转到第一行或最后一行下
Ctrl+B 快速打开光标处的类或方法

1.Ctrl＋E，可以显示最近编辑的文件列表
2.Shift＋Click可以关闭文件
3.Ctrl＋[或]可以跳到大括号的开头结尾
4.Ctrl＋Shift＋Backspace可以跳转到上次编辑的地方
5.Ctrl＋F12，可以显示当前文件的结构
6.Ctrl＋F7可以查询当前元素在当前文件中的引用，然后按F3可以选择
7.Ctrl＋N，可以快速打开类
8.Ctrl＋Shift＋N，可以快速打开文件
9.Alt＋Q可以看到当前方法的声明
10.Ctrl＋W可以选择单词继而语句继而行继而函数
11.Alt＋F1可以将正在编辑的元素在各个面板中定位
12.Ctrl＋P，可以显示参数信息
13.Ctrl＋Shift＋Insert可以选择剪贴板内容并插入
14.Alt＋Insert可以生成构造器/Getter/Setter等
15.Ctrl＋Alt＋V 可以引入变量。例如把括号内的SQL赋成一个变量
16.Ctrl＋Alt＋T可以把代码包在一块内，例如try/catch
17.Alt＋Up and Alt＋Down可在方法间快速移动
下面的不是很有用
18.在一些地方按Alt＋Enter可以得到一些Intention Action，例如将”==”改为”equals()”
19.Ctrl＋Shift＋Alt＋N可以快速打开符号
20.Ctrl＋Shift＋Space在很多时候都能够给出Smart提示
21.Alt＋F3可以快速寻找
22.Ctrl＋/和Ctrl＋Shift＋/可以注释代码
23.Ctrl＋Alt＋B可以跳转到抽象方法的实现
24.Ctrl＋O可以选择父类的方法进行重写
25.Ctrl＋Q可以看JavaDoc
26.Ctrl＋Alt＋Space是类名自动完成
27.快速打开类/文件/符号时，可以使用通配符，也可以使用缩写
28.Live Templates! Ctrl＋J
29.Ctrl＋Shift＋F7可以高亮当前元素在当前文件中的使用
30.Ctrl＋Alt＋Up /Ctrl＋Alt＋Down可以快速跳转搜索结果
31.Ctrl＋Shift＋J可以整合两行
32.Alt＋F8是计算变量值

IntelliJ IDEA使用技巧一览表
在使用 InelliJ IDEA 的过程中，通过查找资料以及一些自己的摸索，发现这个众多 Java 程序员喜欢的 IDE 里有许多值得一提的小窍门，如果能熟练的将它们应用于实际开发过程中，相信它会大大节省你的开发时间，而且随之而来的还会有那么一点点成就感：） Try it ！

1 、写代码时用 Alt-Insert （ Code|Generate… ）可以创建类里面任何字段的 getter 与 setter 方法。

2 、右键点击断点标记（在文本的左边栏里）激活速查菜单，你可以快速设置 enable/disable 断点或者条件它的属性。

3 、 CodeCompletion （代码完成）属性里的一个特殊的变量是，激活 Ctrl-Alt-Space 可以完成在或不在当前文件里的类名。如果类没有引入则 import 标志会自动创建。

4 、使用 Ctrl-Shift-V 快捷键可以将最近使用的剪贴板内容选择插入到文本。使用时系统会弹出一个含有剪贴内容的对话框，从中你可以选择你要粘贴的部分。

5 、利用 CodeCompletion （代码完成）属性可以快速地在代码中完成各种不同地语句，方法是先键入一个类名地前几个字母然后再用 Ctrl-Space 完成全称。如果有多个选项，它们会列在速查列表里。

6 、用 Ctrl-/ 与 Ctrl-Shift-/ 来注释 / 反注释代码行与代码块。

-/ 用单行注释标记（“ //… ”）来注释 / 反注释当前行或者选择地代码块。而 Ctrl-Shift-/ 则可以用块注释标记（“ ”）把所选块包围起来。要反注释一个代码块就在块中任何一个地方按 Ctrl-Shift-/ 即可。

7 、按 Alt-Q （ View|Context Info ）可以不需要移动代码就能查看当前方法地声明。连续按两次会显示当前所编辑的类名。

8 、使用 Refactor|Copy Class… 可以创建一个所选择的类的“副本”。这一点很有用，比如，在你想要创建一个大部分内容都和已存在类相同的类时。

9 、在编辑器里 Ctrl-D 可以复制选择的块或者没有所选块是的当前行。

10 、 Ctrl-W （选择字）在编辑器里的功能是先选择脱字符处的单词，然后选择源代码的扩展区域。举例来说，先选择一个方法名，然后是调用这个方法的表达式，然后是整个语句，然后包容块，等等。

11 、如果你不想让指示事件细节的“亮球”图标在编辑器上显示，通过按 Alt-Enter 组合键打开所有事件列表然后用鼠标点击它就可以把这个事件文本附件的亮球置成非活动状态。

这样以后就不会有指示特殊事件的亮球出现了，但是你仍然可以用 Alt-Enter 快捷键使用它。

12 、在使用 CodeCompletion 时，可以用逗点（ . ）字符，逗号（，）分号（；），空格和其它字符输入弹出列表里的当前高亮部分。选择的名字会随着输入的字符自动输入到编辑器里。

13 、在任何工具窗口里使用 Escape 键都可以把焦点移到编辑器上。

Shift-Escape 不仅可以把焦点移到编辑器上而且还可以隐藏当前（或最后活动的）工具窗口。

F12 键把焦点从编辑器移到最近使用的工具窗口。

14 、在调试程序时查看任何表达式值的一个容易的方法就是在编辑器中选择文本（可以按几次 Ctrl-W 组合键更有效地执行这个操作）然后按 Alt-F8 。

15 、要打开编辑器脱字符处使用的类或者方法 Java 文档的浏览器，就按 Shift-F1 （右键菜单的 External JavaDoc ）。

要使用这个功能须要把加入浏览器的路径，在“ General ”选项中设置（ Options | IDE Settings ），另外还要把创建的 Java 文档加入到工程中（ File | Project Properties ）。

16 、用 Ctrl-F12 （ View | File Structure Popup ）键你可以在当前编辑的文件中快速导航。

这时它会显示当前类的成员列表。选中一个要导航的元素然后按 Enter 键或 F4 键。要轻松地定位到列表中的一个条目，只需键入它的名字即可。

17 、在代码中把光标置于标记符或者它的检查点上再按 Alt-F7 （右键菜单中的 Find Usages… ）会很快地查找到在整个工程中使用地某一个类、方法或者变量的位置。

18 、按 Ctrl-N （ Go to | Class… ）再键入类的名字可以快速地在编辑器里打开任何一个类。从显示出来的下拉列表里选择类。
同样的方法你可以通过使用 Ctrl-Shift-N （ Go to | File… ）打开工程中的非 Java 文件。

19 、要导航代码中一些地方使用到的类、方法或者变量的声明，把光标放在查看项上再按 Ctrl-B 即可。也可以通过按 Ctrl 键的同时在查看点上单击鼠标键调转到声明处。

20 、把光标放到查看点上再按 Ctrl-Alt-B 可以导航到一个抽象方法的实现代码。

21 、要看一个所选择的类的继承层次，按 Ctrl-H （ Browse Type Hierarchy ）即可。也可以激活编辑器中的继承关系视图查看当前编辑类的继承关系。22 、使用 Ctrl-Shift-F7 （ Search | Highlight Usages in File ）可以快速高亮显示当前文件中某一变量的使用地方。按 Escape 清除高亮显示。

23 、用 Alt-F3 （ Search | Incremental Search ）在编辑器中实现快速查查找功能。

在“ Search for: ”提示工具里输入字符，使用箭头键朝前和朝后搜索。按 Escape 退出。

24 、按 Ctrl-J 组合键来执行一些你记不起来的 Live Template 缩写。比如，键“ it ”然后按 Ctrl-J 看看有什么发生。

25 、 Introduce Variable 整合帮助你简化代码中复杂的声明。举个例子，在下面的代码片断里，在代码中选择一个表达式：然后按 Ctrl-Alt-V 。

26 、 Ctrl-Shift-J 快捷键把两行合成一行并把不必要的空格去掉以匹配你的代码格式。

27 、 Ctrl-Shift-Backspace （ Go to | Last Edit Location ）让你调转到代码中所做改变的最后一个地方。

多按几次 Ctrl-Shift-Backspace 查看更深的修改历史。

28 、用 Tools | Reformat Code… 根据你的代码样式参考（查看 Options | IDE Setting | Code Style ）格式化代码。

使用 Tools | Optimize Imports… 可以根据设置（查看 Options | IDE Setting | Code Style | Imports ）自动“优化” imports （清除无用的 imports 等）。

29 、使用 IDEA 的 Live Templates | Live Templates 让你在眨眼间创建许多典型代码。比如，在一个方法里键入

再按 Tab 键看有什么事情发生了。
用 Tab 键在不同的模板域内移动。查看 Options | Live Templates 获取更多的细节。

30 、要查看一个文件中修改的本地历史，激活右键菜单里的 Local VCS | Show History… 。也许你可以导航不同的文件版本，看看它们的不同之处再回滚到以前的任何一个版本吧。

使用同样的右键菜单条目还可以看到一个目录里修改的历史。有了这个特性你就不会丢失任何代码了。

31 、如果要了解主菜单里每一个条目的用途，把鼠标指针移到菜单条目上再应用程序框架的底部的状态栏里就会显示它们的一些简短描述，也许会对你有帮助。

32 、要在编辑器里显示方法间的分隔线，打开 Options | IDE Settings | Editor ，选中“ Show method separators ”检查盒（ checkbox ）。

33 、用 Alt-Up 和 Alt-Down 键可以在编辑器里不同的方法之间快速移动。

34 、用 F2/Shift-F2 键在高亮显示的语法错误间跳转。

用 Ctrl-Alt-Down/Ctrl-Alt-Up 快捷键则可以在编译器错误信息或者查找操作结果间跳转。

35 、通过按 Ctrl-O （ Code | Override Methods… ）可以很容易地重载基本类地方法。

要完成当前类 implements 的（或者抽象基本类的）接口的方法，就使用 Ctrl-I （ Code | Implement Methods… ）。

36 、如果光标置于一个方法调用的括号间，按 Ctrl-P 会显示一个可用参数的列表。

37 、要快速查看编辑器脱字符处使用的类或方法的 Java 文档，按 Ctrl-Q （在弹出菜单的 Show Quick JavaDoc 里）即可。

38 、像 Ctrl-Q （ Show Quick JavaDoc 显示简洁 Java 文档）， Ctrl-P （ Show Parameter Info 显示参数信息）， Ctrl-B （ Go to Declaration 跳转到声明）， Shift-F1 （ External JavaDoc 外部 Java 文档）以及其它一些快捷键不仅可以在编辑器里使用，也可以应用在代码完成右键列表里。

39 、 Ctrl-E （ View | Recent Files ）弹出最近访问的文件右键列表。选中文件按 Enter 键打开。

40 、在 IDEA 中可以很容易地对你的类，方法以及变量进行重命名并在所有使用到它们的地方自动更正。

试一下，把编辑器脱字符置于任何一个变量名字上然后按 Shift-F6 （ Refactor | Rename… ）。在对话框里键入要显示地新名字再按 Enter 。你会浏览到使用这个变量地所有地方然后按“ Do Refactor ”按钮结束重命名操作。

41 、要在任何视图（ Project View 工程视图， Structure View 结构视图或者其它视图）里快速

选择当前编辑地部分（类，文件，方法或者字段），按 Alt-F1 （ View | Select in… ）。

42 、在“ new ”字符后实例化一个已知类型对象时也许你会用到 SmartType 代码完成这个特性。比如，键入

再按 Ctrl-Shift-Space ：

43 、通过使用 SmartType 代码完成，在 IDEA 中创建接口的整个匿名 implementation 也是非常容易的，比如，对于一些 listener （监听器），可以键入

Component component;

component.addMouseListener(

  new

);

然后再按 Ctrl-Shift-Space 看看有什么发生了。

44 、在你需要设置一个已知类型的表达式的值时用 SmartType 代码完成也很有帮助。比如，键入

String s = (

再按 Ctrl-Shift-Space 看看会有什么出现。

45 、在所有视图里都提供了速查功能：在树里只需键入字符就可以快速定位到一个条目。

46 、当你想用代码片断捕捉异常时，在编辑器里选中这个片断，按 Ctrl-Alt-T （ Code | Surround with… ）然后选择“ try/catch ”。它会自动产生代码片断中抛出的所有异常的捕捉块。在 Options | File Templates | Code tab 中你还可以自己定制产生捕捉块的模板。

用列表中的其它项可以包围别的一些结构。

47 、在使用代码完成时，用 Tab 键可以输入弹出列表里的高亮显示部分。

不像用 Enter 键接受输入，这个选中的名字会覆盖掉脱字符右边名字的其它部分。这一点在用一个方法或者变量名替换另一个时特别有用。

48 、在声明一个变量时代码完成特性会给你显示一个建议名。比如，开始键入“ private FileOutputStream ”然后按 Ctrl-Space
分享

```

## 常用插件

```
adb idea  // 控制app重启 清缓存等
android butterknife zelezny  绑定view注解
Android Drawable Importer  添加了一个在不同分辨率导入画板或缩放指定图像到定义分辨率的选项
android material design icon generator    一个设置 material design icon的插件工具
android parcelable code generator 自动实现parcelable序列化
方法：
新建好一个实体类后写好属性：
按下Alt+Insert，选择Palcelable，选择需要的属性，按下OK，搞定~~很简单有木有
copyright

cvs integration
ectranslation  studio中直接翻译

selectchapek for android

```

![https://raw.githubusercontent.com/cvabm/FigureBed/master/img/2018-05-09_190212.png](https://raw.githubusercontent.com/cvabm/FigureBed/master/img/2018-05-09_190212.png)

![https://raw.githubusercontent.com/cvabm/FigureBed/master/img/25457634567.png](https://raw.githubusercontent.com/cvabm/FigureBed/master/img/25457634567.png)

![https://raw.githubusercontent.com/cvabm/FigureBed/master/img/567865435678.gif](https://raw.githubusercontent.com/cvabm/FigureBed/master/img/567865435678.gif)

![https://raw.githubusercontent.com/cvabm/FigureBed/master/img/457543.png](https://raw.githubusercontent.com/cvabm/FigureBed/master/img/457543.png)

[https://github.com/jiang111/awesome-androidstudio-plugins###lifecycle-sorter](https://github.com/jiang111/awesome-androidstudio-plugins###lifecycle-sorter)

## 加载.so

```
第一种

把 .so 文件放/app/libs/armeabi

然后在ｂｕｉｌｄ.gradle 中添加
jniLibs.srcDirs = ['libs']　即可

sourceSets {
main {
jniLibs.srcDir 'src/main/libs'
jni.srcDirs = []
}
}

make project 会自动生成ｊａｒ

第二种：
在main目录下新建jniLibs目录，新建 armeabi，把.so文件放入编译既可

```

## studio 快捷键(mac)

[https://developer.android.com/studio/intro/keyboard-shortcuts](https://developer.android.com/studio/intro/keyboard-shortcuts)

```
提取变量 - option + command + v
```

## 刪除空行

ctrl +f ：^* Alt + x 执行 regex ## 去掉注释 - 右键- remove source code comments

## 直接运行签名 apk

[https://blog.csdn.net/baiaihan/article/details/89352798](https://blog.csdn.net/baiaihan/article/details/89352798)

## 去除 warning 提示

```
解决：application下加入：
tools:ignore="GoogleAppIndexingWarning"
```

## 查看详细 log

```
Run with --stacktrace option to get the stack trace. Run with --info or --debug option to get more log output
在terminal输入： gradlew compileDebug --stacktrace
```

## 启动时选择项目

file - Settings - Appearance & Behavior - System Settings - 取消勾选 Reopen last project on startup 选项

```
恢复avd 和avm窗口

Windows-->Customize Perspective...

删除无用的图片资源：
右键点击“app”项目—>选择Refactor–>选择Remove Unused Resources

选择Command Groups Availability选项，确保Android SDK and AVD Manager是勾选上的，否则在Tool Bar Visibility这栏中的Android SDK and AVD Manager是灰色的，不可选

选择Tool Bar Visibility选项--->勾选Android SDK and AVD Manager

无法打开关联的xml文件解决：
          随便打开一个xml,　修改一下，然后　build---clean  --- 然后ctrl + z 恢复xml 保存

```

## 加快编译

```
写到build.gradle文件中。

android{
...
tasks.whenTaskAdded { task ->
if (task.name.contains("lint")
//如果instant run不生效，把clean这行干掉
||task.name.equals("clean")
//如果项目中有用到aidl则不可以舍弃这个任务
||task.name.contains("Aidl")
//用不到测试的时候就可以先关闭
||task.name.contains("mockableAndroidJar")
||task.name.contains("UnitTest")
||task.name.contains("AndroidTest")
//用不到NDK和JNI的也关闭掉
|| task.name.contains("Ndk")
|| task.name.contains("Jni")
) {
task.enabled = false
}
}
}
```

## 在一个 gradle 的 maven property 里添加多个 URL

```
repositories {
  maven { url "http://maven.springframework.org/release" }
  maven { url "https://maven.fabric.io/public" }
}
```

## 将主 module 变为 library

[https://www.jianshu.com/p/2221986bde9f](https://www.jianshu.com/p/2221986bde9f)

## 查看所有todo

view - tool windows -todo

## 常见问题

### Manifest merger failed with multiple errors, see

![https://raw.githubusercontent.com/cvabm/FigureBed/master/img/v2-1341b22c2689f07a21e03716138d35f1_1440w.jpg](https://raw.githubusercontent.com/cvabm/FigureBed/master/img/v2-1341b22c2689f07a21e03716138d35f1_1440w.jpg)

点这个就能看到详细的错误了

一般都是因为引入的三方包存在相同的 label icon 等名字或者是 sdk 版本不一致

### 需要常量表达式

switch 改成 if

### 找不到 so 包

![https://raw.githubusercontent.com/cvabm/FigureBed/master/img/435765434.png](https://raw.githubusercontent.com/cvabm/FigureBed/master/img/435765434.png)

1、.so 在 jniLibs 下

```
build.gradle文件：
android {
    ...
    defaultConfig {
        ...
        ndk {
            abiFilters "armeabi" //, "x86", "armeabi"  按需设置
        }
    }
}

setting.gradle文件:

android.useDeprecatedNdk=true

```

2、.so 在 libs 下

```
sourceSets {
    main {
        jniLibs.srcDirs = ['libs']
    }
}
```

### lock - open (11: 资源暂时不可用)

```
结果终端提示:无法获得锁 /var/lib/dpkg/lock - open (11: 资源暂时不可用) E: 无法锁定管理目录(/var/lib/dpkg/)，是否有其他进程正占用它？”

解决办法如下：

1.终端输入 ps  -aux ，列出进程,找到含有apt-get的进程，直接sudo kill PID解决。
2.强制解锁--命令:
sudo rm /var/cache/apt/archives/lock
sudo rm /var/lib/dpkg/lock

第二种方法；

sudo rm -rf /var/lib/dpkg/lock

try again.

```

### marketplace plugins are not loaded

```
解决方法时这样的：点击File->settings->Appearance&Behavior->System Settings -> Updates
　　将Use secure connection选项的√去掉！
　　然后重点！重启一下Idea！！！
```

### Preview is unavailable until a successful build

```
Try 3 : Build -> Clean project -> rebuild -> restart Android studio
```

### run 的时候显示 edit configuration 对话框

```
选右侧gradle --  点sync with gradle files图标
```

### Declaring custom ‘clean’ task when using the standard Gradle lifecycle plugins is not allowed

![https://raw.githubusercontent.com/cvabm/FigureBed/master/img/6578654.png](https://raw.githubusercontent.com/cvabm/FigureBed/master/img/6578654.png)

### Could not find com.android.tools.build:gradle

![https://raw.githubusercontent.com/cvabm/FigureBed/master/img/245854.png](https://raw.githubusercontent.com/cvabm/FigureBed/master/img/245854.png)

### AS 导入 NDK 工程提示错误 No such property: sdkHandler for class: com.android.build.gradle.LibraryPlugin

```

接到一个NDK工程需要调试，导入后发现总是提示错误

Error:(37, 1) A problem occurred evaluating project ':libuvccamera'.
> No such property: sdkHandler for class: com.android.build.gradle.LibraryPlugin
百度上各种说法，有说要降低gadle版本，有说要在环境变量里配置ANDROID_NDK的路径，试验了都不行，最后参考别人NDK gradle文件修改如下：
未修改之前：
task ndkBuild(type: Exec, description: 'Compile JNI source via NDK') {
   println('executing ndkBuild')
   def ndkBuildingDir = project.plugins.findPlugin('com.android.library').sdkHandler.getNdkFolder().absolutePath
   def ndkBuildPath = ndkBuildingDir
  if (Os.isFamily(Os.FAMILY_WINDOWS)){
    ndkBuildPath = ndkBuildingDir + '/ndk-build.cmd'

} else {
ndkBuildPath = ndkBuildingDir + '/ndk-build'
}
commandLine ndkBuildPath, '-j8', '-C', file('src/main').absolutePath
}

可修改为

task ndkBuild(type: Exec, description: 'Compile JNI source via NDK') {
println('executing ndkBuild')
def ndkBuildingDir = android.ndkDirectory
if (Os.isFamily(Os.FAMILY_WINDOWS)) {
ndkBuildingDir = "$ndkBuildingDir/ndk-build.cmd"
} else {
ndkBuildingDir = "$ndkBuildingDir/ndk-build"
}
commandLine ndkBuildingDir, '-j8', '-C', file('src/main').absolutePath
}

或者修改为
task ndkBuild(type: Exec, description: 'Compile JNI source via NDK') {
println('executing ndkBuild')

//def ndkBuildingDir = project.plugins.findPlugin('com.android.library').sdkHandler.getNdkFolder().absolutePath
//def ndkBuildPath = ndkBuildingDir
def ndkBuildPath = android.ndkDirectory
if (Os.isFamily(Os.FAMILY_WINDOWS)) {
commandLine "$ndkBuildPath/ndk-build.cmd",
'-C', file('src/main').absolutePath, // Change src/main/jni the relative path to your jni source
'-j', Runtime.runtime.availableProcessors(),
'all',
'NDK_DEBUG=1'
} else {
　　 commandLine "$ndkBuildPath/ndk-build",

'-C', file('src/main').absolutePath, // Change src/main/jni the relative path to your jni source
'-j', Runtime.runtime.availableProcessors(),
'all',
'NDK_DEBUG=1'
}

}

```

### Failed to finalize session : INSTALL_FAILED_INVALID_APKLE:

直接 clean 项目后,然后运行就可以

### Error:(1, 0) Your project path contains non-ASCII characters.

得到的答案是所有的路径都要用英文。就是包括 SDK JDK ADT Eclipse 还是工程存储位置，所有的路径都要改成英文。

### multiple dex files define

jar 包重复

### Gradle 编译禁用 Lint 报错

```
而这些错误又经常是第三方库中的，我们可以跳过这些错误，继续编译。

    1.
android {
    2.
  // your build config
    3.
  defaultConfig { ... }
    4.
  signingConfigs { ... }
    5.
  compileOptions { ... }
    6.
  buildTypes { ... }
    7.
  // This is important, it will run lint checks but won't abort build
    8.
  lintOptions {
    9.
      abortOnError false
    10.
  }
    11.
}

```

### 将 Eclipse 项目导入到 Android studio 中 很多点 9 图出现问题解决方法

```
aaptOptions.cruncherEnabled = false
aaptOptions.useNewCruncher = false
```

### 错误: 编码 GBK 的不可映射字符

```
在module下的gradle中加入：

gradle2.0以下：

tasks.withType(Compile) {
    options.encoding = "UTF-8"
}
2.0以上：

tasks.withType(JavaCompile) {
    options.encoding = "UTF-8"
}
```

### Android Gradle Build Error:Some file crunching failed, see logs for details

```

在gradle文件中加入以下黑体字

android {
    compileSdkVersion 23
    buildToolsVersion "23.0.3"

    aaptOptions {
        cruncherEnabled = false
        useNewCruncher = false
    }
    defaultConfig {
        applicationId "com.xxx.xxx"
        minSdkVersion 15
        targetSdkVersion 22
        versionCode 2
        versionName "1.0.2"
        ndk {
            //设置支持的SO库架构
            abiFilters 'armeabi', 'x86', 'armeabi-v7a', 'x86_64', 'arm64-v8a'
        }
    }
}

出现这个错误的原因是有哪种情况？
1.构建Gradle的时候，Gradle会去检查一下是否修改过文件的后缀名；
2.一般大多数是出现在图片上，.jpg修改成了.png就会出现这个问题；
3.9patch图片也可能出现这个问题。
```

### tools.jar seems to be not in Android Studio

```
第一步：将系统变量JAVA_HOME的值后边加上斜杠“\”
第二步：打开Android Studio，测试是否能够成功打开。如果还是出现下面错误提示，那么进入第三步
第三步：将高版本JDK的lib目录下的tools.jar文件复制到Android Studio根目录下的lib文件夹下即可
```

### 安装 andriod studio 时出现 Internal error. Please report to https://code.google.com/

```
有两种方法的哈

一，在文件中添加  disable.android.first.run=true （我试了这种就好使了哈）

1）进入刚安装的Android Studio目录下的bin目录。找到idea.properties文件，用文本编辑器打开。

2）在idea.properties文件末尾添加一行： disable.android.first.run=true ，然后保存文件。

3）关闭Android Studio后重新启动，便可进入界面。

二，编码问题

无意中怀疑是编码问题，保存idea.properties文件文件时将编码设置为utf-8, 终于启动成功。

经过测试，选择ANSI和utf-8无问题，选择Unicode格式则出现问题。
```

### Android Studio 不能获取远程依赖包的解决方法

1、有没有设置了 offline work

2、jcenter 已关闭，用其他代替

```
  mavenCentral()
  maven { url "https://jitpack.io" }
```

![https://raw.githubusercontent.com/cvabm/FigureBed/master/img/6773567.png](https://raw.githubusercontent.com/cvabm/FigureBed/master/img/6773567.png)

### Android Studio: Plugin with id ‘android-library’ not found

使用最新的 gradle

### java.lang.UnsupportedClassVersionError: com/android/dx/command/Main : Unsupported major.minor ver

```
这个错误也是修改版本的问题

一般情况是最小支持的sdk版本高于当前设备的Android系统版本，这时候需要修改manifest和build.gradle两个地方。
修改源码app目录下的“build.gradle”文件，将其中的minSdkVersion 、targetSdkVersion 修改为跟manifest的安卓API版本一致即可。（切记）
```

### Building gradle project info 一直卡住

替换 gradle-wrapper.properties 文件里的 gradle 版本

### This file is indented with tabs instead of 4 space.html

```
File -> Settings -> Editor -> Code Style -> Java -> Tabs and Indents -> Use tab character
```

### INSTALL_FAILED_CPU_ABI_INCOMPATIBLE

使用真机

### Missing Gradle Project Information. Please check if the IDE successfully synchronized its state with the Gradle Project Model

```
tools > Android > Sync Project with Gradle Files
```

### No cached version of com.android.tools.build-gradle

取消 Offline Work

### In Gradle projects- always use http-schemas

```
布局xml文件中出现Gradle不能自动查找自定义属性：
将自定义属性 http://schemas.android.com/apk/res/com.xxx.xxx 修改为：http://schemas.android.com/apk/res-auto 即可
```

### Android Studio 3.5+ 去掉默认的 androidx 选项

Tools —> SDK Manager –> 删除 Android Q，再新建项目时取消 use androidx.artifacts 即可

## as 同步配置到 github 仓库

### Settings Repository

这是一个 Android Studio 默认自带的插件，它的功能就是实现不同设备同步 Studio 的配置。

![https://upload-images.jianshu.io/upload_images/1797490-7023ba7fd0c5110f.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1143/format/webp](https://upload-images.jianshu.io/upload_images/1797490-7023ba7fd0c5110f.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1143/format/webp)

### 使用

[github](https://www.jianshu.com/p/(https://github.com/develar/settings-repository))

**1.首先在 github 上创建一个仓库，用于存储 Studio 的配置文件** **2.File -> Settings Repository,同步设置**

![https://upload-images.jianshu.io/upload_images/1797490-07a1eb59dfd42883.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/404/format/webp](https://upload-images.jianshu.io/upload_images/1797490-07a1eb59dfd42883.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/404/format/webp)

![https://upload-images.jianshu.io/upload_images/1797490-d9860f53eac3288b.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/662/format/webp](https://upload-images.jianshu.io/upload_images/1797490-d9860f53eac3288b.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/662/format/webp)

> Overwrite Local:远程覆盖本地，用户恢复 Studio 的配置。 Overwrite Remote:覆盖远程，用户同步设置。
> 

**3.点击同步按钮，实现同步** 首次同步时需要输入[Github](https://github.com/)的 Token，而不是用户名和密码。自己在[Github](https://github.com/)个人中心设置中创建一个 Token 就可以。

![https://upload-images.jianshu.io/upload_images/1797490-64fa58344f2b2f32.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/803/format/webp](https://upload-images.jianshu.io/upload_images/1797490-64fa58344f2b2f32.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/803/format/webp)

> 从上传的文件中我们可以看到同步的一些内容。 ### studio 的 logcat 一闪而过问题
> 

把 Show only selected application 下拉框，选择 No filters 就可以看到了

### 预览xml默认为split

![预览xml默认为split](images/预览xml默认为split.png)