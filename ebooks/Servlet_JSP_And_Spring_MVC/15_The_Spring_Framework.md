####Dependency Injection依赖性注入

  依赖项注入负责对象的创建，然后把依赖项注入到需要其的对象中。

Spring支持基于setter和基于constructor的依赖项注入，从2.5开始，也支持基于field的依赖项注入(通过Autowired注解类型)

需要通过【XML文件】或应用【注解】来配置Spring来告诉它如何进行依赖项注入，接着需要创建ApplicationContext，代表Spring IoC容器。其中，XML配置文件包含关于bean的信息。ClassPathXmlApplicationContext尝试在classpath中寻找配置文件。

