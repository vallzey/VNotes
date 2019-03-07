### OpenJDK 项目 Code Tools

#### 字节码汇编器反汇编器 [ASMTools](https://wiki.openjdk.java.net/display/CodeTools/asmtools)([Download](https://adopt-openjdk.ci.cloudbees.com/view/OpenJDK/job/asmtools/lastSuccessfulBuild/artifact/asmtools-6.0.tar.gz))

ASMTools 的反汇编以及汇编操作所对应的命令分别为：
```bash
java -cp /path/to/asmtools.jar org.openjdk.asmtools.jdis.Main Foo.class > Foo.jasm
```

```bash
java -cp /path/to/asmtools.jar org.openjdk.asmtools.jasm.Main Foo.jasm
```

#### [JOL](http://openjdk.java.net/projects/code-tools/jol/)([Download](http://central.maven.org/maven2/org/openjdk/jol/jol-cli/0.9/jol-cli-0.9-full.jar))
JOL 可用于查阅 Java 虚拟机中对象的内存分布，具体可通过如下两条指令来实现。

```bash
$ java -jar /path/to/jol-cli-0.9-full.jar internals java.util.HashMap
$ java -jar /path/to/jol-cli-0.9-full.jar estimates java.util.HashMap
```


