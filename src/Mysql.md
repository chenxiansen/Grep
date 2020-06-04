### Mysql常用命令
##### 连接
    mysql   -u用户名 －p用户密码 -h主机地址         
    exit    退出
##### 修改密码
    mysqladmin -u用户名 -p旧密码 password 新密码
    select host,user from mysql.user;   查看数据库已经建立的用户
    drop user '用户名'@'%';             删除MySQL已经创建的用户: 
    grant all privileges on test_db.* to root@'192.168.1.101' identified by '123456';
    （特定ip地址允许访问）
    grant all privileges on test_db.* to root@'%' identified by '123456';
    （所有地址都允许访问）
    flush privileges;                   刷新权限
##### 创建数据库
    create database <数据库名>
##### 显示数据库
    show databases;
##### 删除数据库
    drop database <数据库名>
    drop database if exists <数据库名>;     删除一个不确定存在的数据库
##### 连接数据库
    use <数据库名>
##### 常用操作
    select database();                  当前选择的数据库
    select version();                   显示MYSQL的版本
    select now();                       显示当前时间
    select year(CURRENT_DATE);          显示年
    select month(CURRENT_DATE);         显示月
    select dayofmonth(CURRENT_DATE);    显示天
    select "HAPPY NEW YEAR!";           显示字符串
    select ((1 * 3) / 5 ) + 9;          当计算器
    select concat(firstname," ",lastname) as username  from xxx where age = 18; 拼接字符串
##### 创建表
    create table <表名> ( <字段名1> <类型1> ,..<字段名n> <类型n>);
    create table MyClass(
    > id int(4) not null primary key auto_increment,
    > name char(20) not null,
    > sex int(4) not null default '0',
    > degree double(16,2));
##### 删除表
    drop table <表名>
    drop table if exists <表名> ;     删除一个不确定存在的表
    drop table                        删除当前库所有表，慎用
##### 插入数据
    insert into <表名> ( <字段名1>,..<字段名n > ) values ( 值1 ), ( 值n )
    insert into MyClass values(1,'Tom',96.45),(2,'Joan',82.99), (2,'Wang', 96.59);
##### 查询数据
    select <字段1，字段2，...> from < 表名 > where < 表达式 >     
##### 删除数据
    delete from 表名 where 表达式
    delete from MyClass where id=1;
##### 修改数据
    update 表名 set 字段=新值,… where 条件
    update MyClass set name='Mary' where id=1;
##### 增加字段
    alter table 表名 add字段 类型 其他;                          加字段
    例：alter table MyClass add passtest int(4) default '0'
    alter table 表名 add index 索引名 (字段名1[，字段名2 …]);   加索引
    例：alter table employee add index emp_name (name);
    alter table 表名 add primary key (字段名);                   加主关键字的索引
    例：alter table employee add primary key(id);
    alter table 表名 add unique 索引名 (字段名);                 加唯一限制条件的索引
    例：alter table employee add unique emp_name2(cardnumber);
    alter table 表名 drop index 索引名;                          删除某个索引
    alter table table_name change old_field_name new_field_name field_type;
    （修改原字段名称及类型：）
    alter table table_name drop field_name;                      删除字段
##### 修改表名
    rename table 原表名 to 新表名;
    例：rename table MyClass to YouClass;
##### 备份数据库
    mysqldump -u用户名 -p密码  数据库名 > 导出的文件名           导出整个数据库
    例：mysqldump -u user_name -p123456 database_name > outfile_name.sql
    mysqldump -u 用户名 -p密码 数据库名 表名> 导出的文件名       导出一个表
    例：mysqldump -u user_name -p123456 database_name table_name > outfile_name.sql
    mysqldump -u user_name -p密码 -d –add-drop-table database_name > outfile_name.sql
    （-d 没有数据 –add-drop-table 在每个create语句之前增加一个drop table）
    source xxx.sql;                                              外部导入sql文件
    