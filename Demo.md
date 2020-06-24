<!--
 * Copyright by 2020 Countra. All rights reserved.
 * @author: Countra
 * @date: 2020-06-13
-->

<!-- @import "[TOC]" {cmd="toc" depthFrom=1 depthTo=6 orderedList=false} -->

<!-- code_chunk_output -->

- [Test the first markdown page](#test-the-first-markdown-page)
  - [this is second title](#this-is-second-title)
    - [this is third title](#this-is-third-title)
  - [**_math formula_**](#math-formula)
    - [流程图](#流程图)
  - [你好这是结尾](#你好这是结尾)

<!-- /code_chunk_output -->




# Test the first markdown page

&copy;

[希儿](#jump)
[结尾](#你好这是结尾)

<center>居中对齐</center>
<hr>

use `prinf("hello");` 强调代码

## this is second title

```c
int main()
{
    printf("Hello world!");
    return 0;
}
```

### this is third title

> **_hello fsociety_**

|   c   |  c++  | Java  |
| :---: | :---: | :---: |
|  1.5  |  1.0  |  2.5  |
|   2   |   5   |   6   |

## **_math formula_**

$$
\lim_{x \to \infin}\frac{sin(t)}{x}=1
$$

<div align=center id="jump"><img width='300' height='350' src="https://cdn.jsdelivr.net/gh/Countra/Picgo_pic/images/xier.jpg" /> </div>

![xier](https://cdn.jsdelivr.net/gh/Countra/Picgo_pic/images/xier.jpg)

![20200605210946](https://cdn.jsdelivr.net/gh/Countra/Picgo_pic/images/20200605210946.png)

<center>
<font size=6 color=00fff>下标和上标</font><br>  
H<sub>2</sub>O and CO<sub>2</sub>  <br>
Counta<sup>TM</sup>
</center>

使用 Markdown[^1]可以效率的书写文档, 直接转换成 HTML[^2], 你可以使用 Typora[^t] 编辑器进行书写。
[^1]:Markdown 是一种纯文本标记语言
[^2]:HyperText Markup Language 超文本标记语言
[^t]:NEW WAY TO READ & WRITE MARKDOWN.

- [ ] a task list item
- [ ] list syntax required
- [ ] normal **formatting**, @mentions, #1234 refs
- [ ] incomplete
- [x] completed

### 流程图
```flow
st=>start: Start
e=>end
op=>operation: My Operation
cond=>condition: Yes or No?

st->op->cond
cond(yes)->e
cond(no)->op
```

以及时序图:

```sequence
Alice->Bob: Hello Bob, how are you?
Note right of Bob: Bob thinks
Bob-->Alice: I am good thanks!
```

## 你好这是结尾
