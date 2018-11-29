---
title: windows下 Anaconda 命令
tags: 
notebook: Python
---

# windows下 Anaconda 命令

>安装anaconda：除非你打算使用多个版本的Anaconda或者多个版本的Python，否则便勾选“Register Anaconda as my default Python 3.6”。

## 1. 环境信息
### 显示版本号。
`conda --version`

### 更新conda至最新版本
`conda update conda`

### 显示已创建的环境
`conda info --envs / conda env list / conda info -e`

## 2. 环境创建与删除
### 创建新环境
><env_name> 即创建的环境名。
<package_names> 即安装在环境中的包名>。
如果要在新创建的环境中创建多个包，则直接在<package_names>后以空格隔开，添加多个包名即可。

**`conda create --name <env_name> <package_names>`**
`conda create -n python3 python=3.5 numpy pandas`

### 切换环境
`activate <env_name>`

### 退出当前环境
`deactivate`

### 复制环境
`conda create --name <new_env_name> --clone <copied_env_name>`

### 删除环境
`conda remove --name <env_name> --all`

## 3. Package管理
### 显示当前环境已安装的包名和版本号。
`conda list `
### 在当前环境安装包
`conda install <package_name>`
### 为指定环境安装包
`conda install --name <env_name> <package_name>`
### 用pip安装包（对于conda无法安装的包）
`pip install <package_name>`
>1. pip只是包管理器，无法对环境进行管理。因此如果想在指定环境中使用pip进行安装包，则**需要先切换到指定环境中**，再使用pip命令安装包。
>2. pip无法更新python，因为pip并不将python视为包。
>3. pip可以安装一些conda无法安装的包；conda也可以安装一些pip无法安装的包。因此当使用一种命令无法安装包时，可以尝试用另一种命令。

### 更新所有包
`conda update --all` or `conda upgrade --all`
>建议：在安装Anaconda之后执行上述命令更新Anaconda中的所有包至最新版本，便于使用。
### 更新指定包
`conda update <package_name>` or `conda upgrade <package_name>`

### 卸载当前环境的包
`conda remove <package_name>`
### 卸载指定环境的包
`conda remove --name <env_name> <package_name>`
