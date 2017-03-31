spring对不同的持久化层技术都进行了封装：

* JDBC
* Hibernate
* Mybatis
* JPA


####使用jdbcTemplate：

* 导入依赖项包(`spring-jdbc`、`spring-tx`)

* 创建对象，设置数据库信息


		DriverManagerDataSource dataSource = new DriverManagerDataSource();
        dataSource.setDriverClassName("com.mysql.jdbc.Driver");
        dataSource.setUrl("jdbc:mysql:///temp?characterEncoding=UTF-8&serverTimezone=UTC");
        dataSource.setUsername("root");
        dataSource.setPassword("weichuang");

* 创建`jdbcTemplate`对象，设置数据源

		JdbcTemplate jdbcTemplate = new JdbcTemplate(dataSource);

* 调用`jdbcTemplate`对象里面的方法实现操作

		String sql = "insert into user values(?,?)";
        int rows = jdbcTemplate.update(sql,"wflytoc","weichuang");


####查询

* 查询返回某一个值

		String sql = "select count(*) from user";
        int count = jdbcTemplate.queryForObject(sql,Integer.class);

* 查询返回对象

		String sql = "select * from user where username=?";
        User user = jdbcTemplate.queryForObject(sql,new UserRowMapper(),"wflytoc");

		class UserRowMapper implements RowMapper<User>
* 查询返回List集合

		String sql = "select * from user";
        List<User> users = jdbcTemplate.query(sql,new UserRowMapper());


####Spring配置连接池和DAO使用jdbcTemplate

####Spring的事务管理

事务管理器：`PlatformTransactionManager`接口，Spring为不同的持久化框架提供了不同的`PlatformTransactinoManager`接口实现。

* 声明式事务管理

		1.xml配置文件：使用AOP思想
			<1>配置事务管理器
			<2>配置事务增强
			<3>配置切面
		2.注解
			<1>配置事务管理器
			<2>开启事务注解
			<3>在要使用事务的方法所在类上添加注解：@Transactional
* 

