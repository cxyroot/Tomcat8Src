# Tomcat的两个核心组件：Connector和Container

## 1.Connector组件

​       Connector组件将在某个指定的端口上侦听客户请求，接收浏览器发过来的tcp连接请求，创建一个Request和一个Response对象分别用于和其你去端交换数据，然后会产生一个线程来处理这个请求并把产生的Request和Response对象传给Engine，从Engine中获得响应并返回给客户端。 Tomcat有两个经典的Connector，一个直接侦听来自浏览器的HTTP请求，另外一个侦听来自其他的WebServer的请求。Cotote HTTP/1.1 Connector在端口8080处侦听来自客户浏览器的HTTP请求，Coyote JK2 Connector在端口8009处侦听其他WebServer的Servlet/JSP请求。 Connector 最重要的功能就是接收连接请求然后分配线程让 Container来处理这个请求，所以这必然是多线程的，多线程的处理是 Connector 设计的核心。

## 2.Container组件

Container组件的体系结构如下：

![img](C:\Users\Administrator\AppData\Local\YNote\data\weixinobU7Vjo03UoHRcghQtLhICPwHV2o\7e43f811939540d6a9053ae9bcc6fd8d\1-783011696.jpeg)

**Container**

Container是容器的父接口，该容器的设计用的是典型的责任链的设计模式，它由四个自容器组件构成，分别是Engine、Host、Context、Wrapper。这四个组件是父子关系，存在包含关系。通常一个Servlet class对应一个Wrapper，如果有多个Servlet则定义多个Wrapper，如果有多个Wrapper就要定义一个更高的Container，如Context。 Context定义在父容器 Host 中，其中Host 不是必须的，但是要运行 war 程序，就必须要 Host，因为 war 中必有 web.xml 文件，这个文件的解析就需要 Host 了，如果要有多个 Host 就要定义一个 top 容器 Engine 了。而 Engine 没有父容器了，一个 Engine 代表一个完整的 Servlet 引擎。

**Engine**

Engine 容器比较简单，它只定义了一些基本的关联关系 Host 容器

**Host**

Host 是 Engine 的字容器，一个 Host 在 Engine 中代表一个虚拟主机，这个虚拟主机的作用就是运行多个应用，它负责安装和展开这些应用，并且标识这个应用以便能够区分它们。它的子容器通常是 Context，它除了关联子容器外，还有就是保存一个主机应该有的信息。

**Context**

Context 代表 Servlet 的 Context，它具备了 Servlet 运行的基本环境，理论上只要有 Context 就能运行 Servlet 了。简单的 Tomcat 可以没有 Engine 和 Host。Context 最重要的功能就是管理它里面的 Servlet 实例，Servlet 实例在 Context 中是以 Wrapper 出现的，还有一点就是 Context 如何才能找到正确的 Servlet 来执行它呢？ Tomcat5 以前是通过一个 Mapper 类来管理的，Tomcat5 以后这个功能被移到了 request 中，在前面的时序图中就可以发现获取子容器都是通过 request 来分配的

**Wrapper**

Wrapper 代表一个 Servlet，它负责管理一个 Servlet，包括的 Servlet 的装载、初始化、执行以及资源回收。Wrapper 是最底层的容器，它没有子容器了，所以调用它的 addChild 将会报错。 Wrapper 的实现类是 StandardWrapper，StandardWrapper 还实现了拥有一个 Servlet 初始化信息的 ServletConfig，由此看出 StandardWrapper 将直接和 Servlet 的各种信息打交道。

**说明：除了上述组件外，Tomcat中还有其他重要的组件，如安全组件security、logger日志组件、session、mbeans、naming等其他组件。这些组件共同为Connector和Container提供必要的服务。**