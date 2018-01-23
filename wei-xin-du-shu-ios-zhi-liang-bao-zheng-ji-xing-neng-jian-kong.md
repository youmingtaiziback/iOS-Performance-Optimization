# [微信读书 iOS 质量保证及性能监控](http://wereadteam.github.io/2016/12/12/Monitor/)

## 对网络层成功率的监控 {#对网络层成功率的监控}

统计网络请求的成功、失败率，了解所有错误码的分布情况

## 数据层的性能监控 {#数据层的性能监控}

数据层框架是[GYDataCenter](https://wereadteam.github.io/2016/07/06/GYDataCenter/)

## UI数据源监控 {#UI数据源监控}

我们只需hook了UIDataSource的alloc、NSMutableArray的add等方法，当调用NSMutableArray的add方法时，去遍历所有UIDataSource对象，通过class\_copyIvarList、valueForKey函数把所有的成员变量都找出来看看是否为当前的NSMutableArray，通过NSAssert确保当前在主线程，否则在debug模式下会crash提醒开发者修改

## UI主线程监控 {#UI主线程监控}

#### 防止子线程访问UI

hook掉UIView、CALayer的setNeedsLayout、setNeedsDisplay、setNeedsDisplayInRect:三个方法

#### FPS监控

[demo](https://github.com/featuretower/GYMonitor)

#### 线上用户监控

使用RDM sdk来监控，原理是通过RunLoop的几个Observer来确定主线程是否卡住了

## 业务实时监控 {#业务实时监控}

## 统计Assert断言 {#统计Assert断言}

发布环境下Assert是默认不生效的，需要使其生效

如何捕捉所有的Assert

* NSAssertionHandler线程相关
* 重写NSAssert宏，可能会引起未知问题

* 自己包装NSAssert，使用plcrashreporter这个库来获取堆栈的

## 总结 {#总结}



