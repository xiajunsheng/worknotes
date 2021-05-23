# 1、Java内存区域和内存溢出异常

![jvm](D:\gitrepositoty\worknotes\java\jvm\jvm.bmp)

## 1.1 程序计数器

&emsp;&emsp;程序计数器（Program Counter Register）是一块较小的内存空间，它可以看作是当前线程所执行的字节码的行号指示器。在Java虚拟机的概念模型里，字节码解释器工作时就是通过改变这个计数器的值来选取下一条需要执行的字节码指令，它是程序控制流的指示器，分支、循环、跳转、异常处理、线程恢复等基础功能都需要依赖这个计数器来完成。

&emsp;&emsp;每条线程都需要有一个独立的程序计数器，各条线程之间计数器互不影响，独立存储，我们称这类内存区域为“线程私有”的内存。

&emsp;&emsp;如果线程正在执行的是一个Java方法，这个计数器记录的是正在执行的虚拟机字节码指令的地址；如果正在执行的是本地（Native）方法，这个计数器值则应为空（Undefined）。此内存区域是唯一一个在《Java虚拟机规范》中没有规定任何OutOfMemoryError情况的区域。

## 1.2 Java虚拟机栈

&emsp;&emsp;Java虚拟机栈（Java Virtual Machine Stack）也是线程私有的，它的生命周期与线程相同。虚拟机栈描述的是Java方法执行的线程内存模型：每个方法被执行的时候，Java虚拟机都会同步创建一个栈帧（Stack Frame）用于存储局部变量表、操作数栈、动态连接、方法出口等信息。每一个方法被调用直至执行完毕的过程，就对应着一个栈帧在虚拟机栈中从入栈到出栈的过程。

&emsp;&emsp;局部变量表存放了编译期可知的各种Java虚拟机基本数据类型（boolean、byte、char、short、int、float、long、double）、对象引用（reference类型，它并不等同于对象本身，可能是一个指向对象起始地址的引用指针，也可能是指向一个代表对象的句柄或者其他与此对象相关的位置）和returnAddress类型（指向了一条字节码指令的地址）。这些数据类型在局部变量表中的存储空间以局部变量槽（Slot）来表示，其中64位长度的long和double类型的数据会占用两个变量槽，其余的数据类型只占用一个。局部变量表所需的内存空间在编译期间完成分配。

## 1.3 本地方法栈

&emsp;&emsp;本地方法栈（Native Method Stacks）与虚拟机栈所发挥的作用是非常相似的，其区别只是虚拟机栈为虚拟机执行Java方法（也就是字节码）服务，而本地方法栈则是为虚拟机使用到的本地（Native）方法服务。

## 1.4 Java堆

&emsp;&emsp;Java堆是被所有线程共享的一块内存区域，在虚拟机启动时创建。此内存区域的唯一目的就是存放对象实例，Java世界里“几乎”所有的对象实例都在这里分配内存。在《Java虚拟机规范》中对Java堆的描述是：“所有的对象实例以及数组都应当在堆上分配”。

## 1.5 方法区

&emsp;&emsp;方法区（Method Area）与Java堆一样，是各个线程共享的内存区域，它用于存储已被虚拟机加载的类型信息、常量、静态变量、即时编译器编译后的代码缓存等数据。虽然《Java虚拟机规范》中把方法区描述为堆的一个逻辑部分，但是它却有一个别名叫作“非堆”（Non-Heap），目的是与Java堆区分开来。

&emsp;&emsp;运行时常量池（Runtime Constant Pool）是方法区的一部分。Class文件中除了有类的版本、字段、方法、接口等描述信息外，还有一项信息是常量池表（Constant Pool Table），用于存放编译期生成的各种字面量与符号引用，这部分内容将在类加载后存放到方法区的运行时常量池中。

## 1.6 直接内存

&emsp;&emsp;直接内存（Direct Memory）并不是虚拟机运行时数据区的一部分，也不是《Java虚拟机规范》中定义的内存区域。在JDK 1.4中新加入了NIO（New Input/Output）类，引入了一种基于通道（Channel）与缓冲（Buffer）的I/O方式，它可以使用Native函数库直接分配堆外内存，然后通过一个存储在Java堆里面的DirectByteBuffer对象作为这块内存的引用进行操作。这样能在一些场景中显著提高性能，因为避免了在Java堆和Native堆中来回复制数据。

## 1.7 对象

### 1.7.1 对象创建

![对象创建](D:\gitrepositoty\worknotes\java\jvm\对象创建.png)

### 1.7.2 对象内存结构

&emsp;&emsp;HotSpot虚拟机中，对象在内存中存储的布局可以分为三块区域：对象头（Header）、实例数据（Instance Data）和对齐填充（Padding）。
![对象内存结构01](D:\gitrepositoty\worknotes\java\jvm\对象内存结构01.png)

**对象头**

- 用于存储对象自身的运行时数据， 如哈希码（HashCode）、GC分代年龄、锁状态标志、线程持有的锁、偏向线程ID、偏向时间戳等等，这部分数据的长度在32位和64位的虚拟机（暂 不考虑开启压缩指针的场景）中分别为32个和64个Bits。

- Mark Word被设计成一个非固定的数据结构以便在极小的空间内存储尽量多的信息，它会根据对象的状态复用自己的存储空间。

  - *无锁状* 

    ![image-20210523134948904](C:\Users\JS\AppData\Roaming\Typora\typora-user-images\image-20210523134948904.png)
    
  - *加锁状态*
  
    ![image-20210523135120375](C:\Users\JS\AppData\Roaming\Typora\typora-user-images\image-20210523135120375.png)
    
    
    
    

# 99、附录

## 术语

| 术语名称    | 说明                                  |
| ----------- | ------------------------------------- |
| JIT         | Just In Time Compiler 即时编译器      |
| HotSpot     | 一种Java 虚拟机，具有热点代码探测能力 |
| OSR         | On-Stack Replacement 栈上替换编译     |
| Stack Frame | 栈帧                                  |
| Slot        | 局部变量槽                            |
| TLAB            | Thread Local Allocation Buffer 线程私有的分配缓冲区 |
|             |                                       |

## 参考链接
[Java语言和虚拟机规范](https://docs.oracle.com/javase/specs/index.html)

