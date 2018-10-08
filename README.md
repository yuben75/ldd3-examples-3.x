Advertisement
=================
腾讯诚招PHP后台、C++后台、Android终端、IOS终端

有意者邮件522069228(@)qq.com

长期有效

PHP后台
http://hr.tencent.com/position_detail.php?id=21921

C++后台
http://hr.tencent.com/position_detail.php?id=16499

Android终端
http://hr.tencent.com/position_detail.php?id=17212

IOS终端
http://hr.tencent.com/position_detail.php?id=16916


ldd3-examples-3.x
=================

port of the ldd3 source code examples to linux 3.x

Backgroud
=================
ldd3 is Linux Device Drivers, Third Edition.
This is a great book about how to write linux device drivers.
You can get this book and its source code examples free
from http://lwn.net/Kernel/LDD3/.

But, the souce code examples in the book are based on linux 2.6.10,
which was released in 2005. This means that all the original examples 
won't compile in the current linux 3.x branch. I've ported all examples 
to the longterm stable branch after linux 3.0, including:

|branch          |original release date|
|----------------|:--------------------:|
|linux 3.0       |July 2011 |
|linux 3.2       |January 2012 |
|linux 3.4       |May 2012 |
|linux 3.10      |June 2013 |
|linux 3.12      |November 2013 |
|linux 3.14      |March 2014 |
|linux 3.18      |December 2014 |
|linux 4.1       |June 2015 |

The key difference between this project and other porting attemps is that
all these examples not only compile on the modern kernel version,
but they also **RUN** on the modern kernel!


Quick start
=================
a. clone this repo

b. checkout to branch which is nearest to your linux kernel version

c. just type ```make``` to build ldd3 examples


How to port
=================
(This section is for developers who want to port ldd3 examples by themselves,
reading previous quick start section is enough for the beginners.)

Make it compile.
-----------------
a. clone linux-stable repo from
    http://git.kernel.org/pub/scm/linux/kernel/git/stable/linux-stable.git

b. Use git log to find out who changed what when. Then determine what is causing 
   it to not compile. then change ldd3 examples according to those commits.

   If  compiling errors are 'XXX symbol not found', find root causing commits by:
```
        $git log -p <XXX symbol's file path in original linux version> |\
          grep <XXX symbol>
```

c. Use git bisect when git log fails to work.

Make it run.
-----------------
First you should understand the original examples,

Second you should understand the related commits in the modern linux version.

If you still can't fix the bug, debug it using below methods:

a. compare similar driver code in linux-stable.
   For example: debuging snull by refering to loopback.c,
       debug sbull by refering to loop.c...

b. printk

c. gdb/qemu.
   compile busybox+linux running in qemu, load buggy module, use gdb to debug it.
   Embedded Linux From Scratch is useful when doing such tasks, refer to
   http://free-electrons.com/docs/elfs/.

















