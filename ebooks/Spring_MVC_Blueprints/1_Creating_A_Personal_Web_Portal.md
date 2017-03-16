####添加依赖项：

		dependencies {
    		testCompile group: 'junit', name: 'junit', version: '4.11'
    		compile group: 'org.springframework', name: 'spring-webmvc', version: '4.1.2.RELEASE'
    		compile group: 'javax.servlet', name: 'javax.servlet-api', version: '3.1.0'
    		compile group: 'javax.servlet.jsp', name: 'javax.servlet.jsp-api', version: '2.3.1'
    		compile group: 'javax.servlet', name: 'jstl', version: '1.2'
    		compile group: 'javax.mail', name: 'mail', version: '1.4.7'
		}

####相关配置

*   配置DispatcherServlet

		    <servlet>
        		<servlet-name>springmvc</servlet-name>
        		<servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>
				<init-param>
            		<param-name>contextConfigLocation</param-name>
            		<param-value>/WEB-INF/configs/springmvc-servlet.xml</param-value>
        		</init-param>
    		</servlet>

    		<servlet-mapping>
        		<servlet-name>springmvc</servlet-name>
        		<url-pattern>*.html</url-pattern>
    		</servlet-mapping>
*   创建Spring容器

		<?xml version="1.0" encoding="UTF-8"?>
		<beans xmlns="http://www.springframework.org/schema/beans"
      		 xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       		 xmlns:context="http://www.springframework.org/schema/context"
       		 xmlns:mvc="http://www.springframework.org/schema/mvc"
      		 xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans-4.1.xsd
                           http://www.springframework.org/schema/context http://www.springframework.org/schema/context/spring-context-4.1.xsd
                           http://www.springframework.org/schema/mvc http://www.springframework.org/schema/mvc/spring-mvc-4.1.xsd">
        		<mvc:annotation-driven />
        		<context:component-scan base-package="controller" />
        		<mvc:default-servlet-handler />
        		<mvc:resources mapping="/css/**" location="/css/" />
		</beans>

