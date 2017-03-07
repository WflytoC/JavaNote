##JSP 标准标签库（JSTL）

使用任何库，你必须在每个JSP文件中的头部包含<taglib>标签，根据JSTL标签所提供的功能，可以将其分为5个类别：

####核心标签

	<%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core" %>

####格式化标签

	<%@ taglib prefix="fmt" uri="http://java.sun.com/jsp/jstl/fmt" %>

####SQL标签

	<%@ taglib prefix="sql" uri="http://java.sun.com/jsp/jstl/sql" %>

####XML标签

	<%@ taglib prefix="x" uri="http://java.sun.com/jsp/jstl/xml" %>

####JSTL函数

	<%@ taglib prefix="fn" uri="http://java.sun.com/jsp/jstl/functions" %>