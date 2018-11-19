#MySQL错误笔记
		常用jdbc:mysql://localhost:8888/students?useUnicode=true&characterEncoding=utf-8&useSSL=false
##字符串问题

> Unknown initial character set index '255' received from server. Initial client character set can be forced via the 'characterEncoding' property.
> 
> 原因：字符集的问题，这种情况一般要检查 程序编码 、 mysql编码 、web服务器编码 这三种编码是否一致。

* 解决方法
> 后面加上 ?useUnicode=true&characterEncoding=utf8

		String url = "jdbc:mysql://localhost:8888/
				students?useUnicode=true&characterEncoding=utf8";
					String username = "root";
					String password = "123456";

##运行time_zone问题

>mysql 运行报错
>
>The server time zone value 'ÖÐ¹ú±ê×¼Ê±¼ä' is unrecognized or represents more than one time zone.

* 解决方法：从错误即可知道是时区的错误，因此只要将时区设置为你当前系统时区即可，
> 在mysql 语句中输入
> 
		SET GLOBAL time_zone='+8:00'   
		或者加上：
  		&serverTimezone=GMT%2B8
##证书问题SSL
* 在JDBC连接Mysql数据库的过程中出现了如下的警告信息:


		WARN: Establishing SSL connection without server's identity verification is not recommended.  
		According to MySQL 5.5.45+, 5.6.26+ and 5.7.6+ requirements SSL connection must be       
		established by default if explicit option isn't set. For compliance with existing   
		applications not using SSL the verifyServerCertificate property is set to 'false'. 
		You need either to explicitly disable SSL by setting useSSL=false, or set 
 		useSSL=true and provide truststore for server certificate verification.

>是Mysql数据库的SSL连接问题，提示警告不建议使用没有带服务器身份验证的SSL连接，是在MYSQL5.5.45+, 5.6.26+ and 5.7.6+版本中才有的这个问题。解决办法在警告中已经说明了：

* 解决方法  

		1.在数据库连接的url中添加useSSL=false;  
		2.url中添加useSSL=true，并且提供服务器的验证证书。

##SQLyog错误2058
* 解决方法
		
		windows 下cmd 登录 mysql -u root -p 登录你的 mysql 数据库，然后 执行这条SQL：
		
		 ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'password';
		
		password 是你自己设置的root密码

