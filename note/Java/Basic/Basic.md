> 1. ```JIT``` 属于运行时编译。在完成第一次编译后，会将字节码对应的机器码保存下来。下次直接使用。
> 2. ```char``` 在 ```java``` 中占 2 字节。
> 3. ```String``` 内部类是 ```private final char value[]``` 是用 ```final``` 修饰是不可变的。
> 4. ```StringBuilder``` 和 ```StringBuffer``` 都是继承于 ```AbstractStringBuilder``` 内部也是字符数组 ```char[] value``` 没有 ```final``` 修饰，所以是可变的。
> 5. 上述三个类型的线程安全性：
>> * ```String``` 不可变，*线程安全*
>> * ```StringBuffer``` 加了同步锁，*线程安全*
>> * ```StringBuilder``` *线程不安全*
>
> 6. 上述三个类型的性能比较：
>> * ```String``` 每次改变都会生成新的 ```String``` 对象，然后指针再指向新的 ```String``` 对象。
>> * ```StringBuffer``` 和 ```StringBuilder``` 是对本身进行操作，```StringBuilder``` 的性能略高于 ```StringBuffer```。
> 7. 接口和抽象类的异同：
>> * 