####创建控制器

控制器类必须要使用@Controller注解，每个控制器类都有多个服务或处理器(service or handler)方法，DispatcherServlet会将每个方法映射到用户的请求上，方法必须要使用@RequestMapping注解。

实际上有四种类别的控制器：

* call a page only：只是调用一个页面

* bring model(s) to views：将模型传输给视图

* has multi-services or multi-actions：拥有多个服务或动作

* accepts request parameters (form controllers)：接受请求参数