---
layout: post
title: Jupyter在默认主题的基础上设置字体样式
categories: 开发环境
description: 根据个人习惯修改Jupyter的默认主题
keywords: Jupyter，主题
---



> 最近学习使用到了Jupyter，由于之前使用过vscode, pycharm，所以刚看到Jupyter的主题、字体等感觉很不爽，但是Jupyter又不能像pycharm那样设置主题和字体等。上网查了一下后试了两种方法：
> 第一种： 安装插件jupyter-themes。设置好后主题和字体等确实改变了，但是整体并不美观，而且暗黑色主题导致坐标数值看不太清...
> 第二种：由于Jupyter是一个网页，可自己根据需要设置css文件（C:\Users\xxx\.jupyter\custom\custom.css）。参考作者：[https://www.zhihu.com/question/40012144/answer/363009024](https://www.zhihu.com/question/40012144/answer/363009024)。

>自己可根据需要修改或添加css代码
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200701173411975.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mzg2NjA2OA==,size_16,color_FFFFFF,t_70)
```css
/* Body */
/*
#notebook-container {
    width: 70%
}
*/

/*navigate_menu*/
#navigate_menu {
    min-width: 200px;
	min-height: 100px;
	font-size: 13px;
}

/*header*/
body > #header #header-container {
	margin-left: 13px;
}
span.save_widget span.filename {
	color: #e22978;
}

/* Markdown */
div#notebook {
    font-family: san francisco, "PingFangSC-Medium", "Microsoft YaHei";
    line-height: 20px;
    -webkit-font-smoothing: antialiased !important;
}

/* Markdown - h */
div#notebook h2, h3, h4, h5, h6 {
    color: #007aff;
}

/*header  logo*/
.cm-header {
	margin: 2px 0;
}

/* Markdown - quote */
div#notebook blockquote{
    background-color: #f8f8f8;
    color: #505050;
    padding: 8.5px;
    margin: 0.5em -0.5em 0.5em -0.4em;
}

/* Markdown - code in paragraph */
div#notebook p code, div#notebook li code {
    font-family: Consolas, "PingFangSC-Medium", "Microsoft YaHei";
    font-size: 1em !important;
    color: #111111;
    border: 0.5px solid #cfcfcf;
    border-radius: 2px;
    background-color: #f7f7f7;
    padding: .1em .2em;
    margin: 0px 2px;
}

/* Markdown - code */
div.text_cell_render pre {
    border: 1px solid #cfcfcf;
    border-radius: 2px;
    background: #f7f7f7;
    line-height: 1.21429em;
    padding: 8.5px;
    margin: 0.5em -0.5em 0.5em -0.4em;
}
div.text_cell_render code {
    background: #f7f7f7;
}

/* Code */
div.CodeMirror pre {
    font-family: Consolas !important;
    font-size: 17px !important;
	/*padding: 3px !important;*/
    line-height: 140%;
    -webkit-font-smoothing: antialiased !important;
}

/* Code - output */
div.output pre {
    font-family: Consolas !important;
    line-height: 20px;
    -webkit-font-smoothing: antialiased !important;
	overflow-y: hidden;
}

/* Code - comment */
span.cm-comment {
    /*font-family: Consolas !important;
    font-style: normal !important;
	font:bold 12px/0.75em Consolas,STXingkai, SimHei;	
	color: #D91B78 !important;

*/
	font-size: 15px !important;
	font-family:Consolas,STXingkai, SimHei !important;   
	
}

/* Codes - comment   """ """*/
.cm-s-ipython span.cm-string {
    font-size: 15px !important;
}

/* Hinterland option*/
option {
	font-family: Consolas !important;
}

/*Table of Contents*/
#toc-wrapper .toc {
    font-family: Consolas, "PingFangSC-Medium", "Microsoft YaHei";
	font-size: 16px;
}


/* Code - highlighting */
.cm-s-ipython .CodeMirror-cursor {
    border-left: 1px solid #ff711a !important;
}
.cm-s-ipython span.cm-comment {
    color: #8d8d8d;
    font-style: italic;
}
.cm-s-ipython span.cm-atom {
    color: #055be0;
}
.cm-s-ipython span.cm-number {
    color: #ff8132;
}
.cm-s-ipython span.cm-property {
    color: #303030;
}
.cm-s-ipython span.cm-attribute {
    color: #303030;
}
.cm-s-ipython span.cm-keyword {
    color: #713bc5;
    font-weight: bold;
}
.cm-s-ipython span.cm-string {
    color: #009e07;
}
.cm-s-ipython span.cm-meta {
    color: #aa22ff;
}
.cm-s-ipython span.cm-operator {
    color: #055be0;
}
.cm-s-ipython span.cm-builtin {
    color: #e22978;
}
.cm-s-ipython span.cm-variable {
    color: #303030;
}
.cm-s-ipython span.cm-variable-2 {
    color: #de143d;
}
.cm-s-ipython span.cm-variable-3 {
    color: #aa22ff;
}
.cm-s-ipython span.cm-def {
    color: #e22978;
    font-weight: bold;
}
.cm-s-ipython span.cm-error {
    background: rgba(191, 97, 106, .40);
}
.cm-s-ipython span.cm-tag {
    color: #e22978;
}
.cm-s-ipython span.cm-link {
    color: #ff8132;
}
.cm-s-ipython span.cm-storage {
    color: #055be0;
}
.cm-s-ipython span.cm-entity {
    color: #e22978;
}
.cm-s-ipython span.cm-quote {
    color: #009e07;
}
div.CodeMirror span.CodeMirror-matchingbracket {
    color: #1c1c1c;
    background-color: rgba(30, 112, 199, .30);
}
div.CodeMirror span.CodeMirror-nonmatchingbracket {
    color: #1c1c1c;
    background: rgba(191, 97, 106, .40) !important;
}
.cm-s-default .cm-hr {
    color: #055be0;
}







```
