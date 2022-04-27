Tomcat 处理一个HTTP请求的过程

```
1.用户在浏览器中输入网址localhost:8080/test/index.jsp，请求被发送到本机端口8080，被在那里监听的Coyote HTTP/1.1 Connector获得；

2.Connector把该请求交给它所在的Service的Engine（Container）来处理，并等待Engine的回应；

3.Engine获得请求localhost/test/index.jsp，匹配所有的虚拟主机Host；

4.Engine匹配到名为localhost的Host（即使匹配不到也把请求交给该Host处理，因为该Host被定义为该Engine的默认主机），名为localhost的Host获得请求/test/index.jsp，匹配它所拥有的所有Context。Host匹配到路径为/test的Context（如果匹配不到就把该请求交给路径名为“ ”的Context去处理）；

5.path=“/test”的Context获得请求/index.jsp，在它的mapping table中寻找出对应的Servlet。Context匹配到URL Pattern为*.jsp的Servlet，对应于JspServlet类；

6.构造HttpServletRequest对象和HttpServletResponse对象，作为参数调用JspServlet的doGet()或doPost(),执行业务逻辑、数据存储等；

7.Context把执行完之后的HttpServletResponse对象返回给Host；

8.Host把HttpServletResponse对象返回给Engine；

9.Engine把HttpServletResponse对象返回Connector；

10.Connector把HttpServletResponse对象返回给客户Browser。
```

