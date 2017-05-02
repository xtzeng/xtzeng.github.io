---
title: MarkDown一些常用语法
date: 2017-04-26 10:51:45
tags:
---

1.引入代码

```java
public class Main {
    public static void main(String[] args) {
        System.out.println("Hello World");
    }
}
```

```javascript
var s = "Javascript syntax hightlighting";
alert(s);
```
2.链接(Links)
Markdown中有两种方式，实现链接，一种是内联方式，另一种是引用方式

内联方式：This is an [baidu link](http://www.baidu.com)

引用方式：I get 10 times more traffic from [Google][1] than from [Yahoo][2] or [MSN][3].  

[1]: http://google.com/        "Google" 
[2]: http://search.yahoo.com/  "Yahoo Search" 
[3]: http://search.msn.com/    "MSN Search"

3.分割线

“一个空行”加上“连续3个以上的减号符号(即—)”的组合，使得得到一个分割线。 快捷键：Ctrl+R

----------

4.表格

使用“|”符号隔开不同列，第一行作为列名行，第二行必须为一个格式控制行，表明整个内容以表格形式展示。格式控制行最简单的样式如“|-|-|-|”所示，这表示以3列的形式展示表格。在“-”的左边加“:”（即“:-”），表示单元格的内容左对齐;在“-”的右边加“:”（即“-:”），表示单元格的内容右对齐;在“-”的两边加“:”（即“:-:”），表示单元格的内容居中对齐。 
比如现在有如下内容：


### 表格

| Item      |    Value | Qty  |
| :-------- | --------:| :--: |
| Computer  | 1600 USD |  5   |
| Phone     |   12 USD |  12  |
| Pipe      |    1 USD | 234  |


