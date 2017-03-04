Servlet API：

* javax.servlet
* javax.servlet.http
* java.servlet.annotation
* javax.servlet.descriptor


####相关的类

* ServletRequest

* ServletResponse

* ServleteConfig：封装了通过@WebServlet或部署描述器传递给servlet的配置信息

* ServletContext：代表servlet应用，每个web应用只有一个上下文

* GenericServlet：抽象类，提供了Servlet接口中所有方法的默认实现，除了service方法声明是抽象的。

* HttpServlet

* HttpServletRequest

* HttpServletResponse


####使用部署描述器(Deployment Descriptor)


  		<web-app xmlns="http://java.sun.com/xml/ns/javaee"
        		xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
        		xsi:schemaLocation="http://java.sun.com/xml/ns/javaee http://java.sun.com/xml/ns/javaee/web-app_3_0.xsd"
        		version="3.0">
    		<servlet>
        		<servlet-name>SimpleServlet</servlet-name>
        		<servlet-class>SimpleServlet</servlet-class>
        		<load-on-startup>10</load-on-startup>
    		</servlet>
    		<servlet-mapping>
        		<servlet-name>SimpleServlet</servlet-name>
        		<url-pattern>/simple</url-pattern>
    		</servlet-mapping>
		</web-app>