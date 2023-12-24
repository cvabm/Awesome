# java_diff

slug: java_diff
status: Published
tags: java
type: Post

[[toc]]

## 实体 entity、JavaBean、Model、POJO、domain 的区别

[https://blog.csdn.net/u011665991/article/details/81201499](https://blog.csdn.net/u011665991/article/details/81201499)

## for 循环与 foreach 的区别

在固定长度或长度不需要计算的时候 for 循环效率高于 foreach. 在不确定长度,或计算长度有性能损耗的时候,用 foreach 比较方便. foreach 的时候会锁定集合中的对象.期间不能修改.

需要循环数组结构的数据时，建议使用普通 for 循环，因为 for 循环采用下标访问，对于数组结构的数据来说，采用下标访问比较好。 需要循环链表结构的数据时，一定不要使用普通 for 循环，这种做法很糟糕，数据量大的时候有可能会导致系统崩溃。

## equals、==、hashCode()区别

```
== 的作用：
　　基本类型：比较的就是值是否相同
　　引用类型：比较的就是地址值是否相同
equals 的作用:
　　引用类型：默认情况下，比较的是地址值。
    但是String重写了equals，所以比较的是变量值是否相同。
注：不过，我们可以根据情况自己重写该方法。一般重写都是自动生成，比较对象的成员变量值是否相同

```

```
equals 与 hashCode

　前提： 谈到hashCode就不得不说equals方法，二者均是Object类里的方法。由于Object类是所有类的基类，所以一切类里都可以重写这两个方法。

原则 1 ： 如果 x.equals(y) 返回 “true”，那么 x 和 y 的 hashCode() 必须相等 ；
原则 2 ： 如果 x.equals(y) 返回 “false”，那么 x 和 y 的 hashCode() 有可能相等，也有可能不等 ；
原则 3 ： 如果 x 和 y 的 hashCode() 不相等，那么 x.equals(y) 一定返回 “false” ；
原则 4 ： 一般来讲，equals 这个方法是给用户调用的，而 hashcode 方法一般用户不会去调用 ；
原则 5 ： 当一个对象类型作为集合对象的元素时，那么这个对象应该拥有自己的equals()和hashCode()设计，而且要遵守前面所说的几个原则。
————————————————
版权声明：本文为CSDN博主「书呆子Rico」的原创文章，遵循 CC 4.0 BY-SA 版权协议，转载请附上原文出处链接及本声明。
原文链接：https://blog.csdn.net/justloveyou_/java/article/details/52464440
```

## Java 中 overload 和 override 的区别

[https://blog.csdn.net/zhouhong1026/article/details/8232350](https://blog.csdn.net/zhouhong1026/article/details/8232350)

## 定时器 alarmmanager 和 timer 的区别

```
在Android上常用的定时器有两种，一种是Java.util.Timer，一种就是系统的AlarmService了。

实验1：使用Java.util.Timer。
在onStart()创创建Timer，每5秒更新一次计数器，并启动。
Java代码

1mTimer = new Timer();
2mTimer.schedule(new TimerTask() {
3 @Override
4 public void run() {
5 ++mCount;
6 mHandler.sendEmptyMessage(0);
7 }
8 }, 5*1000, 5*1000);

当连接USB线进行调试时，会发现一切工作正常，每5秒更新一次界面，即使是按下电源键，仍然会5秒触发一次。
当拔掉USB线，按下电源键关闭屏幕后，过一段时间再打开，发现定时器明显没有继续计数，停留在了关闭电源键时的数字。

实验2：使用AlarmService：
2.1通过AlarmService每个5秒发送一个广播，setRepeating时的类型为AlarmManager.ELAPSED_REALTIME。

Java代码
1AlarmManager am = (AlarmManager)getSystemService(ALARM_SERVICE);
2am.setRepeating(AlarmManager.ELAPSED_REALTIME, firstTime, 5*1000, sender);

拔掉USB线，按下电源键，过一段时间再次打开屏幕，发现定时器没有继续计数。
2.2setRepeating是的类型设置为AlarmManager.ELAPSED_REALTIME_WAKEUP
Java代码

1AlarmManager am = (AlarmManager)getSystemService(ALARM_SERVICE);
2am.setRepeating(AlarmManager.ELAPSED_REALTIME_WAKEUP, firstTime, 5*1000, sender);
拔掉USB线，按下电源键，过一点时间再次打开屏幕，发现定时器一直在计数。
如此看来，使用WAKEUP才能保证自己想要的定时器一直工作，但是肯定会引起耗电量的增加。
```

### ConcurrentHashMap

[https://www.cnblogs.com/zhuawang/p/4779649.html](https://www.cnblogs.com/zhuawang/p/4779649.html)

## HashMap 和 Hashtable 的区别。

HashMap 是 Hashtable 的轻量级实现（非线程安全的实现），他们都完成了 Map 接口，主要区别在于 HashMap 允许空（null）键值（key）,由于非线程安全，效率上可能高于 Hashtable。 HashMap 允许将 null 作为一个 entry 的 key 或者 value，而 Hashtable 不允许。 HashMap 把 Hashtable 的 contains 方法去掉了，改成 containsvalue 和 containsKey。因为 contains 方法容易让人引起误解。 Hashtable 继承自 Dictionary 类，而 HashMap 是 Java1.2 引进的 Map interface 的一个实现。 最大的不同是，Hashtable 的方法是 Synchronize 的，而 HashMap 不是，在多个线程访问 Hashtable 时，不需要自己为它的方法实现同步，而 HashMap 就必须为之提供外同步。

Hashtable 和 HashMap 采用的 hash/rehash 算法都大概一样，所以性能不会有很大的差异。

## sleep() 和 wait() 有什么区别

sleep 是线程类（Thread）的方法，导致此线程暂停执行指定时间，给执行机会给其他线程，但是监控状态依然保持，到时后会自动恢复。调用 sleep 不会释放对象锁。wait 是 Object 类的方法，对此对象调用 wait 方法导致本线程放弃对象锁，进入等待此对象的等待锁定池，只有针对此对象发出 notify 方法（或 notifyAll）后本线程才进入对象锁定池准备获得对象锁进入运行状态。

## break 和 continue 区别

break 停止这个 for 循环

continue 跳出这个 for 循环里的某一次