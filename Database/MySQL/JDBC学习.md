* 加载与注册JDBC驱动:
		//数据库驱动的完整类名
		//String driver = "oracle.jdbc.driver.OraclerDriver";
		String driver = "com.mysql.jdbc.Driver";

		Class.forName(driver);

* 建立连接
		
		//String jdbcUrl = "jdbc:oracle:thin:@localhost:1521:dbName";
		//String jdbcUrl = "jdbc:microsoft:sqlserver//localhost:1433;DatabaseName=dbName";
		String jdbcUrl = "jdbc:mysql://localhost:3306/dbName";
		userName = "root";
		password = "123456";

		Connection connection = DriverManager.getConnection(jdbcUrl,userName,password);;
* 访问数据库

		数据库连接被用于向数据库服务器发送命令和SQL语句。

		三个接口分别定义了对数据库的调用的不同方式：

			Statement
			PreparedStatement
			CallableStatement