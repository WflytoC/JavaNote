####XML命名空间

使用【前缀】来避免命名冲突：

		<h:table>
			<h:tr>
				<h:td>Apple</h:td>
			</h:tr>
		</h:table>

使用命名空间：

		<h:table  xmlns="http://www.w3.org/TR/html14">
			<h:tr>
				<h:td>Apple</h:td>
			</h:tr>
		</h:table>

		为<table>标签添加了xmlns属性

####xmlns(XML命名空间)属性

xmlns属性放置在元素的开始标签中，所有带有相同前缀的子元素都会与同一命名空间相关联，使用以下语法：

		xmlns:namespace-prefix(命名空间前缀)="namespaceURI(标示命名空间的地址)"

####默认的命名空间

为元素定义默认的命名空间可以省去在所有的子元素中使用前缀的工作。语法如下：

		xmlns="namespaceURI"

####xsi:schemaLocation

定义了XML命名空间和对应的`XSD`(`Xml Schema Definition`)文档的位置的关系。它的值由一个或多个URI引用对组成，两个URI之间以空白符分隔（空格和换行均可）。第一个URI是定义的XML命名空间的值，第二个URI给出Schema文档的位置，Schema处理器将从这个位置读取Schema文档，该文档的targetNamespace必须与第一个URI相匹配。


		