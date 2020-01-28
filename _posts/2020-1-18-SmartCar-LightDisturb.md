---
layout:     post                    # 使用的布局（不需要改）
title:     阳光算法  # 标题 
subtitle:   Method for disturbing light in Smart Car. #副标题
date:       2020-01-18              # 时间
author:     ZK                      # 作者
header-img: img/post-bg-2015.jpg    #这篇文章标题背景图片
catalog: true                       # 是否归档
tags:
   - NXP Smart Car   	#标签
---

# 阳光算法方案

> 简介：用卷积核来实现边缘增强，用以处理阳光强烈时导致的边缘模糊

## 1.目前问题

​		在阳光干扰的路段，对原始图像直接进行全局二值化会导致大片道路边缘信息丢失。而对于后提出的分块二值化，若处理的局部图像分布于路中，会导致设定的阈值产生近乎一般黑一般白，影响中线提取。

## 2.解决方案

​		先采用如下卷积算子预处理图像，在此基础上进行二值化，最后中线提取。相比于直接二值化，本方案可保留丰富的边缘信息。![卷积.jpg](https://i.loli.net/2020/01/28/yqcUtmAHxDdGYNF.jpg)

## 3.效果展示

* 传统处理

![对比三.jpg](https://i.loli.net/2020/01/28/XNVtnJG6bivfO7l.jpg)

* 卷积算子

![对比2.jpg](https://i.loli.net/2020/01/28/249g8Ut6FIcQGCn.jpg)



## 4.代码部分

```python
import cv2 as cv
import numpy as np

def custom_blur_demo(image):	# 自定义卷子算子
    kernel = np.array([[0, 1, 0],[1, -4, 1],[0, 1, 0]], np.float32)
    dst = cv.filter2D(image, -1, kernel=kernel)
    cv.imshow("custom_blur_demo", dst)
    return dst

def threshold_demo(image):		# 图像二值化
    gray = cv.cvtColor(image, cv.COLOR_BGR2GRAY)
    ret, binary = cv.threshold(gray, 127, 255, cv.THRESH_BINARY|cv.THRESH_OTSU)
    print("threshold value %s"%ret)
    cv.imshow("binary", binary)

print("--------- Hello Python ---------")
src = cv.imread("D:/Zack/Desktop/DataSet/lightDistur/2.BMP")
cv.namedWindow("input image", cv.WINDOW_AUTOSIZE)
cv.imshow("input image", src)
dst = custom_blur_demo(src)
threshold_demo(src)
cv.waitKey(0)
cv.destroyAllWindows()
```

## 5.算法复杂度分析

​		只取一行来提取中点时：

* 80 * 180图像：计算量为180次乘法，900次加法。
* 缩小至到16 * 30时，计算量为30次乘法，150次加法。

## 6.缺陷

​		无法补全过度曝光严重而导致边缘信息完全丢失的道路图像。
