在命令行中执行`.sql`文件中的命令

		mysql -u root -p < salila-schema.sql


####获取数据

`SELECT * FROM tableName;`

* 排序：`ORDER BY (DESC,ASC)`

		SELECT last_name,first_name FROM actor ORDER BY last_name ASC,first_name DESC;
* 管理返回结果的行数

		LIMIT指定返回结果的行数：
			SELECT last_name FROM actor ORDER BY first_name DESC limit 5;

		WHERE声明返回结果的每条记录满足的条件：
			SELECT title,length FROM film WHERE length < 60 ORDER BY title;

		WHERE的其它操作符
			A IN (B,C,D)
			A BETWEEN B AND C
			A LIKE 'PATTERN'[_匹配单个字符，%匹配多个字符]
			A REGEXP '/EXPRESSION/'
* 聚合函数和分组

		聚合函数在返回的结果记录被分成组时最有用，计算使用[组中的每条记录]来执行。

		SELECT customer_id,SUM(amount) AS amt FROM payment GROUP BY customer_id ORDER BY amt DESC LIMIT 10;

####更新数据

		UPDATE customer SET last_name='DAY-WEBB',last_update=last_update WHERE customer_id=245;


####删除数据

		DELETE FROM customer WHERE customer_id=245;