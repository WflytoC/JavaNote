拦截器相当于过滤器(filter)

* 定义拦截器，实现`HandlerInterceptor`接口，接口中提供三个方法。

		1.preHandle：进入Handler方法之前执行
		2.postHandle：进入Handler方法之后，返回ModelAndView之前执行
		3.afterCompletion：执行Handler完成之后执行
* 拦截器配置：针对HandlerMapping进行拦截设置

		    <mvc:interceptors>
        		<mvc:interceptor>
            		<mvc:mapping path="/**"/>
            		<bean class="interceptor.HandlerInterceptor1"/>
        		</mvc:interceptor>
        		<mvc:interceptor>
            		<mvc:mapping path="/**"/>
            		<bean class="interceptor.HandlerInterceptor2"/>
        		</mvc:interceptor>
    	</mvc:interceptors>