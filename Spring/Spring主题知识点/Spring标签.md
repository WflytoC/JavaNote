####Spring表单标签

要使用Spring MVC提供的表单标签，首先需要在视图页面添加：

		<%@ taglib prefix="form" uri="http://www.springframework.org/tags/form" %>

form标签：

		<form:form modelAttribute="contentModel" method="post">

其中modelAttribute属性指定该表单绑定哪个模型，当指定了对应的模型后就可以在form标签内部其它表单标签上通过为`path`指定模型的属性名称来绑定模型中的数据

		<form:input path="username"/>