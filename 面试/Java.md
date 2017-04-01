#### 基础知识
1.`swithc(expr)` 中，expr在jdk1.5之前可以是byte，short，char，int，jdk1.5中可以是enum，jdk1.7开始，可以是String，但是long都不可以；
2.两个对象equals时，hashCode一定相等，大师hashCode相等，不一定equals；在哈希集合中，先用hashCode定位，如果存在hash碰撞（hashCode一样），再进行equals比较；
3.Object.wait和Object.notfy；只有拥有该对象的锁的线程才可以调用wait，只有notify，notifyAll，中断，wait时间到了，线程才会进入runnable状态；
4.强/软/弱/虚引用；强引用：对象就不会回收；软引用：堆将要OOM，回收软引用指向的对象；弱引用:GC回收弱引用指向的对象；
5.String/StringBuffer/StringBuilder，String是只读字符串，StringBuffer/StringBuilder是可以修改的，StringBuffer是线程安全，StringBuilder是线程不安全的；
6.try/catch/finally，try中有return，finally中的return还是会执行，并且return结果是finally中的；
7.Error和Exception，都继承与Throwable，Exception又分为Check-Exception和RuntimeException；
8.内部静态类和内部非静态类，内部非静态类需要持有外部类的引用；
9.XML解析，SAX/PULL/DOM，SAX和PULL是基于事件的，边解析边处理，DOM是读取整个文件，再处理；
    SAX和PULL都是基于事件驱动，SAX是内部驱动，PULL需要业务层自己驱动；DOM是读取整个文件；
10.ArrayList和LinkedList都是线程不安全的，Vector是线程安全的，但是Vector2倍扩容，更占内存；
11.HashMap，HashTable，ConcurrentHashMap：HashMap线程不安全，HashTable通过在方法上加synchronized，ConcurrentHashMap通过分段锁，高并发下提升性能；
    HashMap的结构是数组+链式HashEntry，通过hashCode定位数组的position，如果hashCode冲突，则通过链式用来存储；
12.扩容，ArrayList：超过最大时，2被扩容；Vector：超过最大时，2倍扩容；LinkedList：不需要扩容；HashMa/HashTable扩容因子是0.75；
13.Java集合主要分为三类：List，Set和Map，List和Set继承于Collection；
#### OOM
Java内存泄漏的根本原因是什么呢？长生命周期的对象持有短生命周期对象的引用就很可能发生内存泄漏；
##### 1.常见OOM场景
+ 静态集合类引起内存泄漏；
+ 集合中的对象修改之后，remove失败；
+ 监听器未删除；
+ 各种连接未关闭，比如数据库，网络，io；
+ 内部类和外部模块的引用；
+ 单例模式；
+ 图片加载；

##### 2.OOM解决方案
+ 图片大小缩放（BitmapFactory.Option.inJustDecodeBounds = true,BitmapFactory.Option.inSampleSize = n）,
图片质量压缩（BitmapFactory.Option.inPreferredConfig = Config.RGB_565）;
+ Cache设计；
+ SoftRefrence/WeakRefrence；
+ 资源Close（Cursor，Connection，IO）
+ 池技术/享元;

#### JVM
##### JVM内存模型

![JVM_内存模型](Image/JVM_内存模型.png)

#### GC
##### 1.GCRoot
GCRoot是堆之外可访问的对象，可能是：System Class（系统加载器加载的类），JNI Local（Native中的本地变量），JNI Global（Native中的全局变量），Thread Block（当前活跃线程块中的引用对象），Thread（启动且未停止的线程），Busy Monitor（其wait或notify方法被调用，或者synchronized同步的对象），Java Local（局部变量），Native Stack（Native代码的入参和出参），Finalizer（在队列中等待Finalizer运行的对象），Unfinalized（拥有finalize方法，但是还没有被终结且不再finalizer队列的对象），Unreachable（其他对象不可达，但是被内存分析器标记为GCRoot），Unknown（没有根类型的对象）；

##### 2.GC算法
引用计数算法（存在循环引用问题）
GCRoot
