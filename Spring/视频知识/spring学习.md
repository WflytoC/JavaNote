####Spring概念

两部分核心：

* AOP

		面向切面编程，扩展功能不是修改源代码实现
* IoC

		调用一个类的方法(非静态)，那么创建该类的对象(使用new方法)；而IoC把对象交给Spring配置创建。

一站式框架：

* Spring在javaEE三层结构中，每一层都提供了不同的解决技术；

		1.Web层：SpringMVC
		2.Service层：Spring的IoC
		3.DAO层：Spring的jdbcTemplate

####IoC操作

* 把对象的创建交给Spring进行管理
* IoC操作两种方式：

		1.配置文件方式
		2.注解方式
* IoC底层原理

		1.xml配置文件
		2.dom4j解析xml
		3.工厂设计模式
		4.反射

####IoC入门

* 导入依赖项jar包

* 创建类，在类里编写方法

* 创建Spring配置文件，配置创建的类

		spring核心配置文件名称和位置不固定，官方建议名称为applicationContext.xml

####Bean实例化的方式

* 使用类的无参数构造创建

		<bean id="bean1" class="bean.Bean1"></bean>
* 使用静态工厂创建

		<bean id="bean2" class="bean.Bean2Factory" factory-method="getBean2">
* 使用实例工厂创建

		<bean id="bean3Factory" class="bean.Bean3Factory"></bean>
    	<bean id="bean3" factory-bean="bean3Factory" factory-method="getBean3"></bean>

####Bean标签

* id属性：

		Bean的名称，在代码中可以根据id值获取配置的对象
* class属性

		
* name属性

		功能和id一样
* scope属性

		1.singleton：默认值，单例
		2.prototype：多例
		3.request
		4.session
		5.globalSession


####属性注入

概念：创建对象时，对类的属性设置值

属性注入的方式：

* 使用set方法注入

		    <bean id="book" class="props.Book">
        		<property name="bookName" value="三国演义"></property>
    		</bean>

* 有参数的构造方法注入

		    <bean id="prop1" class="props.PropertyDemo1">
        		<constructor-arg name="username" value="wflytoc"></constructor-arg>
    		</bean>
* 使用接口注入

复杂属性的注入：

* 注入对象类型属性(重点)

		    <bean id="userDao" class="ioc.UserDAO"></bean>
    		<bean id="userService" class="ioc.UserService">
        		<property name="userDAO" ref="userDao"></property>
    		</bean>
* 注入复杂类型属性


    	<bean id="person" class="props.Person">
        	<property name="pname" value="wflytoc"></property>
        	<!--数组属性注入-->
        	<property name="arrs">
            	<list>
                	<value>A</value>
                	<value>B</value>
                	<value>C</value>
            	</list>
        	</property>
        	<!--List类型属性注入-->
        	<property name="list">
            	<list>
                	<value>a</value>
                	<value>b</value>
                	<value>c</value>
            	</list>
        	</property>
        	<!--Map类型属性注入-->
        	<property name="map">
            	<map>
                	<entry key="a" value="A"></entry>
                	<entry key="b" value="B"></entry>
                	<entry key="c" value="C"></entry>
            	</map>
        	</property>
        	<!--Properties类型属性注入-->
        	<property name="properties">
            	<props>
                	<prop key="driverClass">com.mysql.jdbc.Driver</prop>
                	<prop key="username">root</prop>
            	</props>
        	</property>
    	</bean>



####IoC和DI区别

* IoC：控制反转，把对象的创建交给Spring进行配置

* DI：依赖注入，向类里面的属性中设置值

* 两者关系：依赖注入不能单独存在，需要在IoC基础之上完成操作


####Spring整合Web项目原理

在服务器启动的时候，为每个项目创建`ServletContext`对象。

* 在ServletContext对象创建的时候，使用监听器来监听该对象创建的时间

* 加载Spring配置文件，利用该配置文件创建对象；

* 把创建出来的对象放到ServletContext域对象里面(利用setAttribute方法)

* 需要使用对象时，从ServletContext域中获取(getAttribute方法)