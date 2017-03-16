		SELECT
			a.first_name,a.last_name,
			COUNT(fa.film_id) AS appearnce_count
		FROM 
			film_actor AS fa
			JOIN actor AS a ON a.actor_id = fa.actor_id
		GROUP BY 
			fa.actor_id
		ORDER BY
			a.first_name ASC
		LIMIT 5;


####JOIN的类型

MySQL提供三种join类型：

* INNER JOIN：默认是该类型

		SELECT * FROM foo f INNER JOIN bar b ON b.foo_id = f.foo_id;

		MySQL比较foo表和bar表中的每一行，根据ON条件来决定匹配的对，匹配的行会连接在一起。
* LEFT OUTER JOIN

		返回与INNER JOIN相同的行，但是也包括来自JOIN关键字左边的那个数据表中未匹配的行
* RIGHT OUTER JOIN

		返回与INNER JOIN相同的行，但是也包括来自JOIN关键字右边的那个数据表中未匹配的行


####改变数据表

		ALTER TABLE actor ADD COLUMN bio VARCHAR(255) AFTER last_name;

		ALTER TABLE actor DROP COLUMN bio;