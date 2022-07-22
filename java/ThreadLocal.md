
## ThreadLocal

### 你能说一下 ThreadLocal 吗？

ThreadLocal提供线程局部变量，每个线程都有自己的副本变量，多个个线程之间互不干扰。

**底层结构：**

Thread 类提供了一个 ThreadLocal.ThreadLocalMap threadLocals = null 的实例变量，其实就是每个线程都有自己的 ThreadLocalMap。

```
/* ThreadLocal values pertaining to this thread. This map is maintained
  * by the ThreadLocal class. */
ThreadLocal.ThreadLocalMap threadLocals = null;

```
ThreadLocalMap 作为 ThreadLocal 的内部类有自己的实现，key 相当于 ThreadLocal，value 是放入的值，因为它继承了 WeakReference 类，它是一个**弱应用**。
每个线程在往 ThreadLocal 里放值的时候，都会往自己的 ThreadLocalMap 里存，读也是 ThreadLocal 作为引用，在自己的 map 里找对应的 key，从而实现了**线程隔离**。
```
public class ThreadLocal<T> {

    ......

    static class Entry extends WeakReference<ThreadLocal<?>> {
        /** The value associated with this ThreadLocal. */
        Object value;

        Entry(ThreadLocal<?> k, Object v) {
            super(k);
            value = v;
        }
    }

    ......

}
```
ThreadLocalMap 有点类似 HashMap 的结构，HashMap 是由**数组+链表**实现的，而 ThreadLocal 中没有链表。


- **强引用**：创建一个对象并把这个对象赋给一个引用变量，普通 new 出来对象的变量引用都是强引用，有引用变量指向时永远不会被垃圾回收，jvm 即使抛出 OOM，可以将引用赋值为 null，那么它所指向的对象就会被垃圾回收。
- **软引用**：如果一个对象具有软引用，内存空间足够，垃圾回收器就不会回收它，如果内存空间不足了，就会回收这些对象的内存。只要垃圾回收器没有回收它，该对象就可以被程序使用。
- **弱引用**：非必需对象，当 JVM 进行垃圾回收时，无论内存是否充足，都会回收被弱引用关联的对象。
- **虚引用**：虚引用并不会决定对象的生命周期，如果一个对象仅持有虚引用，那么它就和没有任何引用一样，在任何时候都可能被垃圾回收器回收。






