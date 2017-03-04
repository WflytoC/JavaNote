维持HTTP连接状态：

* URL Rewriting： 格式 -- `url?key-1=value-1&..`

* Hidden fields：将值放在HTML表单的隐藏域中

		<input type="hidden" value="1" name="id" />

* Cookie：可以通过服务器或浏览器创建或删除。

* HttpSession对象：HttpSession存储在内存中，存储在HttpSession中的值不会发送给客户端。