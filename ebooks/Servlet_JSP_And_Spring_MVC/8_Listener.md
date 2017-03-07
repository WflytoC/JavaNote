Servlet API提供了一系列事件类(继承自java.util.Event)和监听器接口(分为三种不同的级别：ServletContext、HttpSession、ServletRequest)。

####监听器接口及其注册

* ServletContextListener：监听Servlet上下文(创建和关闭)的生命周期事件。

* ServletContextAttributeListener

* HttpSessionListener：

* HttpSessionAttributeListener

* HttpSessionActivationListener

* HttpSessionBindingListener
* ServletRequestListener：监听ServletRequest的创建与移除

* ServletRequestAttributeListener

* AsyncListener

创建监听器，只需要创建一个实现上面接口的Java类，有两种方法来注册监听器：

* 使用WebListener注解

		@WebListener
		public class ListenerClass implements ListenerInterface{}
* 在部署描述器中使用listener元素

		<listener>
			<listener-class>..</listener-class>
		</listener>


