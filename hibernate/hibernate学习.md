ORM：实体类和数据库表进行一一对应

####搭建Hibernate环境

* 导入依赖项jar包

* 创建实体类

		要求实体类有一个属性值是唯一的

* 配置实体类和数据库表一一对应关系(映射关系)：创建映射配置文件

		1.创建xml格式的配置文件(名称和位置没有固定要求，建议放在实体类所在的包中，名称为XXX.hbm.xml)
		
* 创建hibernate的核心配置文件：

		1.核心配置文件名称(hibernate.cfg.xml)和位置(类加载目录下)固定
		2.配置数据库信息、配置hibernate信息、加载映射文件


####实现操作

* 加载hibernate核心配置文件
* 创建SessionFactory对象
* 使用SessionFactory创建session对象
* 开启事务
* 写具体逻辑操作
* 提交事务
* 关闭资源

####Hibernate核心API

* `Configuration`

* `SessionFactory`

* `Session`

* `Transaction`