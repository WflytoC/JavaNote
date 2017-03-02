####引入依赖项：

	compile group: 'org.springframework', name: 'spring-web', version: '4.1.2.RELEASE'
    compile group: 'org.springframework', name: 'spring-webmvc', version: '4.1.2.RELEASE'
    compile group: 'org.springframework', name: 'spring-context', version: '4.1.2.RELEASE'
    compile group: 'org.springframework', name: 'spring-context-support', version: '4.1.2.RELEASE'
    compile group: 'org.springframework', name: 'spring-tx', version: '4.1.2.RELEASE'
    compile group: 'javax.servlet', name: 'javax.servlet-api', version: '3.1.0'
    compile group: 'javax.servlet.jsp', name: 'javax.servlet.jsp-api', version: '2.3.1'
    compile group: 'javax.servlet', name: 'jstl', version: '1.2'
    compile group: 'commons-logging', name: 'commons-logging', version: '1.1.3'


####配置web.xml文件

	<?xml version="1.0" encoding="UTF-8"?>
	<web-app xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xmlns="http://java.sun.com/xml/ns/javaee" xmlns:web="http://java.sun.com/xml/ns/javaee"
         xsi:schemaLocation="http://java.sun.com/xml/ns/javaee http://java.sun.com/xml/ns/javaee/web-app_3_0.xsd"
         id="WebApp_ID" version="3.0">
    <display-name>Personal</display-name>

    	<servlet>
        	<servlet-name>center</servlet-name>
        	<servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>
        	<load-on-startup>1</load-on-startup>
    	</servlet>

    	<servlet-mapping>
        	<servlet-name>center</servlet-name>
        	<url-pattern>*.html</url-pattern>
    	</servlet-mapping>
    	<servlet-mapping>
        	<servlet-name>center</servlet-name>
        	<url-pattern>/</url-pattern>
    	</servlet-mapping>
    	<mime-mapping>
        	<extension>png</extension>
        	<mime-type>image/png</mime-type>
    	</mime-mapping>

	</web-app>


####配置Spring容器

	<?xml version="1.0" encoding="UTF-8"?>
	<beans xmlns="http://www.springframework.org/schema/beans"
       		xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:aop="http://www.springframework.org/schema/aop"
       		xmlns:context="http://www.springframework.org/schema/context"
       		xmlns:tx="http://www.springframework.org/schema/tx"
       		xmlns:mvc="http://www.springframework.org/schema/mvc"
       		xsi:schemaLocation="http://www.springframework.org/schema/aop http://www.springframework.org/schema/aop/spring-aop-4.1.xsd
				http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans-4.1.xsd
				http://www.springframework.org/schema/tx http://www.springframework.org/schema/tx/spring-tx-4.1.xsd
				http://www.springframework.org/schema/context http://www.springframework.org/schema/context/spring-context-4.1.xsd
				http://www.springframework.org/schema/mvc http://www.springframework.org/schema/mvc/spring-mvc-4.1.xsd">

			<!-- 容器自动扫描组件类 -->
    		<context:component-scan base-package="com.tcwee.personal.web.portal" />
    		
			<!-- 允许在类中使用注解 -->
			<mvc:annotation-driven />
    		
			<mvc:default-servlet-handler />
    
			<!-- 使用特定的URL来指向静态资源的位置 -->
			<mvc:resources mapping="/css/**" location="/style/" />

			<!--  第一种视图解析，需要创建.properties文件 -->
    		<bean id="viewResolver"
          		class="org.springframework.web.servlet.view.ResourceBundleViewResolver">
        			<property name="basename">
            			<value>config.views</value>
        			</property>
    		</bean>

			<!--  第二种视图解析 -->
			<bean 
				class="org.springframework.web.servlet.view.InternalResourceViewResolver">  
        			<property name="prefix" value="/WEB-INF/views/"/>  
        			<property name="suffix" value=".jsp"/>  
    		</bean> 
	</beans>