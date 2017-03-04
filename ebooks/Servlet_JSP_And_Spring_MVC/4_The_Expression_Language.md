####EL语法：

EL语法：`${expression}` 例如，`${x+y}`

* 在EL中，通过`[]`或`.`来获取对象的属性；但是如果属性名不是一个合法的Java变量名，只能使用`[]`操作符。


####EL隐式对象

* pageContext：代表了PageContext，可以获得其它的JSP隐式对象。
* initParam
* param
* paramValues
* header
* headerValues
* cookie
* applicationScope
* sessionScope
* requestScope
* pageScope


####其它操作符

EL也提供了其它操作符：算术、关系、逻辑、条件、`empty`操作符

		$(empty x)：如果x是null或者长度为0的字符串或者空的Map、数组、集合，表达式都返回true。