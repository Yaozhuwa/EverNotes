---
title: Win10 Anaconda 安装 tensorflow -gpu版本
tags: 深度学习
notebook: B1-DeepLearning
---
# Win10 Anaconda 安装 tensorflow GPU 版本

## 一、安装CUDA和cudnn
首先要根据自己的gpu情况下载对应版本的CUDA安装包和cudnn。并不是有GPU就可以使用tensorflow。
>重点就在这里，不是所有的cuda都适用于你的显卡，也不是所有cuda都和将要安装的tensorflow匹配！就在这里需要搞清楚2件事情:
>
>第一，你的显卡适合什么cuda?
>
>第二，cuda需要配套什么tensorflow?
>——引用自：[深度学习环境搭建：win10+GTX1060 + tensorflow1.5+keras+cuda9.0+cudnn7](https://blog.csdn.net/qq_33856151/article/details/79295086)

确定你需要的CUDA版本：[TENSORFLOW：检查显卡支持哪个版本的CUDA](https://www.cnblogs.com/yingchuan-hxf/p/7710071.html)

官方的tensorflow-gpu包只支持CUDA9.0版本，而我的笔记本gpu适用于CUDA10.0版本。需要自己重新编译，这里我使用了网上别人编译好的.whl文件。参考链接：[在CUDA10的环境下安装支持gpu的tensorflow版本（亲测有效）](https://blog.csdn.net/weixin_38538282/article/details/84625937)

CUDA10.0及对应版本的cudnn的安装：[Win10安装CUDA10和cuDNN](https://blog.csdn.net/qq_37296487/article/details/83028394)

## 二、Conda 换源
找到.condarc文件，改成如下设置：
```
ssl_verify: true
channels:
  - https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/main/
  - https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/free/
show_channel_urls: true
```
## 三、安装tensorflow
1. 打开 Anaconda prompt，创建新的环境
`conda create -n tf36 python=3.6`
2. 更新`pip`
`python -m pip install --upgrade pip`
### pip安装
安装tensorflow GPU版本
`pip install --ignore-installed --upgrade tensorflow-gpu`
安装CPU版本命令如下
`pip install --upgrade --ignore-installed tensorflow`
### conda安装
conda 安装tensorflow：
`conda install tensorflow-gpu`

conda 安装CPU版本命令：
`conda install tensorflow`
### 自编译的.whl文件安装
下载得到[.whl文件](https://download.csdn.net/download/weixin_38538282/10816219)，然后再进入到该目录下，输入`pip install tensorflow-1.12.0rc0-cp36-cp36m-win_amd64.whl`命令即可。

## 四、安装pylint
Pylint 是一个 Python 代码分析工具，它分析 Python 代码中的错误，查找不符合代码风格标准  
`conda install pylint`

