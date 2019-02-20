---
title: nasm汇编
date: 2019-02-18 11:00:56
tags:
    - 汇编
    - nasm
---
# nasm汇编
## 寄存器
### 通用寄存器
8086CPU的所有寄存器都是16位的，可以存放两个字节。  
AX,BX,CX,DX这4个寄存器通常用来存放一般性数据，被称为通用寄存器。AH,AL,BH,BL,CH,CL,DH,DL分别为AX,BX,CX,DX对应的高字节和低字节  
32位和64位的系统通用寄存器在其标记前分别加E和R，如EAX，RAX。

### 段寄存器
CS,DS,ES,FS,GS,SS为8086CPU的段寄存器。  
CS:IP为代码段寄存器，用来描述CPU代码执行的位置，计算方法为CSx16+IP。CPU在加电复位时，CS=FFFFH，IP=0000H。即CPU从内存FFFF0H单元开始执行。
DS为数据段寄存器，存储数据段的起始位置
ES，FS，GS为额外的三个段寄存器，命名按照字母顺序
SS为栈段寄存器。

### 偏移寄存器
BP,SI,DI,SP为8086CPU的四个偏移寄存器。  
BP为基址指针寄存器，指向函数的本地环境起始位置。  
SI，DI为源变址寄存器和目的变址寄存器。  
SP为栈指针寄存器，指向栈顶。

### 标志寄存器
EFLAGS寄存器为存放CPU相关状态的寄存器，常用状态标志有:  
ZF=zero flag,  
IF=interrupt enable flag,  
SF=sign flag,  
ZF=zero flag,  
AF=auxiliary carry flag,  
PF=parity flag,  
TF=trap flag
DF=direction flag
OF=overflow flag

## 常用汇编指令
### 赋值指令
```
mov <dest>,<source>
```
将源操数复制到目的操作数，不能讲数据直接复制到某个段寄存器，而必须通过通用寄存器为跳板。
### 加减乘除
```
inc <dest>              ;自增
dec <dest>              ;自减
add <dest>,<source>     ;将源操作数与目的操作数相加，结果存在目的操作数中，操作数尺寸必须一致。
adc <dest>,<source>     ;将源操作数，目的操作数和进位标志相加，操作数尺度必须一致。
sub <dest>,<source>     ;从目的操作数中减去源操作数
sbb <dest>,<source>     ;从目的操作数中减去源操作数，再减去进位标志 

mul <source>     ;将AL/AX/EAX与源操作数相乘，如果源操作数是8位的，则与AL相乘，积存储在AX中；如果源操作数是16位的，则与AX相乘，积存储在EAX中；如果源操作数是32位的，则与EAX相乘，积存储在EDX:EAX中。 

div <dest>,<source>     ;执行8位/16位/32位的无符号整数除法操作。如果除数是8位的，被除数是AX，商在AL中，余数在AH中；如果除数是16位的，被除数是DX:AX，商在AX中，余数在DX中；如果除数是32位的，被除数是EDX:EAX，商在EAX中，余数在EDX中。
```
### push与pop
```
push <value>    ;入栈
pop <dest>      ;出栈
```
### 逻辑运算and,or,xor,not
常用的位运算，与C语言位运算相同  
### 跳转指令(根据标志寄存器的值)
```
jmp <dest>      ;无条件跳转
je/jz <dest>    ;等于则跳转
jne/jnz <dest>  ;不等于则跳转
```
跳转指令还有很多，这里不一一列出

### call与ret
```
call <dest>     ;调用过程，类似C语言函数调用
ret             ;调用过程返回，类似C语言的return
```

### lea
```
lea <dest>,<source> ;将源操作数的偏移地址存入目的操作数
```

### 中断
```
int <val>       ;向处理器发送一个中断信号
```

## 示例(hello world)
```
section .data                   ;声明数据段
msg db "Hello Wrold!",0xa       ;定义一个hello world字符串，  
                                db为伪指令define byte，  
                                0xa为ascii中的换行符
len equ $ - msg                 ;equ第一字面常量，$表示当前位置，$-msg计算字符串长度

section .text                   ;声明代码段
    global _start               ;声明起始调用过程

_start:
    mov edx, len                ;调用sys_write
    mov ecx, msg
    mov ebx, 1
    mov eax, 4
    int 0x80
    mov ebx, 0                  ;调用sys_exit
    mov eax, 1
    int 0x80
```