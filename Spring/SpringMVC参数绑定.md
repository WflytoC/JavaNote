####参数绑定过程

* 客户端请求`key/value`
* 处理器适配器调用springmvc提供的`参数绑定组件`将`key/value`数据转化为controller方法的形参

		参数绑定组件：在springmvc早期版本使用PropertyEditor；后期使用converter(进行任意类型的转化)，在特殊情况下需要自定义。
* controller方法(形参)

####参数绑定类型

* 默认支持的类型：

		1.HttpServletRequest
		2.HttpServletResponse
		3.HttpSession
		4.Model/ModelMap
* 简单数据类型

		1.通过@RequestParam对简单类型的参数进行绑定
		
		2.如果不使用@RequestParam，要求request传入参数名称和controller方法的形参名称一致。

		3.如果使用@RequestParam，不用限制request传入参数名称和controller方法的形参名称一致
		
		4.通过required属性指定参数是否必须传入；通过defaultValue属性指定参数的默认值。

		String editItems(Model model,@RequestParam(value = "id") Integer items_id)
* POJO

		页面中input元素的name属性和controller方法的形参POJO的属性名保持一致，将页面中的数据绑定到POJO中。

		对于controller形参中POJO对象，如果属性中有日期类型，需要自定义参数绑定。将请求的日期数据串转换成日期类型。

* 包装类型

		页面参数：		
		<input name="itemsCustom.name" />
		
		controller方法形参：	
		ModelAndView queryItems(HttpServletRequest request, ItemsQueryVo itemsQueryVo)

		其中，ItemsQueryVo有属性itemsCustom，而itemsCustom有属性name

* 数组类型

		页面参数：
		<c:forEach>
		<input type="checkbox" name="items_id" value="${item.id}"/>
		</forEach>
		
		controller方法形参：
		String deleteItems(Integer[] items_id)
* List类型
* Map

		

	