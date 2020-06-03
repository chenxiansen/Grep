Yum常用命令
====
    yum search  xxxx        查找某个包
    yum install xxxx        安装某个包
    yum remove  xxxx        删除某个包
    yum update  xxxx        升级指定软件包
    yum deplist xxxx        查询指定软件包的依赖关系
    yum localinstall xxxx   从硬盘安装rpm包并使用yum解决依赖
    yum update              升级系统
    yum list                列出所有可安装的软件包
    yum list updates        列出所有可更新的软件包
    yum list installed      列出所有已安装的软件包
    yum list extras         列出所有已安装但不在Yum Repository 內的软件包
    yum list xxxx           列出所指定软件包
    yum info xxxx           获取软件包信息
    yum info                列出所有软件包的信息
    yum info updates        列出所有可更新的软件包信息
    yum info installed      列出所有已安裝的软件包信息
    yum info extras         列出所有已安裝但不在Yum Repository 內的软件包信息
    yum provides  xxxx      列出软件包提供哪些文件  
    yum grouplist           查看系统中已经安装的和可用的软件组，可用的可以安装
    yum grooupinstall xxxx  安装上一个命令显示的可用的软件组中的一个
    yum grooupupdate  xxxx  更新指定软件组的软件包
    yum grooupremove  xxxx  卸载指定软件组中的软件包
    yum list yum\*          列出所有以yum开头的软件包
#清除YUM缓存
----
####yum 会把下载的软件包和header存储在cache中，而不会自动删除。可以使用yum clean指令进行清除
    yum clean packages          清除缓存目录(/var/cache/yum)下的软件包
    yum clean headers           清除缓存目录(/var/cache/yum)下的 headers
    yum clean oldheaders        清除缓存目录(/var/cache/yum)下旧的 headers
    yum clean, yum clean all    清除缓存目录(/var/cache/yum)下的软件包及旧的headers
    
    
    