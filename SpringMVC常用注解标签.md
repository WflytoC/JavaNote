
####@Controller

使用@Controller标记一个类是Controller。在SpringMVC 中，控制器Controller 负责处理由DispatcherServlet 分发的请求，它把用户请求的数据经过业务处理层处理之后封装成一个Model ，然后再把该Model 返回给对应的View 进行展示。

####@RequestMapping

RequestMapping是一个用来处理请求地址映射的注解，可用于类或方法上。用于类上，表示类中的所有响应请求的方法都是以该地址作为父路径。

RequestMapping注解有六个属性：

* value： 指定请求的实际地址，指定的地址可以是URI Template 模式

* method： 指定请求的method类型，GET、POST、PUT、DELETE等

* consumes： 指定处理请求的提交内容类型（Content-Type），例如application/json, text/html

* produces:    指定返回的内容类型，仅当request请求头中的(Accept)类型中包含该指定类型才返回

* params： 指定request中必须包含某些参数值是，才让该方法处理

* headers： 指定request中必须包含某些指定的header值，才能让该方法处理请求


####@Resource和@Autowired

@Resource和@Autowired都是做bean的注入时使用，两者都可以写在字段和setter方法上。两者不同点：

* @Autowired只按照byType注入

* @Autowired注解是按照类型（byType）装配依赖对象，默认情况下它要求依赖对象必须存在，如果允许null值，可以设置它的required属性为false。如果我们想使用按照名称（byName）来装配，可以结合@Qualifier注解一起使用

* @Resource默认按照ByName自动注入，。@Resource有两个重要的属性：name和type，而Spring将@Resource注解的name属性解析为bean的名字，而type属性则解析为bean的类型。所以，如果使用name属性，则使用byName的自动注入策略，而使用type属性时则使用byType自动注入策略。如果既不制定name也不制定type属性，这时将通过反射机制使用byName自动注入策略。


####@ModelAttribute和 @SessionAttributes

* 在该Controller的所有方法调用前，先执行此@ModelAttribute方法

* @SessionAttributes将值放到session作用域中，写在class上面


####@PathVariable

用于将请求URL中的模板变量映射到功能处理方法的参数上，即取出uri模板中的变量作为参数。


####@requestParam

@requestParam主要用于在SpringMVC后台控制层获取参数，类似一种是request.getParameter("name")，它有三个常用参数：defaultValue = "0", required = false, value = "isApp"；defaultValue 表示设置默认值，required 通过boolean设置是否是必须要传入的参数，value 值表示接受的传入的参数类型。

####@ResponseBody

该注解用于将Controller的方法返回的对象，通过适当的HttpMessageConverter转换为指定格式后，写入到Response对象的body数据区。使用时机：返回的数据不是html标签的页面，而是其他某种格式的数据时（如json、xml等）使用

####@Component

相当于通用的注解，当不知道一些类归到哪个层时使用，但是不建议

####@Repository

用于注解dao层，在daoImpl类上面注解。
