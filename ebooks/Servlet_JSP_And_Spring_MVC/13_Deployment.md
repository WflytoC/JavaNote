部署描述器名称为`web.xml`，必须位于`WEB-INF`目录下，Java产生的`.class`文件放在`WEB-INF/classes`，Java库放在`WEB-INF/lib`下。



####部署描述器

`web-app`元素是根元素，可以声明下面的子元素：

* servlet声明、映射
* ServletContext初始化参数
* session配置
* listener类
* filter声明、映射
* MIME类型映射
* welcome文件列表
* error页
* JSP特定的设置
* JNDI设置


####核心元素

* `context-param`

		该元素将值传递给ServletContext，这些值可以在任意的servlet/JSP页面中读取。该元素必须包含param-name和param-value，可以选择性地包含description元素。

		<context-param>
			<param-name>location</param-name>
			<param-value>localhost</param-value>
		</context-param>

		<context-param>
			<param-name>port</param-name>
			<param-value>80</param-value>
			<description>The port number used</description>
		</context-param>
* `distributable`

		如果出现，该元素表明应用部署到分布式的servlet/JSP容器中。该元素内容必须是空的。
		
		<distributable />
* `error-page`：

		该元素包含HTTP错误码到资源路径的映射或者Java异常类型到资源路径的映射。该元素必须包含下面子元素：
			error-code：声明HTTP错误码
			exception-type：声明需要捕获的Java异常的名称
			location：声明资源路径，必须以/开头

		<error-page>
			<error-code>404<error-code>
			<location>/error.html</location>
		</error-page>

		<error-page>
			<exception-type>javax.servlet.ServletException<exception-type>
			<location>/exception.html</location>
		</error-page>
* filter

		该元素声明了servlet过滤器，至少要包含filter-name和filter-class元素。可以选择性地包含下面的元素：icon，display-name，description，init-param，async-supported。

		<filter>
			<filter-name>UpperFilter</filter-name>
			<filter-class>org.tcwee.UpperFilter</filter-class>
		</filter>

		<filter>
			<filter-name>ImageFilter</filter-name>
			<filter-class>org.tcwee.ImageFilter</filter-class>
			<init-param>
				<param-name>resolution</param-name>
				<param-value>1024</param-value>
			</init-param>
		</filter>
* filter-mapping

		该元素声明了filter应用到哪些资源上，一个Filter可以应用到Servlet或URL模式上。执行Filter的顺序与部署描述器中filter-mapping出现的顺序一致。

		该元素包含filter-name和url-pattern或servlet-pattern。

		<filter-mapping>
			<filter-name>UpperFilter<filter-name>
			<servlet-name>UpperServlet</servlet-name>
		</filter-mapping>

		<filter-mapping>
			<filter-name>ImageFilter<filter-name>
			<url-pattern>/*</url-pattern>
		</filter-mapping>
* `listener`

		该元素注册了监听器，它包含了listener-class元素，定义了监听器类

		<listener>
			<listener-class>com.ccmobile.AppListener</listener-class>
		</listener>




####Web片段(Fragment)

Web Fragment可以向存在的应用中添加插件或框架。Web Fragment通常是一个jar包(该文件放在WEB-INF/lib目录中)，包含一般的web对象，例如servlet、filter、listener或其它资源。Web Fragment可以有描述器，命名为web-fragment.xml，根元素为web-fragment。













