### Find常用命令
##### 语法
    find   path   -option   [   -print ]   [ -exec   -ok   command ]   {} \;
    
    -name                   #根据文件名查找
    -perm                   #工具文件权限查找
    -prune                  #该选项可以排除某些查找目录
    -user                   #根据文件属主查找
    -group                  #根据文件属组查找
    -mtime  -n | +n         #根据文件更改时间查找
    -nogroup                #查找无有效属组的文件
    -nouser                 #查找无有效属主的文件
    -newer file1 !file2     #查找更改时间比file1新但比file2旧的IDE文件
    -type                   #按文件类型查找
    -size -n +n             #按文件大小查找
    -mindepth n             #从n级子目录开始搜索
    -maxdepth n             #最多搜索到n级目录
 ##### 常用选项
    -name       find /etc -name '*.conf'                    #查找 /etc 目录下以 conf 结尾的文件，文件名区分大小写
    -iname      find . -name test                           #查找当前目录下所有文件名为 test 的文件，文件名不区分大小写
    -user       find . -user root                           #查找文件所属用户为 root 的所有文件
    -group      find . -group root                          #查找文件所属组为 root 的所有文件
    -type       根据类型查找：如下
                f　　 文件　　　　　　　　      find . -type f 
                d　　 目录　　　　　　　　      find . -type d 
                c　　 字符设备文件　　　　      find . -type c
                b　　 块设备文件　　　　　      find . -type b
                l　　 链接文件　　　　　　      find . -type l
                p　　 管道文件　　　　　　      find . -type p
    -size       根据文件大小查询 
                -n　　小于 大小为 n 的文件
                +n　　大于 大小为 n 的文件     
                find /etc -size +10000c                     #查找 /ect 目录下，大于 10000 字节的文件  
                find /etc -size -1M                         #查找 /etc 目录下，小于 1M 的文件  
     -mtime 
                -n　　n 天以内修改的文件
                +n　　n 天以外修改的文件
                n　　 正好 n天 修改的文件
                find /etc -mtime -5 -name '*.conf'          #查询 /etc 目录下，5天以内修改 且以 conf 结尾的文件
                find /etc -mtime +10 -user root             #查询 /etc 目录下，10天之前修改，且属于 root 的文件
     -mmin　
                -n　　n 分钟以内修改过的文件
                +n　　n 分钟之前修改过的文件   
                find /etc -mmin +30                         #查询 /etc 目录下 30分钟 之前修改过的文件
                find /etc -mmin -30 -type d                 #查询 /etc 目录下 30分钟 之前修改过的目录
     -mindepth n                                            #从第 n 级目录开始搜索
                find /etc -mindepth 3                       #从 /etc 的第三级子目录开始搜索
     -maxdepth n                                            #表示至多搜索到第 n-1 级子目录
                find /etc -maxdepth 3 -name '*.conf'        #在 /etc 中搜索符合条件的文件，但最多搜索到 2级 子目录
 ##### 不常用选项  
     -nouser    find /etc -type f -nouser                   #查询没有所属用户的文件    
     -nogroup   find /etc -type f -nogroup                  #查询没有所属组的文件
     -perm      find /etc -perm 664                         #根据权限查询
     -prune     
     #通常和 -path 一起使用，用于将特定目录排除在搜索条件之外。过滤条件写在其他条件前面
     find . -path ./test -prune -o -type f                  
     #查找当前目录下的所有普通文件，但排除 test目录
     
     find . -path ./test -prune -o -path ./opt -prune -o -type f    
     #查找当前目录下所有普通文件，但排除 test目录 和 opt目录
     
     find . -path ./test -prune -o -path ./opt -prune -o -type f -a -user root  
     #查找当前目录下所有普通文件，但排除 test目录 和 opt目录，但属主为 root
     
     find . -path ./test -prune -o -path ./opt -prune -o -tyep f -a -user root -a -size +500    
     #查找当前目录下所有普通文件，但排除 test目录 和 opt目录，但属主为 root，且文件大小必须大于 500字节
    
     -newer file1    find . -newer a                        #查找当前目录下比 a 文件要新的文件
 ##### 操作查找到的文件
     -print                                                 #打印输出。 默认的选项，即打印出找到的结果
     -exec       
     #对搜索到的文件执行特定的操作，固定的格式为：-exec 'commond' {} \;   注意：{} 表示查询的结果 
     
    find /etc -type f -name '*.conf' -size +10k -exec rm -f {} \;         
    # 搜索 /etc 目录下的文件（非目录），文件以 conf 结尾，且大于 10k，然后将其删除
    
    find /data/log -name '*.log' -mtime +7 -exec rm -f \;                 
    # 将 /data/log/ 目录下以 .log 结尾的文件，且更改时间在 7 天以上的删除
    
    find /etc -type f -name '*.conf' -size +10k -exec cp {} /root/conf/ \;  
    #搜索条件同 例1 一样，但是不删除，只是将其复制到 /root/conf 目录下  
    
 ##### 逻辑运算符　
     -a　　　　         与  （默认情况查询条件之间都是 与 的关系）
     -o　　　　         或
     -not | ！　        非                    
                
