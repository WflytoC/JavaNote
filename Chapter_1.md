IoC(Inversion of Control)是设计原则，解耦对象与其依赖项。这种解耦通过将对象创建与依赖项注入交给外部组件，例如IoC。

####Dependency Injection

依赖项注入是IoC的特定形式，对象的依赖项通过三种形式注入：

* 构造器(constructor)
* 属性(setter)
* 接口


Ioc容器是下面接口的实现：

* org.springframework.beans.factory.BeanFactory
* org.springframework.context.ApplicationContext

Spring提供了ApplicationContext的几个具体实现。在Spring中，IoC容器管理的对象叫作beans，beans定义在配置元数据中。

