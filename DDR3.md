# 简介
<ref: https://blog.csdn.net/fzhykx/article/details/84783393>

DDR3的内部是一个存储阵列，可以将它想象成一张表格。
和表格的检索原理一样，指定一个行（Row）、列（Column），就可以索引到对应单元格，此即内存芯片寻址基本原理。
对于内存，这个单元格可称为存储单元,该表格（存储阵列）即称逻辑 Bank（Logical Bank，下面简称Bank）。 

DDR3内部Bank示意图，这是一个NXN的阵列，B代表Bank地址编号，C代表列地址编号，R代表行地址编号,根据寻址命令就能确定表中对应地址中存储的对应数据。若寻址命令是B1、R2、C6，则为图中红格位置。
目前DDR3内存芯片基本上都是8个Bank设计，也就是共有8个“表格”。寻址流程：先指定Bank地址，指定行地址，指列地址，最终寻址单元。

![DDR3-inner-BANK-Pic](https://img-blog.csdn.net/20140116161443671?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvbmp1aXRqZg==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/Center)

目前DDR3系统还存在物理Bank的概念，这是对内存子系统的一个相关术语，不针对内存芯片。为了保证CPU正常工作，内存必须一次传输完CPU在一个传输周期内所需要的数据。而CPU在一个传输周期能接受的数据容量就是CPU数据总线的**位宽**，单位为bit(位)。控制内存与CPU之间数据交换的北桥芯片也因此**将内存总线的数据位宽等同于CPU数据总线的位宽**，这个位宽就称为物理Bank（Physical Bank，有的资料称之为Rank）的位宽。目前这个位宽基本为64bit。
