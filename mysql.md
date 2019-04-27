## mysql
* 通过brew安装mysql:```brew install mysql```

* 查看brew安装的mysql信息：```brew info mysql```

* 查看mysql帮助信息：```mysqld --help --verbose | less```
	* 'Default options are read from the following files in the given order:
		* /etc/my.cnf 
		* /etc/mysql/my.cnf 
		* /usr/local/etc/my.cnf 
		* ~/.my.cnf

* 启动mysql:```mysql.server start```
	
* 停止mysql:```mysql.server stop```

* 连接mysql:```mysql -u root -p```

* log路径：```/usr/local/var/mysql/```


## 安装Navicat
* [Navicat 安装和破解](https://www.jianshu.com/p/f42785e55b6b)

* Navicat 连接数据库error:2059:
	* error: 2059 Authentication plugin...：是由于mysql8.0之后加密方式的改变，mysql8之前为mysql_native_password，mysql8之后为caching_sha2_password，解决当前error的方式可以通过更改加密方式为mysql_native_password实现。

	* 1.查看密码策略：```SHOW VARIABLES LIKE 'validate_password%';```
	* 2.设置密码强度等级：```set global validate_password.policy=LOW;``` // 设置密码强度等级为low
	* 3.修改加密方式：```ALTER USER 'root'@'localhost' IDENTIFIED BY 'password' PASSWORD EXPIRE NEVER;```
	* 4.更新用户密码：```ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'password';```
	* 5.刷新权限：```FLUSH PRIVILEGES;```