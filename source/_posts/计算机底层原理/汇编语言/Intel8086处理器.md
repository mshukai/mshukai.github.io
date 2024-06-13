## 寄存器

| 寄存器                                                       | 功能描述                                                     |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| AX（累加器）、BX（基址寄存器）、CX（计数器）、DX（数据寄存器） | 这 4 个寄存器是通用寄存器，每一个还可以当成 2 个 8 位寄存器来使用，分别 AH、AL、BH、BL、CH、CL、DH、DL |
| SI（索引/变址寄存器）、DI（目标索引寄存器）、BP（基址指针寄存器）、SP（堆栈指针寄存器） | 这 4 个寄存器也是通用寄存器                                  |
| DS 数据段寄存器                                              |                                                              |
| CS 代码段寄存器                                              |                                                              |
| IP 指令指针寄存器                                            |                                                              |
| ES 附加段寄存器                                              |                                                              |
|                                                              |                                                              |
|                                                              |                                                              |
| FLAGS 标志寄存器                                             | 见下文                                                       |

## FLAGS 标志寄存器

| 标志位            | 功能描述                                           | 标识位          | 功能描述        |
| ----------------- | -------------------------------------------------- | --------------- | --------------- |
| CF（Carry Flag）  | 进位标志                                           | OF（Over Flag） | 溢出标志        |
| SF（Sign Flag）   | 符号位标志                                         | ZF（Zero Flag） | 结果为 0 时置 1 |
| PF（Parity Flag） | 奇偶标志，运算结果低 8 位 1 的个数为偶数个时置为 1 |                 |                 |
| DF                |                                                    |                 |                 |

## 指令

### 字符串传送指令

| 指令 | 功能描述 | 标志位状态 |
| ---- | -------- | ---------- |
|      |          |            |
|      |          |            |



| 指令                                  | 功能描述                                                     | 标志位要求            |
| ------------------------------------- | ------------------------------------------------------------ | --------------------- |
|                                       |                                                              |                       |
|                                       |                                                              |                       |
|                                       |                                                              |                       |
|                                       |                                                              |                       |
|                                       |                                                              |                       |
| neg                                   |                                                              |                       |
| div                                   |                                                              |                       |
| idiv                                  |                                                              |                       |
| `cbw`（Convert Byte to Word）         | 操作码为 98，目的是将寄存器 AL 中的有符号数扩展到整个寄存器 AX |                       |
| `cwd`（Convert Word to Double-word）  | 操作码为 99，目的是将寄存器 AX 中的有符号数扩展到整个寄存器 `DX:AX` |                       |
| `jns`（jump when not has sign flag ） |                                                              | SF                    |
| `js`（jump when has sign flag ）      |                                                              | SF                    |
| `jz`（jump when has zero flag ）      |                                                              |                       |
| `jnc`（jump when not has carry flag） |                                                              | CF                    |
| `jc`（jump when has carry flag）      |                                                              | CF                    |
| `jp`（jump when has parity flag ）    |                                                              | PF                    |
| `cmp`（compare）                      | 根据运算的结果设置相应的标志位                               | CF、OF、`ZF`、AF、PF  |
| `je`（jump when equal ）              | 实际上是通过 `cmp` 指令执行减法操作                          | `ZF` = 1              |
| `jne`（jump when not equal ）         |                                                              | `ZF` = 0              |
| `jg`（jump when greater than）        |                                                              | `ZF` = 0<br />SF = OF |
| `jl`（jump when less than）           | 更多比较相关条件转移指令请参考书籍《x86汇编语言：从实模式到保护模式（第2版）》第 7.9.5 章节 |                       |
| `jcxz`（jump if CX is zero）          |                                                              |                       |
|                                       |                                                              |                       |

> 指令英文简称可参考文章：[汇编指令的英文全称（中英文对照）_条件转移指令jpe的全称-CSDN博客](https://blog.csdn.net/ywbhnay/article/details/51106143)。
