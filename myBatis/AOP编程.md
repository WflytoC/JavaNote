####安装

		compile group: 'org.mybatis', name: 'mybatis', version: '3.4.2'

####从XML中构建SqlSessionFactory

SqlSessionFactionBuilder需要从XML配置文件中创建SqlSessionFactory实例。XML配置文件包含了MyBatis系统的设置，例如获取数据库连接实例的数据源、决定事务作用域的事务管理器。

####探索映射的SQL表达式

表达式可以使用XML文件或者注解定义

		<!DOCTYPE mapper
  			PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
  			"http://mybatis.org/dtd/mybatis-3-mapper.dtd">
		<mapper namespace="org.mybatis.example.BlogMapper">
  			<select id="selectBlog" resultType="Blog">
    			select * from Blog where id = #{id}
  			</select>
		</mapper>


讲解：

* namespace：必须与对应的接口全类名相同；
* id：必须与对应接口的某个对应的方法名相同；
* parameterType：接口中方法的参数类型；
* resultType：接口中方法的返回值类型
* `#{}`：代表变量

####作用域和生命周期


* SqlSessionFactoryBuilder：该实例最好的作用域是方法作用域，创建好该实例后，没必要一直保持它。

* SqlSessionFactory：该实例在应用运行期间应当一直存在，可以利用单例模式或静态单例模式。

* SqlSession：该实例不应当被共享，不是线程安全的。因此最好的作用域是请求或者方法作用域。

* Mapper Instances：这是你创建的接口，用来绑定映射的表达式(mapped statement)。mapper接口的实例通过SqlSession来获取。
