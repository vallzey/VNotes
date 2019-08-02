# Java中接口与抽象类的区别？ [🔗](https://www.cnblogs.com/dolphin0520/p/3811437.html) 

- 首先接口可以多实现，类只能单继承抽象类。
- 接口中定义的对象都是final abstract，而抽象类中不仅仅拥有abstract对象，但是后面发现如果一个类不包含抽象方法，只是用abstract修饰的话也是抽象类。
- 也就是说抽象类不一定必须含有抽象方法。
- 包含抽象方法的类称为抽象类，但并不意味着抽象类中只能有抽象方法


# 双亲委派模型
- [类加载器（classloader）和双亲委派模型原理](https://www.cnblogs.com/dolphin0520/p/3811437.html) 
> （这里有个源码细节，由于启动类加载器是内嵌于 JVM 且无法被引用，因此 Extension Classloader 指派 parent 为 null，即等同于指派启动类加载器为自己的父加载器）

java中类加载器主要用于实现类的加载，Java中的类和类加载器一起唯一确定类在JVM中的一致性。

系统提供的类加载器：启动类加载器、扩展类加载器、应用程序类加载器。

- 启动类加载器：用C++实现，是JVM的一部分，其他加载器使用Java实现，独立于JVM。主要负责加载<JAVA_HOME>\lib目录下的类库或被-Xbootclasspath参数指定的路径中的类库，应用程序不能使用该类加载器。
- 扩展类加载器：负责加载<JAVA_HOME>/lib/ext目录下或者类系统变量java.ext.dirs指定路径下的类库，开发者课直接使用。
- 应用程序类加载器：主要负责加载classpath下的类库，若应用程序没有自定义类加载器，默认使用此加载器

双亲委派模型要求除了启动类加载器，其他类加载器都有自己的父类加载器，使用组合关系来实现复用父类加载器。过程：若一个类加载器收到类加载请求，会把此请求委派给父类加载器去完成，每层都是如此，因此所有的加载请求最后都会传到启动类加载器；只有当父类加载器反馈不能加载，才会把此请求交给子类完成。

好处：使得java类伴随他的类加载器有了优先级；保证Java程序运行的稳定性


# 简述分派

包括静态分派与动态分派

- 静态分派：发生在编译时期，所有依赖静态类型来定位方法执行版本的分派称为静态分派，典型应用为方法重载。
- 动态分派：在运行期根据实际类型确定方法执行版本的分派过程。典型应用为方法重写，实现是在方法去中建立方法表，若子类中没有重写父类方法，则子类虚方法表中该方法的入口地址与父类指向相同，否则子类方法表中地址会替换为指向子类重写的方法的入口地址。


# 对象的内存布局

[JVM——深入分析对象的内存布局](https://www.cnblogs.com/zhengbin/p/6490953.html)


# java中的泛型擦除？   
[Java 泛型，你了解类型擦除吗？](https://blog.csdn.net/briblue/article/details/76736356)

# 死锁是如何产生的以及四个必要条件？  
[死锁产生的原因及四个必要条件](https://zhuanlan.zhihu.com/p/25677118)

# 简述java Object类中的方法有哪些？
[java基础之Object类解析](https://zhuanlan.zhihu.com/p/55584118)


# 简述java中内部类

[Java内部类详解](https://www.cnblogs.com/dolphin0520/p/3811445.html)

# CopyOnWriteArrayList？

[CopyOnWriteArrayList](https://www.cnblogs.com/dolphin0520/p/3938914.html)












