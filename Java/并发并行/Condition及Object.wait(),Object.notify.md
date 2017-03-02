#### wait 和 notify
+ `Object.wait()` `Object.wait(long)` `Object.notify()` `Object.notify()` 都是Object类的native final 方法；
+ 调用某个对象的 `wait` 方法，释放对象锁，阻塞当前线程，必须在 `synchronized` 中，且该对象必须和 `synchronized` 的锁对象是同一个；
+ `wait()` 是释放对象锁，阻塞当前线程， `wait(long)` 释放对象锁long时间，时间一过，重新获取对象锁；
+ 调用某个对象的 `notify` 方法，唤醒该对象的其他 `wait` 线程，必须在 `synchronized` 中，且该对象必须和 `synchronized` 的锁对象是同一个，执行完 `synchronized` 块，释放锁；
+ `notify()` 是唤醒一个 `wait` 该对象锁的线程， `notifyAll()` 是唤醒所有 `wait` 该对象锁的线程，具体哪个线程获取该对象锁由实现决定；
+ `Thread.sleep` 只是将当前线程睡眠，不涉及对象锁；

---

#### Condition
+ Condition是java1.5中出现的，用来替代 `wait` `notify` 实现线程间的协作，更加安全和高效；
+ `Condition.await` 类似于 `Object.wait` ， `Conditon.signal` 类似于 `Object.notify` ；

---

#### 例子
+ 线程间协作最经典的例子就是生产者-消费者模式；当队列已满时，生产者需要释放锁，让消费者消费队列；当队列已空时，消费者需要释放锁，让生产者进行生产队列；
