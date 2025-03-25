# Markdown速成

> 作为一名合格的程序员，学会熟练使用Markdown进行书写各类文档的技术是必不可少的。为了方便快速入门，下面会介绍几种最常见的Markdown语法，可以对照着原文本和预览学习。
## 0. Markdown编辑器下载

推荐[typora](https://typoraio.cn/)(收费), [StackEdit](https://stackedit.io/), [VSCode](https://code.visualstudio.com/), [MarkText](https://github.com/marktext/marktext)等。

## 1. 标题
```
Markdown中一共有6种标题大小
分别为
# 一级标题
## 二级标题
### 三级标题
#### 四级标题
##### 五级标题
###### 六级标题
具体结果如下：
```

# 一级标题

## 二级标题

### 三级标题

#### 四级标题

##### 五级标题

###### 六级标题

## 2. 引用

```cpp
在一段引用前方加上'>'即为引用
样例如下：
>这是一段样例
```

> 这是一段样例

## 3. 标号

### (1) 有序标号

```
即直接在每一点前方添加标号(如：1. 2. 3. ...)
样例如下：
1. 第一点 (在'.'后面需要加空格)
2. 第二点
```

1. 第一点
2. 第二点
   
### (2) 无序标号

```cpp
即直接每一点前方添加"- "或"* "
样例如下：
- 第一点
* 第二点
```
- 第一点
* 第二点
  
## 4. 任务列表(仅部分编辑器支持)

```cpp
在个点前方加入"- [ ] "即可
- [ ] Task1
- [ ] Task2

```

- [ ] Task1
- [ ] Task2
  
## 5. 代码块
```cpp
代码块的格式如下：
例如cpp代码块
在代码前加上"```cpp"
在代码后加上"```"
样例如下：
```
```cpp
#include <bits/stdc++.h>
using std::cout, std::endl;
int main()
{
    int a = 1, b = 2;
    cout << a + b << endl;
    return 0;
}
```
## 6. 数学公式
```cpp
Latex数学公式前后均用"$$"
样例如下：
$$
\frac{\partial f}{\partial x} = 2\sqrt{a}x
$$
```
$$
\frac{\partial f}{\partial x} = 2\sqrt{a}x
$$
## 7. 表格
```cpp
表格分为三部分：
表头 |姓名|年龄|成绩|
对齐方式 |:-|-:|:-:|(分别为左对齐 右对齐 居中)
数据 |A|11|100|
     |B|12|60| 
```
|姓名|年龄|成绩|
|:-|-:|:-:|
|A|11|100|
|B|12|60| 

## 8. 横线
```cpp
添加横线只需要"---"
样例如下；
```
---

## 9. 跳转
### (1) 普通链接
```cpp
插入链接格式为：
[example](www.example.com "A example")
其中"www.example.com"为跳转链接
"A example"是鼠标悬浮文本上的提示
样例如下：
```
[example](www.example.com "A example")
### (2) 引用链接
```cpp
引用链接格式为：
[example][id]
并在后方(至少空一行)某处申明：
[id]:www.example.com "A example"
样例如下：
```
[example][id]

[id]: www.example.com "A example"
### (3) 标题跳转
```cpp
标题跳转格式为：
[标题一](#1-标题)
样例如下：
```
[标题一](#1-标题)

## 10. 插入图片
```cpp
格式如下：
![<替代文本>](<图片地址>"<提示>")
样例如下：
```
![这是一张图片](https://pics0.baidu.com/feed/64380cd7912397dd03088099cc2fb5bad1a28770.jpeg?token=030072e977892ca8c2f929b933137e8e"杀软二次元")

## 11. 行内格式
```cpp
格式如下：
*斜体*
**加粗**
`行内代码`
<u>下划线<\u>
$\theta=x^2$
H~2~O (下标)
x^2^ (上标)
==代码高亮==
Markdown支持大多数html，你甚至可以嵌入视频(仅部分编辑器支持)
<iframe src="//player.bilibili.com/player.html?isOutside=true&aid=985242933&bvid=BV1nt4y17729&cid=824324429&p=1&high_quality=1&danmaku=0" allowfullscreen="allowfullscreen" width="100%" height="500" scrolling="no" frameborder="0" sandbox="allow-top-navigation allow-same-origin allow-forms allow-scripts"></iframe>
```
*斜体*

**加粗**

`行内代码`

<u>下划线</u>

$\theta=x^2$

H~2~O (下标)

x^2^ (上标)

==代码高亮==

<iframe src="//player.bilibili.com/player.html?isOutside=true&aid=985242933&bvid=BV1nt4y17729&cid=824324429&p=1&high_quality=1&danmaku=0" allowfullscreen="allowfullscreen" width="100%" height="500" scrolling="no" frameborder="0" sandbox="allow-top-navigation allow-same-origin allow-forms allow-scripts"></iframe>