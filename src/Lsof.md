### lsof常用命令
    lsof                                            # 列出所有打开的文件，备注: 如果不加任何参数，就会打开所有被打开的文件，建议加上一下参数来具体定位
    lsof   /filepath/file                           # 查看谁正在使用某个文件
    lsof +D /filepath/filepath2/                    # 递归查看某个目录的文件信息，备注: 使用了+D，对应目录下的所有子目录和文件都会被列出
    lsof | grep '/filepath/filepath2/'              # 比使用+D选项，遍历查看某个目录的所有文件信息 的方法
    lsof  -u username                               # 列出某个用户打开的文件信息
    lsof -c mysql                                   # 列出某个程序所打开的文件信息，备注: -c 选项将会列出所有以mysql开头的程序的文件，其实你也可以写成 lsof | grep mysql, 但是第一种方法明显比第二种方法要少打几个字符了
    lsof -c mysql -c apache                         # 列出多个程序多打开的文件信息
    lsof -u test -c mysql                           # 列出某个用户以及某个程序所打开的文件信息
    lsof   -u ^root                                 # 列出除了某个用户外的被打开的文件信息，备注：^这个符号在用户名之前，将会把是root用户打开的进程不让显示
    lsof -p 1                                       # 通过某个进程号显示该进行打开的文件
    lsof -p 123,456,789                             # 列出多个进程号对应的文件信息
    lsof -p ^1                                      # 列出除了某个进程号，其他进程号所打开的文件信息
    lsof -i                                         # 列出所有的网络连接
    lsof  -i tcp                                    # 列出所有tcp 网络连接信息
    lsof  -i udp                                    # 列出所有udp网络连接信息
    lsof -i :3306                                   # 列出谁在使用某个端口
    lsof -i udp:55                                  # 列出谁在使用某个特定的udp端口
    lsof -i tcp:80                                  # 特定的tcp端口
    lsof  -a -u test -i                             # 列出某个用户的所有活跃的网络端口
    lsof -N                                         # 列出所有网络文件系统
    lsof -u                                         # 域名socket文件
    lsof -g 5555                                    # 某个用户组所打开的文件信息
    lsof -d description(like 2)                     # 根据文件描述列出对应的文件信息
    lsof -d 2-3                                     # 根据文件描述范围列出文件信息
    
    
    
    
    
    
    
    
    