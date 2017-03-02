利用IntelliJ创建Gradle工程：

####工程目录

src/main目录下的结构：

* java：存放java相关文件
* resources
* webapp:存放web相关文件


webapp/WEB-INF目录下的结构:

* web.xml：对工程进行相关配置


####开发流程

1. 利用IDE创建工程
2. 引入依赖项
3. 在xml文件中进行配置


####

* 本质上是由servlet来处理用户请求的

		配置servlet
		
		<servlet>
			<servlet-name>appServlet</servlet-name>
			<servlet-class>xxxx</servlet-class>
			<init-param>
				<param-name>xxx</param-name>
				<param-value>xxx</param-value>
			</init-param>
		</servlet>

		<servlet-mapping>
			<servlet-name>appServlet</servlet-name>
			<url-pattern>/</url-pattern>
		</servlet-mapping>
* 
