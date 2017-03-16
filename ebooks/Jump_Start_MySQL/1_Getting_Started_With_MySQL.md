####与MySQL数据库通信

####MySQL账户和安全

root用户只应当用来执行管理级别的用户，例如创建用户账号，设置权限，清除获取缓存。

* 创建新的用户：在命令行客户端中，使用root账号连接到MySQL数据库，然后执行下面命令：

		CREATE USER 'wflytoc'@'localhost' IDENTIFIED BY 'weichuang'

		其中，wflytoc是用户名，weichuang是密码


MySQL是否允许一个用户执行某项活动，取决于该用户是否具有权限。新创建的用户没有任何权限，所以我们要显式地为用户赋予权限：

		GRANT CREATE,DROP,ALTER,INSERT,UPDATE,SELECT,DELETE,INDEX ON dbName.* To 'wflytoc'@'localhost'

不再需要的权限可以通过REVOKE来去除：

		REVOKE CREATE,DROP,ALTER,INDEX ON dbName.* TO 'wflytoc'@'localhost'