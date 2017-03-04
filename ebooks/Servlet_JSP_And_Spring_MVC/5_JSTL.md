下载JSTL：

		compile group: 'javax.servlet', name: 'jstl', version: '1.2'

JSTL通过多个标签库来暴露动作，可以分为五个类别：

* Core
* XML
* I18n
* Database
* Functions

在JSP页面中使用JSTL，以下面的格式使用taglib指令。

		<%@ taglib uri="" prefix="" %>

		<%@ taglib uri="http://java.sun.com/jsp/jstl/core" prefix="c" %>


####通用目的的动作

* out：计算出表达式的值，将结果输入到当前的JspWriter中。

		<c:out value="${header['accept-language']}" default="Disappear" escapeXml="true"/>
* set：创建一个字符串和引用该字符串的变量、设置对象的属性

		<c:set var="name" value="wflytoc" />
		<c:set target="${address}" property="city" value="Tokyo" />
		
* remove：移除一个变量(只是移除变量)

		<c:remove var ="name" scope="page" />


####条件动作

* if：测试一个条件，如果条件为true，则处理body内容；测试结果会被放在作用域变量中。

		没有body内容：
			<c:if test="testCondition" var="varName" />
		有body内容：
			<c:if test="testCondition" > ..</c:if>

		<c:if test="${param.user=='wflytoc'}" var="right"/>
    	${(right) ? "Ok" : "No"}
		
* choose(相当于switch)、when(相当于case)、otherwise(相当于default)：

		<c:choose>
        	<c:when test="${param.status=='full'}">
            	You are a full number
        	</c:when>
        	<c:when test="${param.status=='student'}">
            	You are a student
        	</c:when>
        	<c:otherwise>
            	Please register
        	</c:otherwise>
    	</c:choose>

####遍历动作

* forEach：遍历body内容多次或者遍历对象数组

		重复body内容固定的次数
		<c:forEach var="x" begin="1" end="5" >
        	<c:out value="${x}" />
    	</c:forEach>

		遍历对象集合/数组
    	<c:forEach var="number" items="${['A','B']}" >
        	${number} <br/>
    	</c:forEach>


		books是List类型
		<c:forEach items="${requestScope.books}" var="book" varStatus="status">
            <c:if test="${status.count%2 == 0}">
                <tr style="background: #eeeeff;">
            </c:if>
            <c:if test="${status.count%2 != 0}">
                <tr style="background: #dedeff">
            </c:if>
            <td>${book.isbn}</td>
            <td>${book.title}</td>
            </tr>
        </c:forEach>
    </table>

		使用forEach来遍历Map，通过key和value属性来获取Map的key和value。

			
* forTokens

		遍历由特定分隔符分开的token。

		<c:forTokens items="A,B,C,D,E,F" delims="," var="item">
            ${item}
        </c:forTokens>


####格式化动作

		<%@ taglib prefix="fmt" uri="http://java.sun.com/jstl/fmt" %>

* formatNumber：格式化数字，最常用的是将数字格式化成货币。

		<fmt:formatNumber  value="12" type="currency"/>
* formatDate
* timeZone
* setTimeZone
* parseNumber

####函数

在EL表达式中，可以使用一系列标准函数，在JSP页面中使用下面的taglib指令：

		<%@ taglib prefix="fn" uri="http://java.sun.com/jsp/jstl/functions" %>

调用函数的格式是：

		${fn:functionName}

		<c:set var="myString" value="Hello World"/>
    	${fn:contains(myString, "Hello")}