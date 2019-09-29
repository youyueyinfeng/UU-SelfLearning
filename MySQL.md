# MySQL

目的：

1.安装mysql5.7，熟练在mysql client下各常用命令的操作
2.熟悉mysql的字段类型；熟悉创建表、修改表、增删改查等常用操作；熟悉mysql权限管理
3.了解MyISAM和Innodb两个引擎的差别
4.掌握mysql索引的使用和原理
5.掌握mysql事务的使用和原理（4个隔离级别、锁机制）



## General Information

The MySQL™ software delivers a very fast, multithreaded, multi-user, and robust SQL (Structured Query Language) database server. The MySQL software is Dual Licensed. Users can choose to use the MySQL software as an Open Source product under the terms of the GNU General Public License  or can purchase a standard commercial license from Oracle.

### What is MySQL

MySQL, the most popular Open Source SQL database management system, is developed, distributed, and supported by Oracle Corporation. 

- MySQL is a database management system, managing a structured collection of data. 
- MySQL databases are relational. A relational database stores data in separate tables rather than putting all the data in one big storeroom. 
- MySQL software is Open Source.
- The MySQL Database Server is very fast, reliable, scalable, and easy to use.
- MySQL Server works in client/server or embedded systems.
- A large amount of contributed MySQL software is available.

### The Main Features of MySQL

#### Internals and Portability

- Written in C and C++.
- Works on many different platforms.
- For portability, uses **CMake** in MySQL 5.5 and up. Previous series use GNU Automake, Autoconf, and Libtool.
- Uses multi-layered server design with independent modules.
- Designed to be fully multithreaded using kernel threads, to easily use multiple CPUs if they are available.
- Provides transactional and nontransactional storage engines.
- Uses very fast B-tree disk tables (`MyISAM`) with index compression.
- Uses a very fast thread-based memory allocation system.
- Executes very fast joins using an optimized nested-loop join.
- Implements in-memory hash tables, which are used as temporary tables.
- Implements SQL functions using a highly optimized class library that should be as fast as possible. Usually there is no memory allocation at all after query initialization.

#### Connectively

- Clients can connect to MySQL Server using several protocols:
- MySQL client programs can be written in many languages. 
- APIs for C, C++, Eiffel, Java, Perl, PHP, Python, Ruby, and Tcl are available, enabling MySQL clients to be written in many languages. 
- The Connector/ODBC (MyODBC) interface provides MySQL support for client programs that use ODBC (Open Database Connectivity) connections. 
- The Connector/J interface provides MySQL support for Java client programs that use JDBC connections. Clients can be run on Windows or Unix. 
- MySQL Connector/NET enables developers to easily create.

##  Installing and Upgrading MySQL

### Which MySQL Version and Distribution to Install

The naming scheme in MySQL 5.7 uses release names that consist of three numbers and an optional suffix; for example, **mysql-5.7.1-m1**. The numbers within the release name are interpreted as follows:

- The first number (**5**) is the major version number.
- The second number (**7**) is the minor version number. Taken together, the major and minor numbers constitute the release series number. The series number describes the stable feature set.
- The third number (**1**) is the version number within the release series. This is incremented for each new bugfix release. In most cases, the most recent version within a series is the best choice.

Release names can also include a suffix to indicate the stability level of the release. Releases within a series progress through a set of suffixes to indicate how the stability level improves. The possible suffixes are:

- **mN** (for example, **m1**, **m2**, **m3**, ...) indicates a milestone number. MySQL development uses a milestone model, in which each milestone introduces a small subset of thoroughly tested features. 
- **rc** indicates a Release Candidate (RC). Release candidates are believed to be stable, having passed all of MySQL's internal testing. 
- Absence of a suffix indicates a General Availability (GA) or Production release. 

Development within a series begins with milestone releases, followed by RC releases, and finally reaches GA status releases.

### Installation

First, get compressed **tar** file `mysql-5.7.26-linux-glibc2.12-x86_64.tar.gz` from <https://dev.mysql.com/downloads/file/?id=485707>. Then follow the instruction to install the **mysql**.

```shell
# create a user and its group for mysql
groupadd mysql
useradd -r -g mysql -s /bin/false mysql
# decompress the tar file
cd /usr/local
tar zxvf /path/to/mysql-5.7.26-linux-glibc2.12-x86_64.tar.gz
ln -s full-path-to-mysql-VERSION-OS mysql
# make some initialization
cd mysql
mkdir mysql-files
chown mysql:mysql mysql-files
chmod 750 mysql-files
bin/mysqld --initialize --user=mysql 
# bin/mysql_ssl_rsa_setup
# bin/mysqld_safe --user=mysql &
```

Create the configure file and add the following configuration, or you may meet the error similar with `Access denied for user ‘root’@‘localhost’(using password: YES)` when you try to use the mysql service. 

