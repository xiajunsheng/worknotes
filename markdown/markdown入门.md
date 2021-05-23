## Typora

### 简介

- Typora删除了预览窗口，以及所有其他不必要的干扰。取而代之的是实时预览。
- Markdown的语法因不同的解析器或编辑器而异，Typora使用的是[GitHub Flavored Markdown](https://help.github.com/articles/basic-writing-and-formatting-syntax/)。

<iframe height="360" width="640" src="https://www.typora.io/img/beta.mp4" frameborder="0" allowfullscreen="" style="color: rgb(85, 85, 85); font-family: Lato, &quot;PingFang SC&quot;, &quot;Microsoft YaHei&quot;, sans-serif; font-size: 16px; font-style: normal; font-variant-ligatures: normal; font-variant-caps: normal; font-weight: 400; letter-spacing: normal; orphans: 2; text-align: justify; text-indent: 0px; text-transform: none; white-space: normal; widows: 2; word-spacing: 0px; -webkit-text-stroke-width: 0px; background-color: rgb(255, 255, 255); text-decoration-thickness: initial; text-decoration-style: initial; text-decoration-color: initial;"></iframe>



### 下载

Typora[下载](https://www.typora.io/#download)。

### 常用快捷键

- 加粗： `Ctrl/Cmd + B`
- 标题： `Ctrl/Cmd + H`
- 插入链接： `Ctrl/Cmd + K`
- 插入代码： `Ctrl/Cmd + Shift + C`
- 行内代码： `Ctrl/Cmd + Shift + K`
- 插入图片： `Ctrl/Cmd + Shift + I`
- 无序列表： `Ctrl/Cmd + Shift + L`
- 撤销： `Ctrl/Cmd + Z`
- 一级标题：快捷键为`Crtl + 1`，以此类推
- 切换原文和语法：`Ctrl/Cmd + /`
- 建议平常写作时，使用快捷键，使用快捷键，使用快捷键，语法了解即可。

### 块元素

#### 换行符

在markdown中，段落由多个空格分隔。在Typora中，只需回车即可创建新段落。

#### 标题级别

> \# 一级标题， 快捷键为Crtl + 1
> \## 二级标题，快捷键为Crtl + 2
> \###### 六级标题，快捷键为Crtl + 6

#### 引用文字

> \> + 空格 + 引用文字

#### 清单

输入 *列表内容 将创建一个无序列表，该*符号可以替换为+或-。

输入1. 列表内容 将创建一个有序列表，其markdown源代码如下：

> 无序列表
> \* AA
> \* BB
> \* CC
>
> 有序列表
>
> 1. AA
> 2. BB
> 3. CC

#### 任务列表

> \- [ ] 不勾选
> \- [x] 勾选

#### 代码块

在Typora中输入``` + 回车，并在后面选择一个语言名称即可语法高亮。

> 语法高亮:
> \
>
> ```
> > def helloWorld():
> > 	print 'hello, world'
> > \
> ```

#### 数学表达式

输入`$$`，然后按“回车”键，如下：
$$
\mathbf{V}_1 \times \mathbf{V}_2 = \begin{vmatrix}
\mathbf{i} & \mathbf{j} & \mathbf{k} \
\frac{\partial X}{\partial u} & \frac{\partial Y}{\partial u} & 0 \
\frac{\partial X}{\partial v} & \frac{\partial Y}{\partial v} & 0 \
\end{vmatrix}
$$

> \$$
> \mathbf{V}_1 \times \mathbf{V}_2 = \begin{vmatrix}
> \mathbf{i} & \mathbf{j} & \mathbf{k} \
> \frac{\partial X}{\partial u} & \frac{\partial Y}{\partial u} & 0 \
> \frac{\partial X}{\partial v} & \frac{\partial Y}{\partial v} & 0 \
> \end{vmatrix}
> \$$

#### 表

输入`| 表头1 | 表头2 |`并回车。即可将创建一个包含两列的表，然后就像操作Word文档一样设置表格即可，没必要知道Markdown的复杂语法，因为这些语法会由Typora自动生成。效果如下：

| First Header | Second Header |
| :----------- | :------------ |
|              |               |

#### 脚注

> 你可以创建一个脚注，像这样[^1].
>
> [^1]: 这是上面的注释内容。

你可以创建一个脚注，像这样[^1](https://www.simon96.online/2018/10/18/Typora入门（中文版）/这是上面的注释内容。).

注意：该例子脚注标识是1，脚注标识可以为字母数字下划线，但是暂不支持中文。脚注内容可为任意字符，包括中文。

#### 分割线

输入`***`或`---` 再按回车即可绘制一条水平线，如下：

------

#### YAML Front Matter

Typora支持[YAML Front Matter](http://jekyllrb.com/docs/frontmatter/)， 在文章开头输入`---`，然后按回车即可。

#### 目录（TOC）

输入`[toc]`然后回车，即可创建一个“目录”。TOC从文档中提取所有标题，其内容将自动更新。

### 跨度元素

跨度元素即图片，网址，视频等，在Typora中输入后，会立即载入并呈现。

#### 链接

##### 内部链接

> 这是一个带有标题属性的[链接](http://example.com/ “标题”).
> 这是一个没有标题属性的[链接](http://example.net/).

效果如下：

这是一个带有标题属性的[链接](http://example.com/).
这是一个没有标题属性的[链接](http://example.net/).

##### 参考链接

> 这是一个[参考链接][id](http://example.com/)。
> [id]: http://example.com/ “标题”

这是一个[参考链接](http://example.com/)。

#### 网址

Typora允许用<括号括起来>, 把URL作为链接插入。输入\[td_simon@outlook.com](mailto:td_simon@outlook.com) 即 [td_simon@outlook.com](mailto:td_simon@outlook.com)。
Typora还会自动链接标准网址。例如：[www.simon96.online。](http://www.simon96.online./)

#### 图片

> ![显示的文字](/path/to/img.jpg)
> ![显示的文字](/path/to/img.jpg “图片标题”)

[![显示的文字](https://www.simon96.online/2018/10/18/Typora%E5%85%A5%E9%97%A8%EF%BC%88%E4%B8%AD%E6%96%87%E7%89%88%EF%BC%89/)](https://www.simon96.online/2018/10/18/Typora入门（中文版）/)
[![显示的文字](https://www.simon96.online/2018/10/18/Typora%E5%85%A5%E9%97%A8%EF%BC%88%E4%B8%AD%E6%96%87%E7%89%88%EF%BC%89/%22%E5%9B%BE%E7%89%87%E6%A0%87%E9%A2%98%22)](https://www.simon96.online/2018/10/18/Typora入门（中文版）/)

#### 倾斜

> *单个星号*
> _单下划线_

效果如下：
*单个星号*

*单下划线*

#### 加粗

> *两个星号*
> _双下划线_

效果如下：
**两个星号**
**双下划线**

#### 代码标记

标记代码使用反引号，即在英文输入法下，ESC键下面和1键左边的符号——`

使用该`printf()`功能。
效果如下：
使用该`printf()`功能。

#### 删除线

> ~~删除线~~

效果如下：

~~删除线~~

#### 下划线

\下划线

效果如下：

下划线

#### 表情符号:smile:

> ：smile ：（注意为：是英文的冒号）

:smile:

#### 下标

H~2~O (需在设置中打开该功能)

#### 上标

X^2^(需在设置中打开该功能)

#### 高亮

==高亮==(需在设置中打开该功能)

### HTML

支持HTML

#### 嵌入内容

支持iframe-based嵌入代码，

> < iframe height=’265’ scrolling=’no’ title=’Fancy Animated SVG Menu’ src=’http://codepen.io/jeangontijo/embed/OxVywj/?height=265&theme-id=0&default-tab=css,result&embed-version=2' frameborder=’no’ allowtransparency=’true’ allowfullscreen=’true’ style=’width: 100%;’>

#### 视频

> < video src=”xxx.mp4” />

------

**总结：**

1. 建议打开大纲视图（快捷键ctrl + shift + 1）。
2. 插入表格需要顶格写，不然显示不出来。
3. 以上语法不用刻意记，在Typora中的右键菜单都有， 常用功能基本上都有快捷键。
