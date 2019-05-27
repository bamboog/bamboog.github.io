### Servlet  （Server Applet）

```
所以, Tomcat 就是一个 Servlet 容器, 能接收用户从浏览器发来的请求,
 然后转发给 Servlet 处理, 把处理完的响应数据发回浏览器.

但是 Servlet 输出 Html, 还是采用了老的 CGI 方式 , 是一句一句输出,
 所以,编写和修改 html 非常不方便, 于是,
 Java Server Pages(JSP) 就来救急了, JSP 并没有增加任何本质上不能用 Servlet 实现的功能, 实际上 JSP 在运行之前,
 需要先编译成 Servlet, 然后才执行的.
```