|-- LICENSE
|-- Makefile
|-- include
|   `-- lddbus.h       示例代码中，#include "lddbus.h"。
|-- lddbus
|   |-- Makefile
|   `-- lddbus.c       CHAPTER_14.4:虚拟总线实现
|-- misc-modules
|   |-- Makefile
|   |-- complete.c     CHAPTER_5.4. Completions 机制
|   |-- faulty.c       CHAPTER_4.5.1. oops 消息
|   |-- hello.c        CHAPTER_2.2：超级用户可以加载和卸载模块示例。
|   |-- hellop.c       CHAPTER_2.8. 模块参数
|   |-- jiq.c          CHAPTER_7.6.1. 共享队列
|   |-- jit.c          CHAPTER_7.4.1. 定时器 API
|   |-- kdataalign.c   CHAPTER_11.4.4. 数据对齐展示编译器如何强制对齐
|   |-- kdatasize.c    CHAPTER_11.1：标准 C 类型的使用。显示长整型和指针在64位平台上的不同大小。
|   |-- seq.c          CHAPTER_4.3.1.4. seq_file 接口
|   |-- silly.c        CHAPTER_9.4.5. 在 1 MB 之下的 ISA 内存
|   `-- sleepy.c       CHAPTER_6.2.2. 简单睡眠
|-- misc-progs
|   |-- Makefile
|   |-- asynctest.c    CHAPTER_6.4. 异步通知
|   |-- dataalign      CHAPTER_11.4.4. 数据对齐展示编译器如何强制对齐
|   |-- dataalign.c    CHAPTER_11.4.4. 数据对齐展示编译器如何强制对齐
|   |-- datasize       CHAPTER_11.1：标准 C 类型的使用。
|   |-- datasize.c     CHAPTER_11.1：标准 C 类型的使用。
|   |-- gdbline        CHAPTER_4.6.1. 使用 gdb。为给定的模块可以创建这个命令
|   |-- inp            CHAPTER_9.2.3. 从用户空间的 I/O 存取。从命令行读写端口的小工具, 在用户空间.
|   |-- inp.c
|   |-- load50         CHAPTER_7.3.1.1. 忙等待。这个程序派生出许多什么都不做的进程, 但是以一种 CPU-密集的方式来做.
|   |-- load50.c
|   |-- mapcmp         Simple program to compare two mmap'd areas.
|   |-- mapcmp.c
|   |-- mapper         CHAPTER_15.2.6. 重新映射 RAM
|   |-- mapper.c
|   |-- nbtest         CHAPTER_6.2.6. 测试 scullpipe 驱动
|   |-- nbtest.c
|   |-- netifdebug     CHAPTER_17.3.3. 接口信息
|   |-- netifdebug.c
|   |-- outp           CHAPTER_9.2.3. 从用户空间的 I/O 存取。从命令行读写端口的小工具, 在用户空间.
|   |-- outp.c
|   |-- polltest       Test out reading with poll()
|   |-- polltest.c
|   |-- setconsole     CHAPTER_4.2.2. 重定向控制台消息
|   |-- setconsole.c
|   |-- setlevel       CHAPTER_4.2.1. printk
|   `-- setlevel.c
|-- pci
|   |-- Makefile
|   `-- pci_skel.c     CHAPTER_12.1.5. 注册一个 PCI 驱动
|-- sbull
|   |-- Makefile
|   |-- sbull.c        CHAPTER_16.1. 注册
|   |-- sbull.h
|   |-- sbull_load
|   `-- sbull_unload
|-- scull              CHAPTER_3. 字符驱动。scull( Simple Character Utility for Loading Localities)
|   |-- Makefile
|   |-- access.c
|   |-- main.c
|   |-- main.c.bak
|   |-- pipe.c
|   |-- pipe.c.bak
|   |-- scull.h
|   |-- scull.init
|   |-- scull_load
|   `-- scull_unload
|-- scullc             CHAPTER_8.2.1. 基于slab高速缓存的scull: scullc
|   |-- Makefile
|   |-- main.c
|   |-- mmap.c
|   |-- scullc.h
|   |-- scullc_load
|   `-- scullc_unload
|-- sculld             CHAPTER_14.4.2.3. 设备结构嵌入
|   |-- Makefile
|   |-- main.c
|   |-- mmap.c
|   |-- sculld.h
|   |-- sculld_load
|   `-- sculld_unload
|-- scullp             CHAPTER_8.3.1. 使用整页的scull: scullp，该例子在后面第15章还会使用。
|   |-- Makefile
|   |-- main.c
|   |-- mmap.c
|   |-- scullp.h
|   |-- scullp_load
|   `-- scullp_unload
|-- scullv             CHAPTER_8.4.1. 使用虚拟地址的scull: scullv，该例子在后面15.2.7. 重映射内核虚拟地址还有介绍
|   |-- Makefile
|   |-- main.c
|   |-- mmap.c
|   |-- scullv.h
|   |-- scullv_load
|   `-- scullv_unload
|-- short              CHAPTER 10 演示中断
|   |-- Makefile
|   |-- short.c
|   |-- short_load
|   `-- short_unload
|-- shortprint         CHAPTER 10 写缓冲区示例
|   |-- Makefile
|   |-- shortprint.c
|   |-- shortprint.h
|   |-- shortprint_load
|   `-- shortprint_unload
|-- simple             CHAPTER_15.2. mmap 设备操作。simple( Simple Implementation Mapping Pages with Little Enthusiasm)
|   |-- Makefile
|   |-- simple.c
|   |-- simple_load
|   `-- simple_unload
|-- skull              LDD2：skull.c对ISAI/O的内存探测分析
|   |-- Makefile
|   |-- skull_clean.c
|   `-- skull_init.c
|-- snull              CHAPTER_17.2. 连接到内核
|   |-- Makefile
|   |-- snull.c
|   |-- snull.h
|   |-- snull_load
|   `-- snull_unload
|-- tty                CHAPTER_18. TTY 驱动
|   |-- Makefile
|   |-- tiny_serial.c
|   `-- tiny_tty.c
`-- usb                CHAPTER_13. USB 驱动
    |-- Makefile
    `-- usb-skeleton.c








