# 简介
<ref: https://blog.csdn.net/fzhykx/article/details/84783393>

DDR3的内部是一个存储阵列，可以将它想象成一张表格。
和表格的检索原理一样，指定一个行（Row）、列（Column），就可以索引到对应单元格，此即内存芯片寻址基本原理。
对于内存，这个单元格可称为存储单元,该表格（存储阵列）即称逻辑 Bank（Logical Bank，下面简称Bank）。 

DDR3内部Bank示意图，这是一个NXN的阵列，B代表Bank地址编号，C代表列地址编号，R代表行地址编号,根据寻址命令就能确定表中对应地址中存储的对应数据。若寻址命令是B1、R2、C6，则为图中红格位置。
目前DDR3内存芯片基本上都是8个Bank设计，也就是共有8个“表格”。寻址流程：先指定Bank地址，指定行地址，指列地址，最终寻址单元。

![DDR3-inner-BANK-Pic](https://img-blog.csdn.net/20140116161443671?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvbmp1aXRqZg==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/Center)

目前DDR3系统还存在物理Bank的概念，这是对内存子系统的一个相关术语，不针对内存芯片。为了保证CPU正常工作，内存必须一次传输完CPU在一个传输周期内所需要的数据。而CPU在一个传输周期能接受的数据容量就是CPU数据总线的**位宽**，单位为bit(位)。控制内存与CPU之间数据交换的北桥芯片也因此**将内存总线的数据位宽等同于CPU数据总线的位宽**，这个位宽就称为物理Bank（Physical Bank，有的资料称之为Rank）的位宽。目前这个位宽基本为64bit。

实际工作中，Bank地址与相应的行地址是同时发出的，此时这个命令称之为“行激活”（Row Active）。在此之后，将发送列地址寻址命令与具体的操作命令（是读还是写），这两个命令也是同时发出的，所以一般都会以“读/写命令”来表示列寻址。根据相关标准，从行有效到读/写命令发出之间的**间隔**被定义为tRCD，即RAS to CAS Delay（RAS至CAS延迟，RAS就是行地址选通脉冲，CAS就是列地址选通脉冲），我们可以理解为行选通周期。tRCD是DDR的一个重要时序参数，广义的tRCD以时钟周期（tCK，Clock Time）数为单位，比如tRCD=3，就代表延迟周期为两个时钟周期，具体到确切的时间，则要根据时钟频率而定，DDR3-800，时钟频率100M,tRCD=3，代表30ns的延迟。
