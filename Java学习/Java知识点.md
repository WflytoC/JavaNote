####比较对象是否相等

* `==`与`!=`是比较对象的句柄是否相等

* `equals()`默认行为是比较句柄，如果想要该方法比较的是对象的内容，则需要重写该方法。大部分Java类库已重写，所以Java库中的对象比较的是内容。如果对象适用于`equals()`的话，则两个对象的`hashCode()`一定要相同。


####方法引用

形式：`类名::方法名`


* 引用静态方法		

		ContainingClass::staticMethodName
* 引用某个对象的实例方法	

		containingObject::instanceMethodName
* 引用某个类型的任意对象的实例方法	

		ContainingType::methodName
* 引用构造方法	

		ClassName::new

####线程Join方法

使用Join实现线程的执行顺序