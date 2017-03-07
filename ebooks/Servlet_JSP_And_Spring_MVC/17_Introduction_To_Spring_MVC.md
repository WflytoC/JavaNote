####DispatcherServlet

`Spring MVC`提供了一个`dispatcher servlet`，全名是`org.springframework.web.servlet.DispatcherServlet`。为了使用该servlet，需要在部署描述器(`web.xml`)中配置它。

		<servlet>
			<servlet-name>springmvc</servlet-name>
			<servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>
			<load-on-startup>1</load-on-startup>
		</servlet>

		<servlet-mapping>
			<servlet-name>springmvc</servlet-name>
			<!--  将所有的请求映射到DispatcherServlet -->
			<url-pattern>/</url-pattern>
		</servlet-mapping>

在`DispatcherServlet`初始化时，它会在应用的`WEB-INF`目录下寻找配置文件，XML文件命名遵循规则`servletName-servlet.xml`.但是，你可以将配置文件放在应用的任何地方，前提是你需要在servlet声明中使用`init-param`元素来告诉`DispatcherServlet`。

		<servlet>
			<servlet-name>springmvc</servlet-name>
			<servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>
			<init-param>
				<param-name>ContextConfigLocation</param-name>
				<param-value>/WEB-INF/config/simple-config.xml</param-value>
		
			</init-param>
		</servlet>



####Controller接口

Spring2.5之前，编写控制器唯一的方法是实现`org.springframework.web.servlet.mvc.Controller`接口。该接口暴露了handleRequest方法，该方法签名为：

		ModelAndView handleRequest(HttpServletRequest request,HttpServletResponse response)

该方法返回的ModelAndView包含了[一个视图路径]或者[一个视图路径和一个模型]。

实现Controller接口的控制器只能处理单个动作。


####创建基本的SpringMVC应用

* 引入SpringMVC的依赖项

		compile group: 'javax.servlet', name: 'javax.servlet-api', version: '3.1.0'
    	
		compile group: 'org.springframework', name: 'spring-webmvc', version: '4.1.2.RELEASE'
* 添加web.xml配置文件和SpringMVC的配置文件

		web.xml文件

		<?xml version="1.0" encoding="UTF-8"?>
		<web-app xmlns="http://xmlns.jcp.org/xml/ns/javaee"
         	xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         	xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee http://xmlns.jcp.org/xml/ns/javaee/web-app_3_1.xsd"
         	version="3.1">
    	<servlet>
        	<servlet-name>springmvc</servlet-name>
        	<servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class> 
        	<init-param>
            	<param-name>contextConfigLocation</param-name>
            	<param-value>/WEB-INF/config/springmvc-servlet.xml</param-value>
        	</init-param>//如果不是通过Servlet初始化参数显式指定SpringMVC配置文件，则配置文件需要放在/WEB-INF下面
    	</servlet>

    	<servlet-mapping>
        	<servlet-name>springmvc</servlet-name>
        	<url-pattern>/</url-pattern>
    	</servlet-mapping>
		</web-app>

		
		springmvc-servlet.xml文件
		
		<?xml version="1.0" encoding="utf-8" ?>
		<beans xmlns="http://www.springframework.org/schema/beans"
    		xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    		xsi:schemaLocation="http://www.springframework.org/schema/beans
    		http://www.springframework.org/schema/beans/spring-beans.xsd">
    		<bean name="/product_input.action" class="controller.InputProductController"/>
    		<bean name="/product_save.action" class="controller.SaveProductController"/>
    		<bean id="viewResolver" class="org.springframework.web.servlet.view.InternalResourceViewResolver">
        		<property name="prefix" value="/WEB-INF/jsp/"/>
        		<property name="suffix" value=".jsp"/>
    	</bean>
		</beans>
		
* 编写控制器类，实现Controller接口，并将该控制器类作为bean配置在SpringMVC配置文件中，其中，name是需要映射的路径。

* 配置视图解析器

