####SSH

* Hibernate：

		1.单独使用Hibernate框架，核心配置文件名称hibernate.cfg.xml和位置在类加载路径下面是固定的。
		2.Hibernate和Spring整合，Hibernate核心配置文件名称和位置没有固定要求。
		3.映射配置文件
* Struts：
	
		1.Action操作
		2.值栈
		3.拦截器
* Spring：

		1.Spring核心配置文件
		2.创建对象
		3.注入属性
		4.使用ServletContext对象和监听器实现
		5.jdbcTemplate
		6.事务配置
####SSH整合

* Struts2和Spring整合

		把Struts的action对象创建交给Spring进行管理
		<bean id="" class="" scope="prototype"/>
* Spring和Hibernate整合

		1.把Hibernate核心配置文件里面的数据库配置，直接写在Spring配置文件中
		2.在服务器启动时候创建sessionFactory对象