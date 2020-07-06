1. ```JIT``` 属于运行时编译。在完成第一次编译后，会将字节码对应的机器码保存下来。下次直接使用。
2. ```char``` 在 ```java``` 中占 2 字节。
3. ```String``` 内部类是 ```private final char value[]``` 是用 ```final``` 修饰是不可变的。
4. ```StringBuilder``` 和 ```StringBuffer``` 都是继承于 ```AbstractStringBuilder``` 内部也是字符数组 ```char[] value``` 没有 ```final``` 修饰，所以是可变的。
5. 上述三个类型的线程安全性：
   + ```String``` 不可变，*线程安全*
   + ```StringBuffer``` 加了同步锁，*线程安全*
   + ```StringBuilder``` *线程不安全*
6. 上述三个类型的性能比较：
   + ```String``` 每次改变都会生成新的 ```String``` 对象，然后指针再指向新的 ```String``` 对象。
   + ```StringBuffer``` 和 ```StringBuilder``` 是对本身进行操作，```StringBuilder``` 的性能略高于 ```StringBuffer```。
7. 接口和抽象类的异同：
   +  
8. ```==``` 和 ```equals``` 方法的区别：
   + ```==``` 对于基本类型比较的是值，对于引用类型比较的是地址。
   + ```equals``` 如果未被覆盖，等同于 ```==``` ；如果被覆盖了，则可以比较内容。
9. ```equals``` 和 ```hashcode``` :
   + 如果 ```equals``` 为 ```true``` 。那么，```hashcode``` 一定相同 。
   + 如果 ```hashcode``` 相同，那么， ```equals``` 不一定为 ```true``` 。
   + 如果 ```equals``` 覆盖过，那么， ```hashcode``` 必须覆盖。
   + ```hashcode``` 只在散列表中有用。
10. ![线程状态图](https://github.com/JK9559/WIO/blob/master/note/Java/Basic/ThreadStatus.png)
11. ```final``` 使用方法总结：
    + ```final``` 能用在：变量上、方法上、类上
    + ```final``` 变量：基本类型上，值不能改。引用类型上，初始化后不能指向另一个对象。
    + ```final``` 方法：
        + 防止继承类修改
        + 会转为内嵌调用提高效率
        + 类中的 ```private``` 方法默认是 ```final``` 的。
    + ```final``` 类：说明该类不能继承。```final``` 类的全部成员方法都是 ```final``` 的。
12. ```Java``` 的异常：
    + 所有的异常都继承于 *```Throwable```* 类
    + 可以分为两类：
        + ```Error```：错误。程序无法处理，比如：```StackOverflowError``` 等。
        + ```Exception```：异常。程序可以处理，比如：
            + ```IOException``` ：如 ```FileNotFoundException```
            + ```RuntimeException``` ：如 ```NullPointerException```
    + ```Throwable``` 常用方法：
        + ```String getMessage()``` *返回异常发生的简要描述*
        + ```String toString()``` *返回异常发生的详细描述*
        + ```void printStackTrace()``` *在控制台打印 ```Throwable``` 封装的异常信息*
        + ```String getLocalizedMessage()``` *返回异常对象的本地化信息。只有覆盖这个方法才行，不然和 ```getMessage``` 一样*。
13. ```try-catch-finally```
    + ```try```： 后接 0 个或者 多个 ```catch```。如果没有 ```catch``` 则必有 ```finally```。
    + ```catch```：处理 ```try``` 的异常。
    + ```finally```：理论上必执行，即使 ```try``` 或者 ```catch``` 有 ```return```， ```finally``` 也会在返回前被执行。
        + 但是 ```finally``` 在以下四种情况也不会被执行：
            + ```finally``` 块上来就发生了异常
            + 前面代码执行了 ```System.exit``` 来退出程序
            + 程序所在线程死亡
            + ```CPU``` 被关闭
14. 深拷贝和浅拷贝：
    + 浅拷贝：基本类型值传递，引用类型传递引用的拷贝。
    + 深拷贝：基本类型值传递，引用类型新创建对象，再复制内容。