---
title: TableView和CollectionView整体上移64pt问题
layout: post
---



两个解决方案

1. self.automaticallyAdjustsScrollViewInsets = NO  这个是有效的，但是会影响其他页面
2. 在切换视图的ViewController中，切换完视图就更改响应ViewController的frame

最后的解决方法是修改了所有子View的Y值