---
title: C++ 全局变量 命名空间中的变量的声明和定义
tags: C++
notebook: C++
---
# C++ 全局变量 命名空间中的变量的声明和定义
## 全局变量
>全局变量，以关键字`extern`在一个头文件声明，在一个cpp文件中定义（赋值）。

其他文件引用该变量的方式有两种：
1. 是通过 `extern`声明引用
2. 包含这个头文件。

## 命名空间中的变量的声明和定义
>在声明命名空间的头文件中，加`extern`声明，在cpp中定义（赋值）。

声明如下：
```cpp
//test.h
#pragma once

namespace testSpace{
    extern int testVarInt;
}
```
定义如下：
```cpp
//test.cpp
#include "test.h"

namespace testSpace{
    int testVarInt = 0;
}
```
其他文件只要`#include "test.h"`就可以使用`testSpace::testVarInt`。