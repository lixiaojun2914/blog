---
title: matplotlib实例
date: 2019-07-01 07:30:22
tags:
---

# matplotlib实例
```py
import matplotlib.pyplot as plt
import numpy as np

x = np.linspace(-3, 3, 50)
y1 = x ** 2
y2 = 2 * x + 1
plt.figure(figsize=(8, 5))
plt.subplot(221)
plt.plot(x, y1, label='up')
plt.plot(x, y2, color='red', linewidth=2., linestyle='--', label='down')
plt.xlim(-1, 2)
plt.ylim(-2, 3)
plt.xlabel('I am x')
plt.ylabel('I as y')
new_ticks = np.linspace(-1, 2, 5)
plt.xticks(new_ticks)
plt.yticks([-2, -1.8, -1, 1.22, 3],
           [r'$really\ bad$', r'$bad$', r'$normal$', r'$good$', r'$really\ good$'])
#gca='get current axis'
ax = plt.gca()
ax.spines['right'].set_color('none')
ax.spines['top'].set_color('none')
ax.xaxis.set_ticks_position('bottom')
ax.yaxis.set_ticks_position('left')
ax.spines['bottom'].set_position(('data', 0))
ax.spines['left'].set_position(('data', 0))
plt.legend()

plt.subplot(222)
plt.plot(x, y1)

plt.subplot(223)
plt.plot(x, y2)

plt.subplot(224)
plt.plot(x, y1)
plt.plot(x, y2)

plt.show()
```
![](https://github.com/lixiaojun2914/blog/blob/master/source/_posts/matplotlib%E5%AE%9E%E4%BE%8B.png?raw=true)