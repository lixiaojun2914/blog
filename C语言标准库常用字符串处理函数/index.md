---
title: C语言标准库常用字符串处理函数
date: "2019-02-14"
tags: 
    - C语言
description: C语言知识
slug: C-lang
image: 006w8JsJly4gv4r2dpemlj61ao0t6agw02.jpg
categories:
    - C语言
---

# string.h
string.h中定义了各种操作字符数组的函数，分为以mem开头和以str开头的两种。以mem开头的函数以给定长度为标准对字符串内存进行操作，以str开头的函数，以'\0'为结尾对字符数组进行操作。
## chr结尾的函数
```c
//在参数str所指向的字符串内存的前n个字节中搜索第一次出现字符c的位置
void *memchr(const void *str, int c, size_t n)
//在参数str所指向的字符串中搜索第一次出现字符c的位置
char *strchr(const char *str, int c)
//在参数str所指向的字符串中搜索最后一次出现字符c的位置
char *strrchr(const char *str, int c)
```
## cpy结尾的函数
```c
//从src复制n个字符到dest
void *memcpy(void *dest, const void *src, size_t n)
//把src所指向的字符串复制到dest
char *strcpy(char *dest, const char *src)
//把src所指向的字符串复制到dest，最多复制n个字符
char *strncpy(char *dest, const char *src, size_t n)
```
在使用cpy函数时，一定要注意判断源字符串和目的字符串的长度，否则会发生缓冲区溢出。
## cmp结尾的函数
```c
//把str1和str2的前n个字节进行比较
int memcmp(const void *str1, const void *str2, size_t n)
//把str1所指向的字符串和str2所指向的字符串进行比较
int strcmp(const char *str1, const char *str2)
//把str1和str2进行比较，最多比较前n个字节
int strncmp(const char *str1, const char *str2, size_t n)
```
## 以cat结尾的函数
```c
//把src所指向的字符串追加到dest所指向的字符串的结尾
char *strcat(char *dest, const char *src)
//把src所指向的字符串追加到dest 所指向的字符串的结尾，直到n字符长度为止
char *strncat(char *dest, const char *src, size_t n)
```
## memset
```c
//复制字符c到参数str所指向的字符串的前n个字符
void *memset(void *str, int c, size_t n)
```
使用memset填充数组时，应当理解memset是以字节为单位进行赋值的，例如memset(a,1,20),若a为int数组，在32位计算机中，a中每个数组元素的值都为0x01010101,即16843009

## strlen
```c
//计算字符串 str 的长度，直到空结束字符，但不包括空结束字符
size_t strlen(const char *str)
```
## strstr
```c
//在字符串str中查找第一次出现字符串needle（不包含空结束字符）的位置。
char *strstr(const char *str, const char *dest)
```