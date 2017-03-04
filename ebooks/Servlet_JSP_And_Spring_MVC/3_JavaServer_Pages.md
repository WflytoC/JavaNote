JSP页面本质上是Servlet，JSP页面第一次被请求时，Servlet/JSP容器做以下两件事：

* 将JSP页面翻译成JSP页面实现类，让JSP页面成为Servlet
* 如果翻译成功，Servlet/JSP容器就会编译Servlet类。


Java代码可以出现在JSP页面的任何地方，通过`<% %>`包装。为了在JSP页面中导入Java类型，使用page指令的import属性。

####隐式对象(Implicit Objects)

在JSP页面中，可以使用隐式对象来获取下面的对象：

* request: HttpServletRequest
* response: HttpServletResponse
* out: JspWriter
* session: HttpSession
* application: ServletContext
* config: ServletConfig
* pageContext: PageContext
* page: JspPage
* exception: Throwable


####指令(Directive)

使用指令来告诉JSP翻译器如何将JSP页面翻译成Servlet。

		page指令
		<%@ page attribute1="value1" attribute2="value2" ... %>

		include指令
		<%@ include file="url" %>


####脚本元素(Scripting Elements)

* Scriptlets

		语法：<% %>
		在一个scriptlet中定义的变量可以在它下面的scriptlet中获取。
* Expressions

		语法：<%= %>
		
* Declarations

		语法：<%! %>
		在JSP页面中可以定义变量和方法。可以使用声明来重写init和destroy方法，为了重写init，声明jspInit方法，为了重写destroy，声明jspDestroy方法。

在JSP2.0中引入了EL(Expression Language)，推荐使用EL来获取服务端对象，而不是在JSP页面中编写Java代码。通过在部署描述器的`<jsp-property-group>`中定义`<scripting-invalid>`元素来禁止脚本元素。

####动作(Actions)

动作会被翻译成执行某项操作的Java代码。格式是<jsp:动作名 />

* useBean：创建一个与Java对象关联的脚本变量
* setProperty与getProperty：设置Java对象的属性和打印Java对象的属性
* include：动态地包含另一个资源
* forward：将当前的页面转到另一个资源


####错误处理

通过使用Page指令的isErrorPage属性来让JSP页面成为错误页。其它页面发生错误时，必须使用page指令的errorPage属性，该属性值为错误处理页的路径。

		<%@ page isErrorPage="true" %>
		<%@ page errorPage="errorHandler.jsp" %>


