数据库表存储在硬盘中或者电脑内存中。


		CREATE TABLE employee(
			employee_id INTEGER UNSIGNED NOT NULL AUTO_INCREMENT,
			last_name VARCHAR(30) NOT NULL,
			email VARCHAR(100) NOT NULL,
			hire_date DATE NOT NULL,
			
			PRIMARY KEY (employee_id),
			INDEX (last_name),
			UNIQUE (email)
		)ENGINE=InnoDB;

		CREATE TABLE address (
			employee_id INTEGER UNSIGNED NOT NULL,
			address VARCHAR(50) NOT NULL,
			postcode CHAR(5) NOT NULL,

			FOREIGN KEY (employee_id) REFERENCES employee(employee_id)

		);

		INSERT INTO address employee(last_name,email,hire_date) VALUES('wflytoc','wcshinestar@outlook.com','2014-2-2');

####创建数据表

使用`CREATE TABLE`创建数据表，该表达式提供了表名称、列名称及其数据类型，我们可以为列定义声明属性。

* `PRIMARY KEY`：该列的所有值都是不同的，可以用来唯一地标识表中的每条记录。

* `AUTO_INCREMENT`：如果该列的值没提供，MySQL会自动使用下一个最大的序列整数作为值，该列必须是`PRIMARY KEY`。

* `INDEX`：让MySQL知道我们在稍后的选择标准中可能会使用该列的值，MySQL会使用该列中的值来创建和管理特殊的索引结构。

* `UNIQUE`：确保存储在该列的所有值都是不同的

* `FOREIGN KEY`：定义了两张表的关系


`DESCRIBE`返回数据表的列名称及其数据类型；
`SHOW CREATE TABLE`返回表达式，可以用来重新创建数据表。

####数据类型和存储类型

每种数据类型在磁盘或内存中的存储需要不同的量，所以我们总是想声明占用空间最小的类型。

* 数字类型：
* 字符串类型：
* 时间格式：
* 特殊的数据类型：

####存储引擎

存储引擎(storage engine)指的是负责管理数据表和数据的底层逻辑和编程代码。引擎将数据在磁盘或内存中如何组织的细节抽象出来，允许我们只从数据表和数据行的角度来思考。


####添加数据

`INSERT INTO`

####使用事务

		START TRANSACTION;
		....
		COMMIT/ROLLBACK;
