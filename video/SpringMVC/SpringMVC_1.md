####SpringMVC架构原理

SpringMVC是Spring框架的一个模块

* 发起请求到前端控制器(`DispatcherServlet`)

* 前端控制器请求`HandlerMapping`查找`Handler`(可以根据XML配置、注解进行查找)

* 处理器映射器`HandlerMapping`向前端控制器返回

* 前端控制器调用处理器适配器去执行`Handler`

* 处理器适配器去执行`Handler`

* `处理器适配器`向前端控制器返回`ModelAndView`

* 前端控制器请求视图解析器去进行视图解析

* `视图解析器`向前端控制器返回View

* 前端控制器进行视图渲染

* 前端控制器向用户响应结果

组件：

* 前端控制器`DispatcherServlet`：接收请求，响应结果，相当于转发器

* 处理器映射器`HandlerMapping`：根据请求的url查找Handler

* 处理器适配器`HandlerAdapter`：根据特定规则(HandlerAdapter要求的规则)去执行Handler

* 视图解析器`ViewResolver`：进行视图解析，根据逻辑视图名解析成真正的视图

* 视图`View`：接口，其实现类支持不同的视图类型





####相关配置

* 处理器适配器：此适配器能执行实现`Controller`接口的`Handler`

* 处理器映射器

* Handler

* 视图解析器：


####SpringMVC和MyBatis整合

Spring将各层进行整合：

* 通过`Spring`管理持久层的`mapper`(相当于DAO接口)
* 通过`Spring`管理业务层的`service`，而service可以调用mapper接口
* 通过`Spring`管理表现层`Handle`r，`Handler`中可以调用`service`接口
* mapper、service和Handler都是JavaBean


####SpringMVC和MyBatis整合

* mybatis配置文件：`sqlMapConfig.xml`文件

* mybatis和spring整合相关配置文件：`applicationContext-dao.xml`(数据源、SqlSessionFactory、mapper扫描器)