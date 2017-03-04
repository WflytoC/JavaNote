####Spring Framework



* Core Container：Provides the IoC and Dependency Injection features.

* AOP and instrumentation：Provides AOP Alliance compliant features for weaving cross-cutting concerns in Spring applications.

* Messaging：Provides messaging abstraction over the Spring Integration project for messaging-based applications.

* Data access/integration：The data-access/integration layer consists of JDBC, ORM, OXM, JMS, and transaction modules.

* Web：Web technology abstraction over Spring MVC, web socket, and portlet APIs.

* Test：Unit testing and integration testing support with JUnit and TestNG frameworks.

Spring是模块化的

####Core Container

* spring-core
* spring-beans
* spring-context
* spring-context-support
* spring-expression


####AOP and Instrumentation

* spring-aop
* spring-aspects
* spring-instrument
* spring-instrument-tomcat


####Messaging

* spring-messaging

####Data Access/Integration

* spring-jdbc
* spring-tx
* spring-orm
* spring-oxm
* spring-jms


####Web

* spring-web
* spring-webmvc
* spring-websocket


####添加依赖项

gradle:

		compile('org.springframework:spring-context')    
		
		compile('org.springframework:spring-tx')    

		compile('org.hibernate:hibernate-entitymanager')

maven:

		<dependency>    
		
			<groupId>org.springframework</groupId>    

			<artifactId>spring-context</artifactId>    

			<version>${spring-framework.version}</version>  

		</dependency>

