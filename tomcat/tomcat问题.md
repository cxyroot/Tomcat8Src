tomcat8 源码代码阅读笔记 作为一个发展有十多年的，广为使用的成熟的应用容器，tomcat还是有很多值得学习的。

我随便抛出一些技术点，看看这些问题你是否思考过？
1）如何让一个java程序成为一个类似于daemon这样的进程，在当前终端关闭后不退出，不同平台靠什么来解决这个问题？

Pipeline[StandardEngine[Catalina].StandardHost[localhost].StandardContext[/examples].StandardWrapper[RequestInfoExample]]
2）如何处理系统信号？

3）如何做监控？

3.2 是否使用jmx?

4）应用是怎么部署的？

5）servlet3有什么不同？

6）多个应用之间是怎么相互隔离的？

7）tomcat的classloader机制是怎样的？

6）servlet3和servlet3.1 新增的异步和非阻塞特性有什么用？

7）怎么预防应用可能导致的内存泄露？

8）关闭服务的时候，应该先暂停/关闭什么，后关闭什么？

9）tomcat的扩展机制是通过什么方式提供给开发者的？

10）BIO/NIO/APR 三种connector实现上的优劣是什么？

11）jsp文件是怎么编译和执行的？

12）HTTP协议本身就够喝一壶，tomcat7/8里支持的websocket/spdy等新特性本身就挺复杂的
tomcat有四五十万行代码，你没有目的的去看会比较耗费精力，
最好先了解大致结构，和运行流程，结合自己想要在某个点的实际需求去深入了解