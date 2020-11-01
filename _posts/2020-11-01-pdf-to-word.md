---
layout: post
title: PDF(包含数学公式)转word
categories: 其他
description: 将PDF中的数学公式完美的转成.doc格式
keywords: PDF，word，mathpix，pandoc，Typora
---


#  1. 说明
> - 个人需求：需要将一篇`pdf`格式的论文（包含很多的数学公式）转换成`.docx`格式。
> - 此方法对英文文献或资料支持非常好，对中文会有识别不出的情况。

# 2. 工具
- [mathpix](https://mathpix.com/)：用于截取pdf中的内容并识别其内容。
- [Typora](https://www.typora.io/)：Typora默认支持` .md`文件转 `.pdf`与` .html`格式，其余的常见格式需要使用 pandoc扩展程序来支持。
- [pandoc](https://www.pandoc.org/)：Typora中的一个扩展插件。

# 3. 实现
## 第一步：
- 下载并安装上述的三个工具。
> 注：
> - pandoc 若遇到下载失败等情况，这位博主提供了一份已经下载好的百度云链接[https://blog.csdn.net/jiajikang_jjk/article/details/80380133](https://blog.csdn.net/jiajikang_jjk/article/details/80380133)，同时这位博主也提供了详细的安装过程可供参考。
> - 工具安装完成后可在Typora中写一段话，然后将其转换成`.docx`格式（转换方法请看第四步）。若转成功，则说明 pandoc 扩展安装成功，否则失败。
## 第二步
- 勾选Typora中的内联公式，文件- 偏好设置-Markdown-内联公式。这主要用来识别话语之间的公式。![在这里插入图片描述](https://img-blog.csdnimg.cn/20201016130803393.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mzg2NjA2OA==,size_10,color_FFFFFF,t_70#pic_center)
## 第三步
- 打开 pdf文件。
- 打开 mathpix 软件，点击 左上角的电脑图标（快捷键：Ctrl+Alt+M），选中pdf中的内容。待 mathpix 软件中显示该内容时，将识别出的内容复制（Ctrl+C）到Typora中。![在这里插入图片描述](https://img-blog.csdnimg.cn/2020101613495658.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mzg2NjA2OA==,size_10,color_FFFFFF,t_70#pic_center)

## 第四步
- 导出文件为`.docx`格式。文件-导出-word(.docx)
![在这里插入图片描述](https://img-blog.csdnimg.cn/20201016135124992.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mzg2NjA2OA==,size_10,color_FFFFFF,t_70#pic_center)
# 4. 效果
- 转换前的 pdf 格式
![在这里插入图片描述](https://img-blog.csdnimg.cn/20201016135433325.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mzg2NjA2OA==,size_10,color_FFFFFF,t_70#pic_center)

- 转换后 `.doc`格式
![在这里插入图片描述](https://img-blog.csdnimg.cn/20201016135309340.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mzg2NjA2OA==,size_10,color_FFFFFF,t_70#pic_center)
# 参考
[https://blog.csdn.net/jiajikang_jjk/article/details/80380133](https://blog.csdn.net/jiajikang_jjk/article/details/80380133)




