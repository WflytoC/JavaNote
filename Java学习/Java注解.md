注解仅仅是元数据，和业务逻辑无关

注解的作用：

* 格式检查：告诉编译器信息，比如被@Override标记的方法如果不是父类的某个方法，IDE会报错
* 减少配置：运行时动态处理，得到注解信息，实现代替配置文件的功能
* 减少重复工作


####元注解

元注解的作用是负责注解其它注解。下面是标准的元注解：

* @Target

		说明Annotation所修饰的对象范围：
			CONSTRUCTOR：描述构造器
			FIELD：描述域
			LOCAL_VARIABLE：描述局部变量
			METHOD：描述方法
			PACKAGE：描述包
			PARAMETER：描述参数
			TYPE：描述类、接口或enum声明
		@Target(ElementType.TYPE)

* @Retention

		定义该Annotation被保留的时间长短，即被描述的注解在什么范围内有效。
			SOURCE：在源文件中有效(源文件保留)
			CLASS：在class文件中有效(class保留)
			RUNTIME：在运行时有效(运行时保留)
		@Retention(RetentionPolicy.RUNTIME)

* @Documented

		标记注解，没有成员，用于描述其它类型的注解应该被作为被标注的程序成员的公共API。
		@Document
* @Inherited

		标记注解，阐述了某个被标注的类型是被继承的。
		@Inherited


####自定义注解


`@interface`用来声明一个注解，其中的每一个方法实际上是声明了一个【配置参数】。方法的名称就是参数的名称，返回值类型就是参数的类型。可以通过default来声明参数的默认值。

		@Target({ElementType.TYPE})
		@Retention(RetentionPolicy.RUNTIME)
		@Documented
		public @interface WebServlet {
			String name() default "";
			String[] urlPatterns() default {};
			int loadOnStartup() default -1;
		}


####创建注解处理器

`AnnotatedElement`接口是所有程序元素（`Class`、`Field`、`Package`、`Method`和`Constructor`）的父接口，所以程序通过反射获取了某个类的AnnotatedElement对象之后，程序就可以调用该对象的如下四个个方法来访问Annotation信息：

* `<T extends Annotation> T getAnnotation(Class<T> annotationClass)`: 返回该程序元素上存在的、指定类型的注解，如果该类型注解不存在，则返回null
* `Annotation[] getAnnotations()`:返回该程序元素上存在的所有注解。
* `boolean isAnnotationPresent(Class<?extends Annotation> annotationClass)`:判断该程序元素上是否包含指定类型的注解，存在则返回true，否则返回false
* `Annotation[] getDeclaredAnnotations()`：返回直接存在于此元素上的所有注释。与此接口中的其他方法不同，该方法将忽略继承的注释。

		