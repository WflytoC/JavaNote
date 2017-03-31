* 全局结果页面配置：

		<global-results>
			<result name="success">/hello.jsp</result>
		</global-results>

* result标签的type属性

		type属性：如何到路径(转发|重定向)，默认是转发，值是dispatcher；重定向，值是redirect；

		其中，属性值为dispatcher、redirect是针对到页面种的配置，可以配置到其它的action里面：
			1.chain：转发到action，一般不用，缓存问题
			2.redirectAction：重定向到action

		<action name="order" class="action.OrderAction">
            <result name="success" type="redirectAction">item</result>
        </action>
        <action name="item" class="action.ItemsAction" >
            <result name="success"  type="redirect">/ok.jsp</result>
        </action>
		

####获取表单数据

* action获取表单提交数据的方式

		1.ActionContext
		2.ServletActionContext
		3.接口注入
* 使用ActionContext类获取

		ActionContext context = ActionContext.getContext();
        Map<String,Parameter> map = context.getParameters();
        Set<String> keys = map.keySet();
        for (String key: keys) {
            Parameter value = map.get(key);
        }
* 使用ServletActionContext类访问

		HttpServletRequest request = ServletActionContext.getRequest();

####操作域对象

		域对象包括request、session、servletContext对象
		HttpServletRequest request = ServletActionContext.getRequest();
		request.setAttribute("list",list);


####封装表单数据的方式

* 原始方式获取表单数据，并封装到实体类对象中

* 属性封装

		直接把表单提交的数据封装到action的属性里面
* 模型驱动封装

		直接把表单数据封装到实体类对象里面
		1.action实现接口ModelDriven
		2.实现接口里的方法：getModel方法
		3.在action里创建实体类对象
* 表达式封装

		1.在action里声明实体类
		2.生成实体类变量的set和get方法
		3.在表单输入项的name属性值里写成表达式形式

####封装表单数据到集合中

* 封装到List集合中

		1.在action中声明List
		2.生成List变量的set和get方法
		3.在表单输入项里写表达式
* 封装到Map集合中

		1.声明map集合
		2.生成get和set方法
		3.在表单输入项的name属性值里写表达式