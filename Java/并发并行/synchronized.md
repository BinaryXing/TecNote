#### 基本常识
+ 每个类只有一个锁，每个对象只有一个锁；
+ synchronized `()` 中的是锁， `{}` 中的是同步代码块；
+ synchronized有两种，同步方法和同步代码块；

---

#### 结论
1. synchronized方法：同步方法拿到的是对象锁，所以不同线程调用该对象的该方法或者其他synchronized方法会互斥；
2. synchronized静态方法：静态同步方法拿到的是类锁，所以不同线程调用该类或者该类的对象的该方法或者其他synchronized静态方法会互斥；
3. synchronized `(obj)` 代码块：代码块拿到的是obj的对象锁，如果不同线程的执行，是同一个对象锁，会互斥；
4. synchronized `(class)` 代码块，代码块拿到的是class的类锁，如果不同线程的执行，会互斥；
