---
title: "Markdown笔记"
date: 2022-01-29T10:04:53+08:00
description: markdown语法笔记
slug: markdown
categories:
    - Markdown
tags:
    - Markdown语法
---
# Markdown语法笔记
## 标题语法
```md
# level1
## level2
### level3
#### level4
##### level5
###### level6
```
# level1
## level2
### level3
#### level4
##### level5
###### level6

## 段落语法
段落中间用一个空行将不同的段落分割
```md
I really like using Markdown.

I think I'll use it to format all of my documents.
```
I really like using Markdown.

I think I'll use it to format all of my documents.

## 换行语法
换行可用两个空格或者html中的\<br\>进行换行
```md
First line with two space after.  
And the next line.
First line with html tag after.<br>
```
First line with two space after.  
And the next line.
First line with html tag after.<br>

## 强调语法
```md
**bold text**  
*italicized text*  
***bold and italicized***  
~~delete line~~
```
**bold text**  
*italicized text*  
***bold and italicized***  
~~delete line~~

## 引用语法
```md
>This is a reference.
> ## This is another reference.
```
>This is a reference.
> ## This is another reference.

## 列表语法
### 有序列表
```md
1. first
2. second
1. third
8. fourth
```
1. first
2. second
1. third
8. fourth

### 无序列表
```md
- first
* second
+ third
```
- first
* second
+ third

### 任务列表
```md
- [x] first
- [ ] second
- [ ] third
```
- [x] first
- [ ] second
- [ ] third

### 列表中添加其他元素
#### 嵌套段落
嵌套段落，应将元素缩进4个空格或一个制表符
```md
- This is the first item.
- This is the second item.  
    Another paragraph below the second item.
- This is the third item.
```
- This is the first item.
- This is the second item.  
    Another paragraph below the second item.
- This is the third item.

#### 嵌套代码块
嵌套代码块，应将元素缩进8个空格或两个制表符,同时增加一个空行
```md
1. Open the file.
2. Find the follow block  

        <html>
            <head>
                <title>Test</title>
            </head>
        </html>
3. Update the title to match.
```
1. Open the file.
2. Find the follow block  

        <html>
            <head>
                <title>Test</title>
            </head>
        </html>
3. Update the title to match.

## 代码语法
- 要将短语标注为代码，将其包裹在反引号( \` )中
    ```md
    type `nano`
    ```
    type `nano`
- 如果代码中包含反引号，将其包裹在双反引号( \`\` )中
    ```md
    type `` `nano` ``
    ```
    type `` `nano` ``

## 分隔线语法
```md
***
---
___
```
***
---
___

## 链接语法
- 链接
    ```md
    [Blog](https://lixiaojun2914.github.io "我的博客地址")
    ```
    [Blog](https://lixiaojun2914.github.io "我的博客地址")
- 网址和email地址
    ```md
    <https://lixiaojun2914.github.io>
    <982090951@qq.com>
    ```
    <https://lixiaojun2914.github.io>  
    <982090951@qq.com>

## 图片语法
```md
![This is a image](https://tenfei04.cfp.cn/creative/vcg/800/new/VCG211291536009.jpg "have fun")
```
![This is a image](https://tenfei04.cfp.cn/creative/vcg/800/new/VCG211291536009.jpg "have fun")

## 表格语法
```md
| Syntax    | Description | test |
| :-------- | :---------: | ---: |
| Header    |    Title    | test |
| Paragraph |    Text     | test |
```
| Syntax    | Description | test |
| :-------- | :---------: | ---: |
| Header    |    Title    | test |
| Paragraph |    Text     | test |

## 围栏代码块
```md
```json
{
    "test": 123,
    "age": 25
}
\```
```
```json
{
    "test": 123,
    "age": 25
}
```

## emoji
```md
:tent: :joy:
```
:tent: :joy: