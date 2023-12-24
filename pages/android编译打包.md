# android编译打包

slug: build
status: Published
tags: android
type: Post

[[toc]]

### 下载依赖包

```jsx
比如下载`implementation 'com.github.jiangdongguo.AndroidUSBCamera:libausbc:3.2.10'`

地址栏输入https://www.jitpack.io/com/github/jiangdongguo/AndroidUSBCamera/libausbc/3.2.10/

会显示
libausbc-3.2.10-sources.jar
libausbc-3.2.10.aar
libausbc-3.2.10.module
libausbc-3.2.10.pom
libausbc-3.2.10.pom.md5
libausbc-3.2.10.pom.sha1

https://www.jitpack.io/com/github/jiangdongguo/AndroidUSBCamera/libausbc/3.2.10/libausbc-3.2.10.aar
```

## 混淆

```
buildTypes {
    release {
        minifyEnabled true
        proguardFiles getDefaultProguardFile('proguard-android.txt'), 'proguard-rules.pro'
    }
}
```

- 默认混淆模板路径 `ANDROID_SDK\tools\proguard\proguard-android.txt`
- 进一步压缩代码 `getDefaultProguardFile("proguard-android-optimize.txt")`
- 自定义的配置 `proguard-rules.pro`
- 如果报错 ，在混淆文件末端加上：`ignorewarnings -keep`

## 使用 keytool 生成密钥文件

`keytool -genkey -alias 【别名】-keyalg 【加密算法】-keystore 【密钥文件名/密钥完整路径】`

`keytool -genkey -alias TestAlias -keyalg RSA -keystore test.jks`

## 查看 shar1

`keytool -v -list -keystore keystore文件路径`

## debug 版本证书（获取 shar1 值)

默认路径：C:.android.keystore

默认密码：android

第一步、打开 Android Studio 的 Terminal 工具

第二步、输入命令：keytool -v -list -keystore keystore 文件路径

第三步、输入 Keystore 密码

即可获取编译的 shar1 值

## 加快编译速度

```
写到build.gradle文件中。
android {
    ...
    tasks.whenTaskAdded {
        task - >
            if (task.name.contains("lint")
                //如果instant run不生效，把clean这行干掉
                || task.name.equals("clean")
                //如果项目中有用到aidl则不可以舍弃这个任务
                || task.name.contains("Aidl")
                //用不到测试的时候就可以先关闭
                || task.name.contains("mockableAndroidJar") || task.name.contains("UnitTest") || task.name.contains("AndroidTest")
                //用不到NDK和JNI的也关闭掉
                || task.name.contains("Ndk") || task.name.contains("Jni")
            ) {
                task.enabled = false
            }
    }
}
```

## gradle设置代理

```
在gradle.properties文件添加
systemProp.http.proxyHost=127.0.0.1
systemProp.http.proxyPort=1080
systemProp.https.proxyHost=127.0.0.1
systemProp.https.proxyPort=1080
```

## gradle 命令

```
./gradlew -v 版本号，首次运行，没有gradle的要下载的哦。
./gradlew clean 删除HelloWord/app目录下的build文件夹
./gradlew build 检查依赖并编译打包
./gradlew assembleDebug 编译并打Debug包
./gradlew assembleRelease 编译并打Release的包
./gradlew installRelease Release模式打包并安装
./gradlew uninstallRelease 卸载Release模式包
```

## 动态加载 so，jar 包

```
import java.lang.reflect.Method;

public class DexLoader {
    public static void loadDex(String dexPath, String dexOutputDir, String optimizedDir, ClassLoader parentClassLoader) {
        DexClassLoader dexClassLoader = new DexClassLoader(dexPath, dexOutputDir, optimizedDir, parentClassLoader);
        try {
            // 加载需要调用的类
            Class<?> loadedClass = dexClassLoader.loadClass("com.example.MyClass");

            // 获取方法
            Method myMethod = loadedClass.getMethod("myMethod", String.class);

            // 创建类实例
            Object instance = loadedClass.newInstance();

            // 调用方法
            String result = (String) myMethod.invoke(instance, "Hello, Reflection!");

            // 输出结果
            System.out.println(result);
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}

String dexPath = "/sdcard/your_dex_file.dex"; // DEX 文件路径
String dexOutputDir = getDir("dex", 0).getAbsolutePath(); // DEX 输出目录
String optimizedDir = getDir("opt", 0).getAbsolutePath(); // 优化后的 DEX 输出目录
ClassLoader parentClassLoader = getClassLoader(); // 父 ClassLoader

//optimizedDir可传null
DexLoader.loadDex(dexPath, dexOutputDir, optimizedDir, parentClassLoader);

```

```
import java.net.URL;
import java.net.URLClassLoader;

public class JarLoader {
    public static void loadJar(String jarPath) {
        try {
            URL jarUrl = new URL("file://" + jarPath);
            URLClassLoader classLoader = new URLClassLoader(new URL[] {jarUrl});

            // 加载需要调用的类
            Class<?> loadedClass = classLoader.loadClass("com.example.MyClass");

            // 创建类实例
            Object instance = loadedClass.newInstance();

            // 调用方法
            // ...

            // 关闭ClassLoader
            classLoader.close();
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```

