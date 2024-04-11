#### android使用java8的API需要设置minsdkVersion26以上的问题
也可以用使用以下插件，则不用设置minsdk了
[Java 8+ API desugaring support (Android Gradle Plugin 4.0.0+)](https://developer.android.com/studio/write/java8-support#library-desugaring). The following version helped in my case:

```java
coreLibraryDesugaring 'com.android.tools:desugar_jdk_libs:1.1.5'
```
