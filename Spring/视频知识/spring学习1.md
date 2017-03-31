####Spring的Bean管理

* 使用注解方式创建对象

		在spring配置文件中开启注解扫描
		<context:component-scan base-package="anno"></context:component-scan>

		对需要创建对象的类进行注解：
		@Component(value = "user")

		创建对象有四个注解，它们的功能都是一样的，不同的名称是为了让标注类本身的用途清晰：
		1.@Component
		2.@Controller
		3.@Service
		4.@Repository

		创建对象是单实例还是多实例：
		@Scope(value = "prototype")
* 使用注解来注入属性

		 @Autowired
    	 private UserDAO userDAO;

		 @Resource(name = "userDao")
    	 private UserDAO userDAO;
* xml和注解方式混合使用