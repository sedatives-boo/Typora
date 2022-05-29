## 流库

### 从迭代到流

```java
// 如果想统计一本书所有长单词，首先将单词放到一个长列表中
var contents = new String(Files.readAllBytes(Paths.get("aice.txt")), StandardCharset.UTF_8);
List<String> words = List.of(contents.split("\\PL+"));
//然后再迭代
int count = 0;
for(String w:words){
    if(w.length()>12) count++;
}
//如果使用流
long count = words.stream().filter(w -> w.length()>12).count();
//将stream改为parallelStream就能以并行方式执行
long count = words.parallelStream().filter(w -> w.length()>12).count();
```

流遵循了“**做什么为非怎么做**”，如上我们描述了做什么：获取单词--长度筛选--计数

- 流不存储元素
- 流操作不会修改数据源（如filter不会移除元素，而是生成新的流）
- 流是惰性执行的，

### 流的创建

如果有一个数组，可用静态的Stream.of 方法



## 输入输出











# 补充

### 字节码

在 Java 中，JVM 可以理解的代码就叫做字节码（即扩展名为 `.class` 的文件），它不面向任何特定的处理器，只面向虚拟机。Java 语言通过字节码的方式，在一定程度上解决了传统解释型语言执行效率低的问题，同时又保留了解释型语言可移植的特点。所以， Java 程序运行时相对来说还是高效的（不过，和 C++，Rust，Go 等语言还是有一定差距的），而且，由于字节码并不针对一种特定的机器，因此，Java 程序无须重新编译便可在多种不同操作系统的计算机上运行。

我们需要格外注意的是 `.class->机器码` 这一步。在这一步 JVM 类加载器首先加载字节码文件，然后通过解释器逐行解释执行，这种方式的执行速度会相对比较慢。而且，有些方法和代码块是经常需要被调用的(也就是所谓的热点代码)，所以后面引进了 JIT（just-in-time compilation） 编译器，而 JIT 属于运行时编译。当 JIT 编译器完成第一次编译后，其会将字节码对应的机器码保存下来，下次可以直接使用。而我们知道，机器码的运行效率肯定是高于 Java 解释器的。这也解释了我们为什么经常会说 **Java 是编译与解释共存的语言** 。

> HotSpot 采用了惰性评估(Lazy Evaluation)的做法，根据二八定律，消耗大部分系统资源的只有那一小部分的代码（热点代码），而这也就是 JIT 所需要编译的部分。JVM 会根据代码每次被执行的情况收集信息并相应地做出一些优化，因此执行的次数越多，它的速度就越快。JDK 9 引入了一种新的编译模式 AOT(Ahead of Time Compilation)，它是直接将字节码编译成机器码，这样就避免了 JIT 预热等各方面的开销。JDK 支持分层编译和 AOT 协作使用。但是 ，AOT 编译器的编译质量是肯定比不上 JIT 编译器的。

**为什么说 Java 语言“编译与解释并存”？**

其实这个问题我们讲字节码的时候已经提到过，因为比较重要，所以我们这里再提一下。

我们可以将高级编程语言按照程序的执行方式分为两种：

- **编译型** ：编译型语言 会通过编译器将源代码一次性翻译成可被该平台执行的机器码。一般情况下，编译语言的执行速度比较快，开发效率比较低。常见的编译性语言有 C、C++、Go、Rust 等等。
- **解释型** ：解释型语言会通过解释器一句一句的将代码解释（interpret）为机器代码后再执行。解释型语言开发效率比较快，执行速度比较慢。常见的解释性语言有 Python、JavaScript、PHP 等等。

根据维基百科介绍：

> 为了改善编译语言的效率而发展出的即时编译技术，已经缩小了这两种语言间的差距。这种技术混合了编译语言与解释型语言的优点，它像编译语言一样，先把程序源代码编译成字节码。到执行期时，再将字节码直译，之后执行。Java与LLVM是这种技术的代表产物。
>
> 相关阅读：基本功 | Java 即时编译器原理解析及实践

解答：是因为 Java 语言既具有编译型语言的特征，也具有解释型语言的特征。因为 Java 程序要经过先编译，后解释两个步骤，由 Java 编写的程序需要先经过编译步骤，生成字节码（`.class` 文件），这种字节码必须由 Java 解释器来解释执行。







# JDBC

将读取的blob文件打印出（IO流通用代码）

```java
//rs  是resultSet对象，
Blob photo = re.getBlob("photo");
InputStream is = photo.getBinaryStream();
FileOutputStream fos = new FileOutputStream("myPhotp.jpg");
byte[] buffer = new byte[1024];
int len;
while((len=is.read(buffer))!= -1){
    fos.write(buffer, 0, len);
}
```

```java
Blob photo = re.getBlob("photo");
InputStream is = photo.getBinaryStream();
FileOutputStream fos = new FileOutputStream("文件输出地址");
byte[] buffer = new byte[1024];
int len;
while((len = is.read(buffer))!=-1){//is 将文件读入到内存
    fos.write(buffer,0,len);//fos  将内存文件读出到硬盘位置
}
```

