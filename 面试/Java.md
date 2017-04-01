#### 基础知识

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
