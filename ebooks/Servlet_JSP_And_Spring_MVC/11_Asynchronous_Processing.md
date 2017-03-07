一个servlet或filter会占据一个处理请求的线程，知道它完成任务。

异步处理可以节约容器线程，异步处理只适合下面的情况：耗费长时间的任务并且任务完成后需要通知用户结果。

WebServlet和WebFilter注解类型可以包含asyncSupport属性，为了支持异步处理，将该属性设置为true：

		@WebServlet(asyncSupport=true...)
		@WebFilter(asyncSupport=true...)

或者在部署描述器中使用async-supported元素：

		<servlet>
			<servlet-name></servlet-name>
			<servlet-class></servlet-class>
			<async-supported>true</async-supported>	
		</servlet>


支持异步处理的servlet或filter可以调用ServletRequest的startAsync方法创建新的线程。

		AyncContext startAsync()
		AyncContext startAsync(ServletRequest req,ServletResponse res)

####编写异步的Servlet

* 调用ServletRequest的startAsync方法，返回AsyncContext；
* 调用AyncContext的setTimeout()方法，传递容器等待任务完成的时间；
* 调用asyncContext.start，传递执行长时间任务的Runnable；
* 任务完成后，在Runnable里调用asyncContext.complete或asyncContext.dispatch方法。


####异步监听器

除了支持执行异步操作的servlet和filter外，利用AsyncListener接口可以在异步处理过程中获取消息。





