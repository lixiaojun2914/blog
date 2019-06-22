---
title: KMP算法
date: 2019-06-22 13:09:46
tags:
    - 算法
    - 模式匹配
    - 串
---
KMP算法是一种字符串模式匹配算法，旨在通过子串来发现不匹配的情况下，下一次模式串应该移动的距离，来减少回溯。
因为这个距离是模式串所决定的，与匹配串无关，所以我们对模式串做一个预处理,用来存储当前位置最长的（前缀==后缀）的长度，可以得到一个next数组如下
```
0                                                           j=0
max{k|i < k < j且p[0]...p[k-1]=p[j-k]...p[j-1] }            集合不为空
1                                                           其它情况
```
因为上面算法是从数组下表1开始的，不符合我们平时使用的字符串，所以代码将所有的位置都减了一个1
因为上面算法是从数组下表1开始的，不符合我们平时使用的字符串，所以代码将所有的位置都减了一个1
```c++
int next_array[maxn];
void get_next(char T[],int len_t) {
	next_array[0] = -1;
	int i = 0;
	int j = -1;
	while (i < len_t) {
		if (j == -1 || T[i] == T[j]) {
			T[++i] != T[++j] ? next_array[i] = j : next_array[i] = next_array[j];//优化，具体查阅严蔚敏的数据结构或算法导论习题32.4-6
			//next_array[++i] = ++j;
		}
		else j = next_array[j];
	}
}

int KMP(char S[], char T[],int pos) {
	int len_s = strlen(S);
	int len_t = strlen(T);
	get_next(T, len_t);
	int i = pos;
	int j = -1;
	while (i < len_s&&j < len_t) {
		if (j == -1 || S[i] == T[j]) { i++; j++; }
		else j = next_array[j];
	}
	if (j >= len_t) return i - len_t;
	return -1;
}
```