## 打 jar 包

```
打jar包
在app下添加依赖 compile project(':core')
Jar包位置：build--libs
```

## 打 aar 包

```
位置：build -- outputs -- aar
引用：
project的gradle：
flatDir {
  dirs 'libs'
 }
app的gradle：
compile(name: 'common-debug', ext: 'aar')
```

## 修改 jar 包内容

1、studio 打开 jar 包,复制要修改的.class 文件内容，，新建一个同名文件，拷贝内容进去，然后 rebuild

(注：按需添加缺失的依赖文件，只保证此.java 文件编译正常即可)

2、拷贝编译出的.class 文件，路径例：app/build/intermediates/javac/debug/classes/org/webrtc/DefaultVideoDecoderFactory.class

3、jar 改为 zip 解压，将刚才.class 文件覆盖，重新改为.jar 即可

## android 将 so 打到 jar 包中并运行

[https://blog.csdn.net/s569646547/article/details/51822014](https://blog.csdn.net/s569646547/article/details/51822014)

## 生成.so 文件

[https://www.jianshu.com/p/3494741f0ad1](https://www.jianshu.com/p/3494741f0ad1)

步骤：

1：配置 ndk 路径

1：写一个 java 类，编译生成.class

2：用命令把.class 转编译成.h 文件

3：在 jniutil.c 中我们需要导入上边的.h 文件，然后实现具体的 test 方法。

## ndk 开发

[https://www.cnblogs.com/yejiurui/p/3476565.html](https://www.cnblogs.com/yejiurui/p/3476565.html)

##　封装 sdk

```
1、将 apply plugin: 'com.android.application'修改成apply plugin: 'com.android.library'
2、去掉applicationId "com.mg.axe.helloworld"
3、删除自定义的Application和在AndroidManifest.xml的配置
4、去点入口的Activity，否则在Android Studio接入时会生成两个图标入口
5、在build下的assembleRelease和assembleDebug都可以生成aar包
6、aar解压即可得到jar
7、引入：
repositories{
        flatDir {
            dirs 'libs'
        }
    }

      // implementation(name: 'aar包的名字', ext: 'aar')
  implementation(name: 'game_sdk', ext: 'aar')
```

- 查看apk是否签名 `keytool -list -printcert -jarfile C:\project\release.apk` ## android 多渠道、多版本打包

```
不同包名、不同签名、不同版本号、替换 string、icon 等
1、app/build.gradle 文件的修改，增加：productFlavors
1.1、defaultConfig 注释掉原本的 applicationId，不然会和多渠道内的包名有冲突
1.2、versionCode 和 versionName 也可以配置进 productFlavors 中去，不多说
1.3、buildTypes 暂时就用默认的
1.4、productFlavors 下一般有这几部分组成

2、修改工程的目录
在 app 目录同级增加其他的 Flavors 文件夹，
比如替换 app_name，原本 app 下 values 中 string.xml 的 app_name 注释掉

注： 配置文件里用通配符引用例如： android:authorities="${applicationId}.provider"

例：

gradle.properties：

MYAPP_RELEASE_STORE_FILE=danbing_release.keystore
MYAPP_RELEASE_KEY_ALIAS=my-key-alias
MYAPP_RELEASE_STORE_PASSWORD=tdyg123
MYAPP_RELEASE_KEY_PASSWORD=tdyg123

MYAPP_RELEASE_STORE_FILE2=claireye_release.jks
MYAPP_RELEASE_KEY_ALIAS2=claireye_release

android{}内：

    signingConfigs {
        normalRelease {
            if (project.hasProperty('MYAPP_RELEASE_STORE_FILE')) {
                storeFile file(MYAPP_RELEASE_STORE_FILE)
                storePassword MYAPP_RELEASE_STORE_PASSWORD
                keyAlias MYAPP_RELEASE_KEY_ALIAS
                keyPassword MYAPP_RELEASE_KEY_PASSWORD
            }
        }

        claireyeRelease {
            if (project.hasProperty('MYAPP_RELEASE_STORE_FILE2')) {
                storeFile file(MYAPP_RELEASE_STORE_FILE2)
                storePassword MYAPP_RELEASE_STORE_PASSWORD
                keyAlias MYAPP_RELEASE_KEY_ALIAS2
                keyPassword MYAPP_RELEASE_KEY_PASSWORD
            }
        }
    }

      buildTypes {
    release {
      // 省略其他配置...
        signingConfig null  // 置空
    }

    debug {
      // 省略其他配置...
        signingConfig null // 置空
    }
    }
    productFlavors {
        normal {
            applicationId "com.amplesky.client.cdc"
            versionCode 13
            versionName "1.0.12"
            dimension "implementation"
            buildConfigField 'boolean', 'openvpn3', 'true'
            signingConfig = signingConfigs.normalRelease
            manifestPlaceholders = [
                    VpnfileProvider: "com.amplesky.client.cdc.provider"
            ]
        }

        claireye {
            applicationId "com.amplesky.client.claireye"
            versionCode 13
            versionName "1.0.12"
            dimension "implementation"
            buildConfigField 'boolean', 'openvpn3', 'true'
            signingConfig = signingConfigs.claireyeRelease
            manifestPlaceholders = [
                    VpnfileProvider: "com.amplesky.client.claireye.provider"
            ]

        }

    }

    applicationVariants.all {
        //判断是release还是debug版本
        def buildType = it.buildType.name
        def fileName
        //获取当前时间的"YYYY-MM-dd"格式。
        def createTime = new Date().format("YYYYMMddHHmm", TimeZone.getTimeZone("GMT+08:00"))
        //只对Release包起作用，如果不是Release包则不变更输出路径，否则可能导致AS无法自动安装debug包。
        if (buildType == "release") {
            it.getPackageApplication().outputDirectory = new File(project.rootDir.absolutePath + "/apks")
        }
        def channel = it.productFlavors[0].name
        it.outputs.each {
            //只对Release包起作用，如果不是Release包则不变更名称。
            if (buildType == "release") {
                //我此处的命名规则是：渠道名_项目名_版本名_创建时间_构建类型.apk
                fileName = "danbing_v${defaultConfig.versionName}-${buildType}_${createTime}.apk"
                fileName = "${channel}_danbing_v${defaultConfig.versionName}_${createTime}-${buildType}.apk"
                //将名字打印出来，以便及时查看是否满意。
                println "file name：-----------------${fileName}"
                //重新对apk命名。(适用于Gradle4.0（含）以上版本)如果你Gradle版本是4.0以下版本则将上面的一行代码放开并注释下面的这一行。
                it.outputFileName = fileName
            }
        }
    }
```

## app 安装失败

1：Package couldn’t be install… & provider is already used by

配置文件中的 content provider 设置 authorities 为不相同的

## 编译报错 Invalid keystore format

更换 android studio 的 jdk

## 编译脚本

- 生成证书,拷贝到 app 路径下

```
keytool -genkey -v -keystore test.jks -alias myalias  -storepass 1234 -keypass 1234 -keyalg RSA -validity 14000

14000为天数
```

- 项目根目录新建 build.bat

```
echo  " **************************package start ************************** "
gradle clean&gradle assembleRelease
echo -e "**************************package complete************************** "
```

- gradle.properties 新增内容

```
MYAPP_RELEASE_STORE_PASSWORD=123456
MYAPP_RELEASE_KEY_PASSWORD=123456
MYAPP_RELEASE_STORE_FILE=test.jks
MYAPP_RELEASE_KEY_ALIAS=my-alias
```

- 修改 app/build.gradle

```
    signingConfigs {
        config {
            storeFile file(MYAPP_RELEASE_STORE_FILE)
            storePassword MYAPP_RELEASE_STORE_PASSWORD
            keyAlias MYAPP_RELEASE_KEY_ALIAS
            keyPassword MYAPP_RELEASE_KEY_PASSWORD
        }
    }
    buildTypes {
        release {
            signingConfig signingConfigs.config
            minifyEnabled false
            proguardFiles getDefaultProguardFile('proguard-android.txt'), 'proguard-rules.pro'
        }
    }

    applicationVariants.all {
        //判断是release还是debug版本
        def buildType = it.buildType.name
        def fileName
        //获取当前时间的"YYYY-MM-dd"格式。
        def createTime = new Date().format("YYYYMMddHHmm", TimeZone.getTimeZone("GMT+08:00"))
        //只对Release包起作用，如果不是Release包则不变更输出路径，否则可能导致AS无法自动安装debug包。
        if (buildType == "release") {
            it.getPackageApplication().outputDirectory = new File(project.rootDir.absolutePath + "/apks")
        }
//        def channel = it.productFlavors[0].name
        it.outputs.each {
            //只对Release包起作用，如果不是Release包则不变更名称。
            if (buildType == "release") {
                //我此处的命名规则是：渠道名_项目名_版本名_创建时间_构建类型.apk
                fileName = "appcenter_v${defaultConfig.versionName}_${createTime}-${buildType}.apk"
                //将名字打印出来，以便及时查看是否满意。
                println "file name：-----------------${fileName}"
                //重新对apk命名。(适用于Gradle4.0（含）以上版本)如果你Gradle版本是4.0以下版本则将上面的一行代码放开并注释下面的这一行。
                it.outputFileName = fileName
            }
        }
    }
```

- 执行 build.bat，生成路径为根目录/apks/

## 编译 aar/jar

```jsx
aar: studio新建module - Android Library - 命名mylib - 在mylib目录执行gradle assembleRelease

jar: 编辑mylib内的build.gradle

android{
  task makeJar(type: Copy) {
        //删除存在的
        delete 'build/libs/myjar.jar'
        //设置拷贝的文件
        from('build/intermediates/aar_main_jar/release/')
        //打进jar包后的文件目录
        into('build/libs/')
        //将classes.jar放入build/libs/目录下
        //include ,exclude参数来设置过滤
        include('classes.jar')
        //重命名
        rename ('classes.jar', 'myjar.jar')
    }
    makeJar.dependsOn(build)
}

```