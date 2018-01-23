# [先弄清楚这里的学问，再来谈 iOS 内存管理与优化（一）](https://www.jianshu.com/p/deab6550553a)

## 内存有分类吗？什么类型的内存可以回收？

[What is resident and dirty memory of iOS?](https://stackoverflow.com/questions/13437365/what-is-resident-and-dirty-memory-of-ios!)

* Clean Memory：在闪存中有备份，能够再次读取。主要包括system framework、binary executable of your app、memory mapped files
* Dirty Memory：所有非Clean Memory，系统无法回收。包括Heap allocation、caches、decompressed images

## 内存之间的关系是什么呢？

* 虚拟内存层面：virtual memory = clean memory + dirty memory
* 物理内存层面：resident memory= dirty memory+clean memory that loaded in physical memory
* 总结virtual memory == \(clean memory + dirty memory\) &gt; resident memory &gt;dirty memory

## 虚拟内存是做啥的？

```
// clean memory
char *buf = malloc(100*1024*1024)

// dirty memory
for(int i=0; i < 3*1024*1024; ++i){
    buf[i] = rand()
}
```

## 使用Allocations工具来验证刚才的说法

![](/assets/import.png)

All Heap & Anoymous VM可以一起来看，代表分配的所有虚拟内存，Dirty Size就是刚才讲的Dirty Memory，resident Size就是物理内存的大小

## 虚拟内存 VS 物理内存

![](/assets/import1.png)

## 为什么桌面系统中很少有应用因为内存过多而被Kill掉，但是iOS会呢？

移动设备（包括苹果、安卓等），无Swap机制，主要是由于移动设备的闪存容量很有限，并且闪存的频繁读写很降低寿命

## iOS内存管理机制是怎样的？基于什么原则来Kill掉进程呢？

![](/assets/import2.png)

# [先弄清楚这里的学问，再来谈 iOS 内存管理与优化（二）](https://www.jianshu.com/p/f95b9bfda4a0)

## Strong Weak Dance

## 降低内存峰值

#### Lazy Allocation

#### 图片的读取

#### NSData & 内存映射文件

#### 其他方式

[庄延军老师的分享](https://link.jianshu.com/?t=http://www.imooc.com/video/11076)

#### NSAutoReleasePool

#### AutoReleasePool

#### 简单总结

* Lazy Allocation
* 图片的读取的正确方式
* NSData & 内存映射文件
* callocVS malloc + memset
* 栈内存分配
* autoReleasePool

## 内存警告处理

* 尽可能多的释放资源，尤其是图片等占用内存多的资源
* 单例模式的滥用，会导致单例对象一直持有资源



