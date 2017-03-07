过滤器拦截请求，并处理ServletRequest和ServletResponse。

过滤器用到的接口：

* Filter：过滤器类必须要实现该接口

		该接口暴露了过滤器的三个周期方法：
			init：只调用一次，在应用启动时doFilter：每次与该过滤器相关联的资源被调用时，该方法就会被调用
			destroy：应用停止时调用

* FilterConfig

* FilterChain

####配置过滤器

目的：

* 决定过滤器拦截哪些资源
* 搭建传递给过滤器init方法的初始值
* 给过滤器名称

配置方法：

* 注解：

		@WebFilter(fileName="",urlPatterns= {/*})
* 部署描述器：

		<filter>
			<filter-name>LoggerFilter</filter-name>
			<filter-class>..</filter-class>
		</filter>

		<filter-mapping>
			<filter-name>LoggerFilter</filter-name>
			<url-pattern>/*</url-pattern>
		</filter-mapping>