---
title: retainCount并不能返回正确的数值
layout: post

---



# retainCount并不能返回正确的数值

我想通过`retainCount`来理解引用计数，在网上搜了搜，看到了这个方法

相同意思的两行代码，却返回了不同的结果

```objc
NSDate *now = [NSDate date];
        NSDate *nowinit = [[NSDate alloc] init];
        NSLog(@"now = %@, retain count = %ld", now,
              CFGetRetainCount((__bridge CFTypeRef)(now)));
        NSLog(@"nowinit = %@, retain count = %ld", nowinit,
              CFGetRetainCount((__bridge CFTypeRef)(nowinit)));

```

retainCount的值

`[NSDate date]`输出的结果是2

`[[NSDate alloc] init]`输出的结果是1

这让我大为不解，从结果来看，他们是完全相同的，不应该会是这样，如果不同的话，其他人也应该会指出的，但我没发现有人说出来。

我尝试Google了一下，Google上第一个就是 [Cocoa中retainCount返回值不准的原因](http://blog.csdn.net/wzzvictory/article/details/9626017)这个，看了之后我才发现，Apple也说了，这个东西不准，我干，既然不准，这个方法还存在干嘛。我有看到[StackOverFlow](http://stackoverflow.com/questions/4636146/when-to-use-retaincount)上面的回答，他劝我们使用 Instruments 中的 Leaks 和 Zombies 来检测泄露的内存和僵尸对象。