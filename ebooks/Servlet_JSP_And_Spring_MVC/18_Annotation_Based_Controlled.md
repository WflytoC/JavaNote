使用基于注解的控制器有一些优势：

* 一个基于注解的控制器可以处理多个动作，即相关的动作可以写在同一个控制器中；

* 基于注解的控制器的请求映射(request mapping)不需要写在配置文件中。使用RequestMapping注解可以让方法成为处理请求的方法。


####Controller注解

		@Controller
		public class LoginController {
		
		}

Spring使用扫描机制来发现应用中所有【基于注解】的控制器类。为了确保Spring可以发现控制器类，需要做以下两件事：

* 在SpringMVC配置文件中声明`spring-context`schema

		<beans
			...
			xmlns:context="http://www.springframework.org/schema/context"
			...
		>
* 在配置文件中使用`<component-scan />`元素

		<context:component-scan base-package="basePackage(控制器所在的包)" />


####RequestMapping注解

为了告诉Spring哪个方法处理哪个动作，需要使用RequestMapping来将URI映射到方法上。

		@RequestMapping(value="/customer_input") 
		public String inputCustomer{
			...
			return "CustomerForm";
		}

 使用RequestMapping注解的value属性来声明映射到方法上的URL。RequestMapping注解还有其它的属性，该注解还可以用来注解控制器类。


####编写处理请求的方法

处理请求的方法可以有【多种类型的参数】和【多种返回值类型】。比如，你需要在方法中获取HttpSrevletRequest和HttpSession，可以将它们作为方法的参数，Spring会为你传递正确的对象：

		@RequestMapping("url/")
		public String otherMethod(HttpServletRequest req,HttpSession session) {
			...
		}

在处理请求方法中可以作为参数类型：

* ServletRequest/HttpServletRequest
* ServletResponse/HttpServletResponse
* HttpSession
* ....
* 表单对象
* org.springframework.ui.Model：该类型包含Map
* 使用`@PathVariable`、`@MatrixVariable`、`@RequestParam`、`@RequestHeader`、`@RequestBody`、`@RequestPart`注解的类型

处理请求的方法可以返回下面类型的值：

* ModelAndView
* Model
* Map
* View
* ....

####编写基于注解的控制器

* 在web.xml文件中注册SpringMVC DispatcherServlet。

* Spring MVC配置文件：
		
		<resources />元素，让SpringMVC正确地处理静态资源，该元素告诉SpringMVC哪些资源可以被单独提供(不收dispatcher servlet约束)

* 每次处理请求的方法被调用时，SpringMVC都会创建Model实例，Model的主要目的是为了添加需要在视图中展示的属性。

####@Autowired和@Service

使用@Autowired对控制器的【属性或方法】注解让[依赖项]注入到控制器中，为了让SpringMVC发现依赖项，必须用@Service来注解依赖项的类。

####请求参数和路径变量(Path Variables)

使用@RequestParam为处理请求的方法的参数进行注解，从而请求参数的值会拷贝到方法参数中。

		public void sendProduct(@RequestParam int productId)


		@RequestMapping(value = "/product_vew/{id}")
		public String viewProduct(@PathVariable Long id,Model model)

导入资源文件：

		<style type="text/css">
			@import url("<c:url value='/css/min.css' />");
		</style>


####@ModelAttribute

@ModelAttribute可以用来注解方法参数或方法。

* @ModelAttribute注解的方法参数，会创建该参数的实例，然后将其添加到Model对象中。

		@RequestMapping(method=RequestMethod.POST)
		public String submitPost(@ModelAttribute("newOrder") Order order,Model model) {}
		
		每次submitPost方法调用时，SpringMVC都会创建Order实例，然后使用newOrder键将其添加到model中
* @ModelAttribute注解非处理请求的方法，该方法会在处理请求的方法之前调用。如果该方法返回对象，那么返回的对象会添加到接下来调用的方法的model里。

		

		 






