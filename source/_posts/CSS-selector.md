---
layout: post
title: CSS 选择器
tag: 前端
date: 2017-06-04
---
推荐一个练习 CSS 选择器的小游戏 [CSS Diner](https://flukeout.github.io/)。
<!--more-->
1. 标签选择器
```
h2 { }
```

2. 类选择器
```
.className { }
```

3. ID 选择器
```
#id { }
```

4. 属性选择器
    1. 简单属性匹配
    ```
    a[href] { }
    ```
    2. 根据具体属性值
    ```
    a[href="google.com"] { }
    ```
    3. 根据部分属性值
    ```
    a[href~="google.com"] { }
    ```
    其他一些匹配模式:
    ```css
    p[foo^="bar"] /*匹配开头*/ 
    p[foo$="bar"] /*匹配结尾*/
    p[foo*="bar"] /*包含*/
    ```
5. 后代（上下文）选择器
    1. 选择后代元素
    2. 选择子元素 
        ```
        h1 > strong { }
        ```

    3. 选择兄弟元素 
        ```
        h1 + p { } /* 选择紧接在一个 h1 元素后出现的所以段落，h1 与 p 有相同的父元素 */
        ```


6. 伪类选择器和伪元素选择器
    1. 伪类选择器 
        ```
        a:visited {color: red;}
        ```
        - 静态伪类 
        `:link  :visited :first-child`
             `:first-child`伪类：用于选择作为某个未知元素的第一个子元素的指定元素。
            `:lang(fr)`伪类：根据元素的语言来选择。不同于 `|=`属性选择器，` lang`的语言信息由属性与 META 信息提供，甚至可能包括 HTTP 头信息。
        - 动态伪类 
        `:focus :hover :active`

        结合伪类
        推荐顺序：`link-visited-focus-hover-active`
    2. 伪元素选择器
        - 设置首字母样式
        ```
        p:first-letter {font-size: 200%}
        ```

        - 设置首行样式
        ```
        p:first-line { }
        ```

        *需要注意的是，应用`:first-letter :first-line`的元素允许的属性是有限制的。*
        - 设置之前和之后元素的样式
        ```
        h2:before {content:" "}
        h2:after { }
        ```



