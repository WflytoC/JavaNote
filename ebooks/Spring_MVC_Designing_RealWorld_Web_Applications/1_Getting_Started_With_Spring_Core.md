Spring基于【IoC容器】为Java开发提供了基础架构，IoC为应用提供了【DI】。

####IoC

IoC是一种设计原则，通过将依赖项的【创建和注入】交给外部组建，例如IoC容器，将对象与它们的依赖项分割开。

`Spring IoC`容器实现下面的接口：

* `org.springframework.beans.factory.BeanFactory`
* `org.springframework.context.ApplicationContext`


IoC容器管理的对象叫作beans，IoC容器会处理beans的装配和生命周期，beans定义在容器需要读取的配置文件中。


####配置元素据(Spring的配置文件)

* 基于XML的配置：可以创建一个根配置文件，然后导入代表其他层的配置文件：

	<beans ...>
		<import resource=""/xml-data-access-object.xml>
		...
	</beans>

* 基于注解的配置：bean的配置定义在bean自身的代码中，对类，字段或方法进行注解。

		@Controller("Greeter")
		public class GreetingServiceImpl implements GreetingService {}

		注解让GreetingServiceImpl成为bean，现在不用将它定义在XML文件中，但是应当指示IoC容器考虑注解：

		<context:component-scan base-package="" />


Spring提供了多种组件原型的beans注解：

* @Component
* @Service：服务层组件
* @Repository：在持久化层作为DAO
* @Controller：
* @RestController：处理Restful的特殊控制器


####Beans

Spring应用是由一系列执行特定功能的beans构成的，使用配置元数据(XML文件、注解)来定义beans。Spring bean的默认作用域是单例(singleton)。

Beans通过id属性或name属性来唯一标识，可以在应用的任何地方通过id属性或name属性来获取bean。如果bean的id或name没有提供的话，Spring会通过类型来自动装配(autowire)bean。


####Bean定义
		
		xml形式：

		<bean id="xmlTaskService" class="com...XmlDefinedTaskService" init-method="init" destroy-method="cleanup">
			<constructor-arg ref="userService" />
			<constructor-arg>
				<bean class="com...TaskInMemoryDAO"></bean>
			</constructor-arg>
		</bean>

		注解形式：

		@Service
		public class AnnotatedTaskService implements TaskService {
			@Autowired
			private UserService userService;
			@Autowired
			private TaskDAO taskDAO;
			
			@PostConstruct
			public void init() {}
			@PreDestroy
			public void destroy(){}

		}


####实例化beans

* 通过构造器：只要bean定义没有factory-method，该bean就是通过构造器来实例化的。
		
* 通过静态工厂方法：相同类中的静态方法，被标记为`factory-method`，该方法被调用来创建实例。


		<bean id="Greeter" class="...GreetingBean" factory-method"newInstance"/>
* 通过实例工厂方法：

		<bean id="greeter" factory-bean="serviceFactory" factory-method="createGreeter" />
		<bean id="serviceFactory" class="...ServiceFactory" />


####注入bean的依赖项

IoC容器的主要目的是解析对象的依赖项。

* 基于构造器

		<bean id="taskService" class="com...SimpleTaskService">
			<constructor-arg ref="userService" />
			<constructor-arg ref="taskDAO" />
		</bean>
* 基于setter方法

		<bean id="systemSettings" class="com..SystemSettings">
			<property name="OpenUserTasksMaxLimit" value="5" />
		</bean>
* 自动装配依赖项

		Spring可以自动装配bean的依赖项，通过检查bean定义。Spring支持四种自动装配模式：no,byName,byType,constructor。

		Spring bean的默认装配是byType。如果你自动装配一个接口，Spring会寻找该接口的实现(实现类被配置为Spring bean)。

		自动装配可以与@Qualifier注解共同工作：

		@Autowired
		@Qualifier("taskDAO")
		private UserService userService;


####Bean作用域

* singleton
* prototype：每次请求bean时，新的实例都会被创建
* request
* session
* globalSession
* application


在XML中定义：

		<bean id="userPreferences" class="class...UserPreferences" scope="session">...</bean>

使用注解：

		@Component
		@Scope("request")
		public class TaskSearch{....}








	

