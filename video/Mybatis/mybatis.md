mybatis让程序主要放在sql上，通过mybatis提供的映射方式，来生成sql语句。mybatis可以将向`preparedStatement`中的`输入参数`自动进行输入映射，将`查询结果集`映射成java对象。


####开发环境搭建

* 依赖项：

		compile group: 'mysql', name: 'mysql-connector-java', version: '6.0.5'
    	compile group: 'org.mybatis', name: 'mybatis', version: '3.4.1'
    	compile group: 'log4j', name: 'log4j', version: '1.2.17'

* mybatis的全局配置文件(sqlMapConfig.xml文件)：

		<?xml version="1.0" encoding="UTF-8" ?>
		<!DOCTYPE configuration
        	PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
       	    "http://mybatis.org/dtd/mybatis-3-config.dtd">
			<configuration>
    			<environments default="development">
        			<environment id="development">
            		<transactionManager type="JDBC"/>
            			<dataSource type="POOLED">
                			<property name="driver" value="com.mysql.jdbc.Driver"/>
                			<property name="url" value="jdbc:mysql://localhost:3306/batis?characterEncoding=UTF-8"/>
                			<property name="username" value="root" />
                			<property name="password" value="weichuang" />
            			</dataSource>
        			</environment>
   		 		</environments>
				<!-- mybatis和spring整合后environment配置将废除 -->
				<mappers>
        			<mapper resource="sqlmap/User.xml"/>
    			</mappers>
			</configuration>

* 映射文件(需要配置在mybatis配置文件中)

		<?xml version="1.0" encoding="UTF-8" ?>
		<!DOCTYPE mapper
        	PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
        	"http://mybatis.org/dtd/mybatis-3-mapper.dtd">
			<mapper namespace="user">
    			<select id="findUserById" parameterType="int" resultType="po.User">
        			SELECT * FROM user WHERE id = #{id}
    			</select>
    			<select id="findUserByName" parameterType="java.lang.String" resultType="po.User">
        			SELECT * FROM user WHERE username LIKE '%${value}%'
    			</select>
		</mapper>


####知识点讲解

* `parameterType`：在映射文件中指定输入参数的类型

* `resultType`：在映射文件中指定输出结果的类型，sql查询可能会返回多条记录，但是`resultType`就是指定单条记录所映射的java对象类型

* `#{}`表示占位符，`${}`表示拼接字符串

* `selectOne`表示查询出一条记录进行映射，`selectList`表示查询出一个列表(多条记录)进行映射

####映射文件的各种类型

* 查询

		<select id="findUserByName" parameterType="java.lang.String" resultType="po.User">
        	SELECT * FROM user WHERE username LIKE '%${value}%' //可能返回多条记录，但是resultType就是指定单条记录映射的类型
    	</select>
* 添加

		<insert id="insertUser" parameterType="po.User">
        	INSERT INTO user(id,username,birthday,sex,address) VALUE (#{id},#{username},#{birthday},#{sex},#{address}) //parameterType指定输入参数类型是pojo，#{}指定pojo的属性名
    	</insert>

		实现主键返回：

		1.自增主键返回，使用LAST_INSERT_ID()

			<selectKey keyProperty="id" order="AFTER" resultType="java.lang.Integer">
            	SELECT LAST_INSERT_ID()
        	</selectKey>
		2.非自增主键返回：使用uuid(),id必须是字符串

			<selectKey keyProperty="id" order="BEFORE" resultType="java.lang.String">
            SELECT uuid()
        </selectKey>

* 删除用户

		<delete id="deleteUserById" parameterType="java.lang.Integer">
        	DELETE FROM user WHERE id=#{id}
    	</delete>
* 更新用户

		<update id="updateUser" parameterType="po.User">
        	UPDATE user SET username=#{username},birthday=#{birthday},address=#{address},sex=#{sex} WHERE id=#{id}
    	</update>



####mybatis开发DAO的方法

通过`SqlSessionFactoryBuilder`创建会话工厂`SqlSessionFactory`。通过`SqlSessionFactory`创建`SqlSession`，使用单例模式管理`sqlSessionFactory`(工厂一旦创建，使用一个实例)。将来`mybatis`和`spring`整合后，使用单例模式管理`sqlSessionFactory`。`SqlSession`是一个面向用户的接口，提供了很多操作数据库的方法。


* 原始DAO开发方法：需要写DAO接口和DAO实现类，在DAO实现类中注入`SqlSessionFactory`，在方法体内通过`SqlSessionFactory`创建`SqlSession`。

* mapper代理方法：只需要编写mapper接口(相当于DAO接口)和编写mapper.xml映射文件。mybatis可以自动生成mapper接口的实现类代理对象，不过需要遵守相关规范：

		1.mapper.xml中的namespace等于mapper接口地址
		2.mapper接口中的方法名与mapper.xml中statement的id一致
		3.mapper接口的方法输入参数类型和mapper.xml中satement的parameterType指定的类型一致
		4.mapper接口的方法返回值类型和mapper.xml中statement的resultType指定的类型一致

		mapper接口的方法参数只能有一个，但是可以使用包装类型的pojo来满足不同业务方法的需求。


####mybatis的配置文件SqlMapConfig.xml文件

* properties属性：将数据库连接参数单独配置在db.properties中

		<properties resource="db.properties"></properties>
* settings属性：全局参数配置，比如开启二级缓存、开启延迟加载

* typeAliases：别名，mybatis默认会支持一些别名，

		<typeAliases>
			<typeAlias type="po.User" alias="user"/> //针对单个别名定义

			<package name="po" /> //批量别名定义，指定包名，mybatis自动扫描包中的po类，别名就是类名(首字母大写或小写)
		</typeAliases>
*  typeHandlers(类型处理器)：mybatis中通过typeHandlers完成jdbc类型和java类型的转换。

*  mappers(映射配置)

		1.通过resource加载单个映射文件
			<mapper resource="mapper/UserMapper.xml" />
		2.通过mapper接口加载映射文件(遵守规范)
			<mapper class="mapper.UserMapper" />
		3.批量加载mapper：指定mapper接口的包名
			<package name="mapper" />
			


####输入映射

通过parameterType指定输入参数的类型，类型可以是简单类型、hashmap、pojo的包装类型


####输出映射

* resultType：只有查询出来的列名和pojo中的属性名一致，改列才可以映射成功

* resultMap：完成高级输出结果映射

		定义resultMap：

			<resultMap type="user" id="userResultMap">
				<id column="" property="" />
			</resultMap>

####动态SQL

mybatis通过表达式进行判断，对sql进行灵活拼接、组装。

* 对查询条件进行判断，如果输入参数不为空才进行

		<where>
			<if test="userCustom!=null">
				<if test="userCustom.sex!=null and userCustom.sex!=''">
					and user.sex = #{userCustom.sex}
				</if>
			</if>
		</where>
* 定义sql片段

* foreach标签



		