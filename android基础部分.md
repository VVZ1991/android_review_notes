# android基础部分

## Intent Service
有两个优点。

1. 不用new线程。
2. Service运行完成后内存会自己回首掉

```
IntentService是Service的子类，是一个异步的，会自动停止的Service，很好的解决了Service里面耗时任务执行完成后，忘记关闭。内存泄漏的问题
```


## Context区别
* Activity和Service一级Application的Context是不一样的，Activity集成自ContenxtThemeWraper。其他的继承自ContextWarpper。
* 每一个Activity和Service以及Application的Context的Context都是一个新的ContextImpl对象
* getApplication()是用来获取Application势力的，但是这个方法只有在Activity的Service中才能调用的到。那么也许在绝大多数情况下。我们都是在Activity或Service中使用Application的。但是如果在一些其他的场景。比如BoardCastReceiver中也想获取Application的实习，这是就可以借助getApplicationContext方法，getApplicationContext比getApplication()方法的作用域会更广一些，任何一个Context实例，只要调用getApplicationContext()都可以拿到我们的Application对象。
* Activity在创建的时候回new一个ContenxtImpl对象并在attacch方法中关联到他，Applicaiton和Service也差不多。ContextWrapper的方法内部都是转调ContextImpl的方法。
* 创建Dialog传入Application的Context是不可以的。
* 尽管Application、Activity、Service都有自己的ContextImpl，并且每个ContextImpl都有自己的mResource对成员，但是由于他们的mResources成员都来自于唯一的ResouceManager但势力，所以他们看似不同的mResource其实都指向的是同一个快内存。
* Context的的数量等于Activity的个数和Service的个数+1，这个1为Application

## AR和Dalvik的区别
Art上医用启动快，运行快，但是耗费更多存储空间，安装时间长，总的来说ART就是一种“空间换时间的方式”

ART:Ahead of TIme Dalvik:Just in Time

什么是Dalvik：Dalvik是Google公司自己设计用于Android平台的Java虚拟机。Dalvik虚拟机是Google等厂商合作开发的Androdi 移动设备平台的核心组成之一，它可以支持已经转化为.dex（即Dalvik Excutable）格式的的Java应用程序的运行，.dex是专门为Dalvik是实现设计的一种压缩格式，适合内存和处理器速度有限的系统。Dalvik经过优化，允许在有限的内存中同时运行多个虚拟机实例，并且每一个Dalvik应用作为独立的Linux进程执行。独立的进程可以防止虚拟机在崩溃的时候所有程序都被关闭。

什么是ART：Android操作系统已经成熟， Google的Android团队开始将注意力转向一些底层组件，其中之一是负责程序运行的Dalvik运行时。Google开发者已经花了两年时间开发更快执行效率更高更省电的替代ART运行是时。ART即代表Anrdoid Runtime，其处理应用程序执行的方式完全不同于Dalvik。Dalivik是依靠一个Just-In—Time(JIT)的编译器去解释字节码。开发者编译过得代码需要通过一个解释器在用户设备上运行，这一机制并不高效，但让应用能更容易在不同的硬件和架构上运行。ART则完全改变了这套做法，在应用安装的时候就预编译字节码到机器语言。这一机制叫AHead-Of—Time（AOT）编译。在移除解释代码这一过程后，应用程序执行将更有效率，启动更快。

ART优点：

1. 系统的性能显著提升
2. 引用启动更快，运行更快，体验更流畅，触感反馈更及时。
3. 更长的电池续航能力
4. 支持更低的硬件

ARG的缺点：

1. 更大的存储张勇空间，可能会增长10%-20%
2. 更长的安装时间