```shell
# create the file if it does not exist
cd /etc/mysql/
sudo cp my.cnf.fallback my.cnf
# add the configuration
sudo echo -e "[mysqld]\nskip-grant-tables" > my.cnf
```

Add the directory of mysql's execute files to the PATH:

```shell
export PATH=/usr/local/mysql/bin/:$PATH
```

Start the mysql service with the user 'mysql'.

```shell
mysqld --user=root &
```

Or use `systemctl` to control mysql service.

```shell
sudo systemctl start mysqld
```

Use `mysqladmin` to test whether the service is usable.

```
mysqladmin version
```

Terminate the mysql service.

```
mysqladmin shutdown
```



## Tutorial





## Python Mysql-Connector



### Session Operation

To manage MySQL transactions in python follow these steps: –

- Create MySQL database connections in python.
- Prepare the SQL queries that you want to run as a part of a transaction. For example for bank transfer, we can combine two SQL queries(withdrawal money and deposit money query) in a single transaction.
- Set an auto-commit property of MySQL connection to false.
- Execute all queries one by one using cursor.execute()
- If all queries execute successfully `commit` the changes to the database
- If one of the queries failed to execute `rollback` all the changes.
- Catch any SQL exceptions that may occur during this process
- Close the cursor object and MySQL database connection



### Exception

- **errors.Error Exception**

This exception is the base class for all other exceptions in the `errors` module. It can be used to catch all errors in a single `except` statement.

```python
import mysql.connector

try:
  cnx = mysql.connector.connect(user='scott', database='employees')
  cursor = cnx.cursor()
  cursor.execute("SELECT * FORM employees")   # Syntax error in query
  cnx.close()
except mysql.connector.Error as err:
  print("Something went wrong: {}".format(err))
```

- **errors.DataError Exception**

This exception is raised when there were problems with the data. Examples are a column set to `NULL` that cannot be `NULL`, out-of-range values for a column, division by zero, column count does not match value count, and so on.

- **errors.ProgrammingError Exception**

This exception is raised on programming errors, for example when you have a syntax error in your SQL or a table was not found.

```python
try:
  cursor.execute("CREATE DESK t1 (id int, PRIMARY KEY (id))")
except mysql.connector.ProgrammingError as err:
  if err.errno == errorcode.ER_SYNTAX_ERROR:
    print("Check your syntax!")
  else:
    print("Error: {}".format(err))
```

- **errors.IntegrityError Exception**

This exception is raised when the relational integrity of the data is affected. For example, a duplicate key was inserted or a foreign key constraint would fail.

```python
cursor.execute("CREATE TABLE t1 (id int, PRIMARY KEY (id))")
try:
  cursor.execute("INSERT INTO t1 (id) VALUES (1)")
  cursor.execute("INSERT INTO t1 (id) VALUES (1)")
except mysql.connector.IntegrityError as err:
  print("Error: {}".format(err))
```

- **errors.InternalError Exception**

This exception is raised when the MySQL server encounters an internal error, for example, when a deadlock occurred.

- **errors.OperationalError Exception**

This exception is raised for errors which are related to MySQL's operations. For example: too many connections; a host name could not be resolved; bad handshake; server is shutting down, communication errors.

- **errors.PoolError Exception**

This exception is raised for connection pool errors.

- **errors.InterfaceError Exception**

This exception is raised for errors originating from Connector/Python itself, not related to the MySQL server.

-  **errors.NotSupportedError Exception**

This exception is raised when some feature was used that is not supported by the version of MySQL that returned the error. It is also raised when using functions or statements that are not supported by stored routines.

- **errors.DatabaseError Exception**

This exception is the default for any MySQL error which does not fit the other exceptions.



















# 参考文献

1. [MySQL 5.7 Reference Manual](http://dev.mysql.com/doc/refman/5.7/en/index.html)
2. [Linux连接mysql报错：Access denied for user ‘root’@‘localhost’(using password: YES)的解决方法](https://www.cnblogs.com/luoa/p/10843980.html)
4. [第一、第二、第三范式之间的理解和比较](https://www.cnblogs.com/ktao/p/7775100.html)
5. [第一范式，第二范式，第三范式，BCNF范式理解](https://blog.csdn.net/u013164931/article/details/79692402)
5. [Mysql数据库外键基础知识和操作](http://www.sohu.com/a/238219087_100192631)
6. [MySQL外键约束（FOREIGN KEY）](http://c.biancheng.net/view/2441.html)
7. [mysql 外键（foreign key）的详解和实例](https://blog.csdn.net/qq_34306360/article/details/79717682)
8. [MySQL的JOIN（一）：用法](https://www.cnblogs.com/fudashi/p/7491039.html)
9. [SQL系列（九）—— 子查询（subQuery）](https://www.cnblogs.com/lxyit/p/9322280.html)
10. [MySQL入门 (九) : 子查询 Subquery](https://justcoding.iteye.com/blog/2321556)











