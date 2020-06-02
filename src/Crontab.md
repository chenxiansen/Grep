#crontab常用命令集合
====
     usage:	crontab [-u user] file
     	crontab [-u user] [ -e | -l | -r ]
     		(default operation is replace, per 1003.2)
     	-e	(edit user's crontab)
     	-l	(list user's crontab)
     	-r	(delete user's crontab)
     	-i	(prompt before deleting user's crontab)
     	-s	(selinux context)   
    service crond start   启动服务
    service crond stop    关闭服务
    service crond restart 重启服务
    service crond reload  重新载入配置
    service crond status  查看状态
##配置参数
----
    * * * * * /command path  
    #####前5个字段分别表示：
    分钟：0-59
    小时：1-23
    日期：1-31
    月份：1-12
    星期：0-6（0表示周日）
##还可以用一些特殊符号：
----
    *： 表示任何时刻
    ,：　表示分割
    －：表示一个段，如第二端里： 1-5，就表示1到5点
    /n : 表示每个n的单位执行一次，*/1, 就表示每隔1个小时执行一次命令。也可以写成1-23/1.
##示例
----
    43 21 * * *               21:43 执行
    15 05 * * * 　　          05:15 执行
    0 17 * * *                17:00 执行
    0 17 * * 1                每周一的 17:00 执行
    0,10 17 * * 0,2,3         每周日,周二,周三的 17:00和 17:10 执行
    0-10 17 1 * *             毎月1日从 17:00到7:10 毎隔1分钟 执行
    0 0 1,15 * 1              毎月1日和 15日和 一日的 0:00 执行
    42 4 1 * * 　 　          毎月1日的 4:42分 执行
    0 21 * * 1-6　　          周一到周六 21:00 执行
    0,10,20,30,40,50 * * * *  每隔10分 执行
    */10 * * * * 　　　　　　  每隔10分 执行
    * 1 * * *　　　　　　　　  从1:0到1:59 每隔1分钟 执行
    0 1 * * *　　　　　　　　  1:00 执行
    0 */1 * * *　　　　　　　  毎时0分 每隔1小时 执行
    0 * * * *　　　　　　　　  毎时0分 每隔1小时 执行
    2 8-20/3 * * *　　　　　　 8:02,11:02,14:02,17:02,20:02 执行
    30 5 1,15 * *　　　　　　  1日 和 15日的 5:30 执行
##附录
----
    例1：30 2 * * * /data/app/scripts/hotbackup/hot_database_backup.sh &
    & 后台执行命令
    
    例2：command >out.file 2>&1 &
    2>&1表示所有的标准输出和错误输出都将被重定向到一个叫做out.file 的文件中。
    0表示键盘输入，1表示标准输出，2表示错误输出
    
    例3：0 2 * * * /u01/test.sh >/dev/null 2>&1 &
    这句话的意思就是在后台执行这条命令，并将错误输出2重定向到标准输出1，
    然后将标准输出1全部放到/dev/null 文件，也就是清空。
    
    
    
