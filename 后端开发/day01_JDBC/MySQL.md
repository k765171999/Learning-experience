## MySQL

```
net start mysql

mysql -uroot -p

show databases //输出所有数据库

use databasename //选用某个数据库

show tables   //输出所有表

use students

select * from stu 
```



> username = root
>
> password = 123456




#MySQL ERROR2013完美解决方案


版权声明：本文为博主原创文章，未经博主允许不得转载。	https://blog.csdn.net/qq_20480611/article/details/45102313
这个错误一般是安装了多个MySQL服务器导致的，解决方案如下：

1、进入MySQL安装目录：D:\Program Files (x86)\MySQL\MySQL Server 5.0\bin>

2、输入mysqld-nt -remove

		D:\Program Files (x86)\MySQL\MySQL Server 5.0\bin>mysqld-nt -remove
		The service doesn't exist!

3、输入mysqld-nt -install

		D:\Program Files (x86)\MySQL\MySQL Server 5.0\bin>mysqld-nt -install
		Service successfully installed.

4、输入net start mysql

		D:\Program Files (x86)\MySQL\MySQL Server 5.0\bin>net start mysql
		MySQL 服务正在启动 ...................
		MySQL 服务无法启动。

5、输入netstat -ano|findstr 3306

	D:\Program Files (x86)\MySQL\MySQL Server 5.0\bin>netstat -ano|findstr 3306
	  TCP    0.0.0.0:3306           0.0.0.0:0              LISTENING       5804

6、输入taskkill -f -pid 5804（此处的5804即上面的进程ID）

	D:\Program Files (x86)\MySQL\MySQL Server 5.0\bin>taskkill -f -pid 5804
	成功: 已终止 PID 为 5804 的进程。

7、输入net start mysql

	D:\Program Files (x86)\MySQL\MySQL Server 5.0\bin>net start mysql
	MySQL 服务正在启动 .
	MySQL 服务已经启动成功。

8、输入mysql -uroot -p进入MySQL



如果设置了环境变量，可在任意目录下执行以上命令
