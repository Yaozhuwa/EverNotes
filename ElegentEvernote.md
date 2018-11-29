---
title: VScode编辑同步Markdown文档到印象笔记
tags: Blog, Elegent
notebook: Elegent
---
# VScode编辑同步Markdown文档到印象笔记

## 第一步 下载VSCode
到[Visual Studio Code官网](https://code.visualstudio.com/)下载VSCode，并安装

## 第二步 安装VScode相关插件
需要两个插件：
> 1. *evermonkey*: 印象笔记同步插件
> 2. *Markdown Preview Enhenced*: md文件实时预览插件

1. 打开vscode如下图步骤搜索安装evermonkey插件
![安装evermonkey](http://yaozhuwa-bucket.oss-cn-beijing.aliyuncs.com/18-10-23/81970806.jpg)
安装结束后Reload
![Reload插件](http://yaozhuwa-bucket.oss-cn-beijing.aliyuncs.com/18-10-23/72779411.jpg)
2. 安装Markdown Preview Enhenced插件
同理安装好Markdown Preview Enhenced插件并Reload。此时软件及插件安装部分完成。

## 第三步 绑定印象笔记账号

在vscode中使用快捷键`Ctrl+Shift+P`调出命令，输入ever，查找命令`Ever Token: Open developer page to get API token`，回车
此时会自动打开默认浏览器并跳出[印象笔记Develooper Tokens](https://app.yinxiang.com/api/DeveloperToken.action)界面。
复制自己的Token值，回到vscode界面，按自己印象笔记账号的版本选择china或者international。按提示粘贴自己的Token和NoteStore URL。
> **Notice**：如果你的页面显示无法申请Develooper Tokens，只需要使用帐户注册邮箱直接发送邮件到 online-help@yinxiang.com ，并说明需要开启Token即可，会有工作人员帮你开放。

## 第三步 开始使用VScode来编辑并同步Markdown笔记到Evernote

VScode界面，使用快捷键`Ctrl+Shift+P`调出命令，输入ever，查找命令到`Ever New: Create a new empty note with markdown supported and...`，回车
![Ever New](http://yaozhuwa-bucket.oss-cn-beijing.aliyuncs.com/18-10-23/54767132.jpg)
vscode会创建一个md文件，如下

![](http://yaozhuwa-bucket.oss-cn-beijing.aliyuncs.com/18-10-23/2854149.jpg)
> 注：橙色字体部分是我自己添加的，你只需要`Ctrl+S`保存文件，并且在`title`后填入笔记名称，`tags`后填入你想要为笔记添加的标签，最后`notebook`后是你自己要保存到的目标笔记本的名称。

编辑markdown笔记的时候，鼠标右键选择`Markdown Preview Enhenced: Open Preview`来让你可以实时预览你的笔记的效果。大致效果如图：
![笔记预览效果图](http://yaozhuwa-bucket.oss-cn-beijing.aliyuncs.com/18-10-23/22568677.jpg)

下面你就可以开始编辑你的Markdwon笔记了。

**同步笔记**的方法也很简单，当你编辑完笔记，同样使用快捷键`Ctrl+Shift+P`调出命令，输入ever publish，查找到命令`Ever publish: Publish current editting note to Evernote server.`，回车，笔记就会上传到你的印象笔记笔记本中，同步完成！

Evermonkey插件的更多使用命令可以自行探索或者查阅官方文档。
## 第四步 使用图床让笔记可以添加图片

我用的是极简图床，打开[极简图床](http://jiantuku.com/#/)，按照极简图床的[帮助文档](https://shimo.im/docs/vbmdsh2LSwoo628P/)注册好阿里云账号并按要求绑定自己的阿里云账号。
使用方式非常简单：把图片拖到/粘贴到极简图床，它将自动成成图片的网址，如下，你只需要按下按钮，就可以将图片网址复制到剪切板。
![极简图床使用](http://yaozhuwa-bucket.oss-cn-beijing.aliyuncs.com/18-10-23/94504263.jpg)

> 截图软件强烈推荐[snipaste](https://www.snipaste.com/)!

这下，你就可以非常愉快地记笔记了！
## 第五步 最后的遗留问题

可惜，事情还没做到完美。我还暂时没有找到让Evernote笔记支持Latex公式的方法。