# Reactor和Proactor 
从Linux的角度看I/O操作需要经过两个过程：1、从存储设备中读取数据到内核缓存 2、从内核缓存读取数据到用户空间
    
平日里说的阻塞I/O和非阻塞I/O讲的是过程1，区别就是过程1是非阻塞（立即返回读取状态），还是阻塞（等待读取存储设备的数据到内核缓存后返回需要的数据）。

平日里说的同步I/O和异步I/O指的是过程2是否阻塞。


### Reactor模型
```同步非阻塞模型```，也称为Dispatch模型。

在Reactor模型中，Reactor负责管理所有的连接，它发现哪个连接有请求了就分配业务线程来处理。

分类：1、单Reactor单线程 2、单Reactor多线程 3、多Reactor多线程 

1、单Reactor单线程下，Reactor的select会一直监听事件，事件来了之后给dispatch分发，如果建立请求的事件则分配acceptor，由acceptor创建一个handler来处理后续的业务； 特点：单线程，同一时刻只有一个handler在工作，例如Redis用的就是这种方案，因为其处理业务够快，不用考虑并发问题；

2、单Reactor多线程，一个Reactor监听事件，但是handler不是阻塞的处理业务，而是开一个线程来处理，handler只负责读写，处理完成之后通知handler。

[这里有详细教程和epoll实现的示例程序: http://www.sean-bollin.com/category/c/](http://www.sean-bollin.com/category/c/)

### Proactor模型

...