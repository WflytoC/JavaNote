####struts2概述

struts2利用拦截器对所有的请求进行拦截，根据不同的操作执行不同的action中的方法。

####入门操作

* 引入依赖项

		compile group: 'org.apache.struts', name: 'struts2-core', version: '2.5.10'
* 创建action

* 配置action类访问路径

		创建struts2核心配置文件(名称和位置是固定，名称是struts.xml，位置为类加载路径)，并进行action配置

* 配置拦截器


####struts源码

* 过滤器名称：`strutsPrepareAndExecuteFilter`

* 过滤器在服务器启动时创建，创建过滤器时执行`init`方法：在`init`方法中主要加载配置文件


####struts配置

* package标签：区别不同的action，要配置action，必须首先写package标签

		1.name属性：属性值与功能没有关系
		2.extends属性：属性值是固定的，让package里面配置的类具有action功能
		3.namespace属性：该属性值与action标签里面的name属性值构成访问路径
* action标签：配置action访问路径

		1.name属性：该属性值与package的namespace属性值构成访问路径
		2.class属性：action全路径
		3.method属性：在action里默认执行execute方法，利用该属性可以指定action中的其它方法
* result标签：根据action方法的返回值，配置到不同的路径里面

		1.name属性：和方法返回值一样
		2.type属性：配置如何到路径中(转发或重定向)

* 修改struts2默认常量值

		1.在struts.xml中进行配置
			<constant name="struts.i18n.encoding" value="UTF-8"/>

####分模块开发

单独写配置文件，把配置文件引入到核心配置文件(`struts.xml`)中

####Action编写方法(三种方式)

* 第一种：创建普通类，不继承任何类，不实现任何接口
* 第二种：创建类，实现接口`Action`
* 第三种：创建类，继承类`ActionSupport`


####访问action的方法

* 使用action标签的method属性(适用于action的方法比较少的情况)

		<action name="add" class="method.BookAction" method="add"/>
* 使用通配符方式

		<action name="book_*" class="method.BookAction" method="{1}">
            <allowed-methods>add,update</allowed-methods>
        </action>
* 动态访问

