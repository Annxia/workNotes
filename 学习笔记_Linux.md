## Linux相关知识

### vi相关知识
1. vi命令模式功能--光标移动    
    - G：移动到文件最后
    - gg:移动到文件开头
    - 0或^:光标移动到所在行的行首
    - $:光标移动到所在行的行尾
    - 光标的上下左右移动：使用键盘上的方向键，或者kjhl对应上下左右
    - Ctrl+f:往下翻一页
    - Ctrl+b:往上翻一页
    - x:删除  
        x:del   X:backspace 
        3x:删除光标所在位置后的3个字符，包括光标所在的位置，如果不小心先按了数字3，可以按ESC取消    
    - dw:删除光标所在处到词尾的内容
    - dd:删除光标所在行，3dd表示删除光标所在位置往下的3行，包括光标所在行。   
    - yw:复制光标所在处到词尾的内容
    - yy:复制光标所在行
    - p:粘贴(包括前面复制操作或删除操作的内容)
    - r:取代光标所在处的字符    
        R:连续取代字符直到按ESC为止 
    - u:(undo)撤销之前的操作


2. 底线模式功能
    - 在命令模式下面输入冒号进入底线模式
    - set nu(set number):显示行号   
      set nonu:不显示行号
    - #：#是你要输入的数字，再按回车，将跳到数字指定的行
    - /关键字:先按/，再输入你要寻找的字
        - 可以输入n,进行向下连续查找，N是往上查找
        - set ic:忽略大小写
        - set noic:不忽略大小写

    - 在底线模式下输入"1,$s/string/replace/g"会将全文的string字符取代为replace字符串    
        - 或者"%s/string/replace/g"
        - 1,$表示从第一行到最后一行
        - s表示替换
        - g表示每行全部替换
        - "1,20s/string/replace/g":将1至20行间的string替代为replace字符串
        - "5s/string/replace/g":只替换第5行
        - "# w filename":如果你想摘取文章的某一段，存成另一个文件，可以用这个指定#代表行号，例如"30,50 w nice"    

    - 保存、退出
        - :w filename---将文件保存为filename
        - :wq---保存文件并退出vi
        - :q!---强制退出vi并不爆粗当前更改内容
        - :W!---强制写文件，如果该文件属性为只读，那么也强制更改该文件并退出
        - :f---查看当前文件信息
        - :edit---在vi里面打开另一个文件

### Linux文件系统目录
1. Linux系统常见目录
    
    目录名 | 作用
    --- | ----
    / | Linux系统的根目录
    /etc | 系统管理和配置文件
    /home | 用户主目录，比如用户user的主目录就是/home/user
    /boot | Linux系统的内核文件放在该目录下面
    /sbin | 系统管理命令，这里存放的是系统管理员使用的管理程序
    /root | 系统管理员的主目录
    /bin | 常用可执行文件，主要有:cat,chmod,chown,data,mv,mkdir,cp,bash等(基本是单人维护模式下还能够被操作的指令)
    /dev | 设备文件，如/dev/cd0
    /usr | 用户级应用程序和文件几乎都在这个目录下面
    /proc | 一个虚拟文件系统，放置的数据都是在内存当中。例如系统核心、进程信息、设备的状态及网络状态等
    /tmp | 公用的临时文件存储点，存放一些临时文件
    /mnt | 系统提供这个目录是让用户临时挂载其他的文件系统
    /lib | 一些库文件

2. 查看文本文件内容     
    - cat命令：短文件，后面接多个文件的时候会自动拼接
    - less命令：长文件
        - k：向上一行
        - j：向下一行

3. 查看文件属性、目录内容   
    - ls 命令
        - 不加参数：列出当前目录的内容
        - -R：所有子目录的内容
        - -l：列模式列出详细信息

4. 通配符

    模式 | 匹配对象
    ---|---
    `*` | 所有文件
    `g*` | 文件以g开头的文件
    `b*.txt` | 以b开头的，格式为txt的文件
    `?`| 匹配任意一个字符
    `[list]` | 匹配list中的任意单一字符
    `[^list]` | 匹配除list中的任意单一字符以外的字符
    `[c1-c2]` | 匹配c1-c2中的任意单一字符，如：[0-9][a-z]
    `{string1,string2,...}` | 匹配string1或string2(或更多)其一字符串
    `{c1..c2}` | 匹配c1-c2中全部字符，如{1..10}

5. find命令          
    find 目录名 条件    
    - -name name：指定要被寻找的文件或目录名称，可用通配符  
    - -type x：以文件类型作为寻找条件；文件类型x为d是目录；x为f是文件   

6. diff命令 
    diff -y 文件名1 文件名2:用在文件大致相同的情况下       
    输出解释：  
    `|` ：显示文件不同的行
    `>` : 显示右边文件比左边文件多出来的行
    `<` : 显示左边文件比右边文件多出来的行  

7. **grep命令**     
    文本过滤器，效率高

    常用参数 | 解释
    -c | 只输出匹配行的计数
    -i | 不区分大小写
    -h | 查询多文件时不显示文件名
    -n | 显示匹配行及行号
    -v | 显示不包含匹配文本的所有行
    -F | 指明pattern非正则表达式
    -A<n> | 同时显示该行之后的n行的内容
    -B<n> | 同时显示该行之前的n行的内容

8. wc命令：文件内容统计      
    - wc -l /etc/passwd :统计/etc/passwd文件有多少行    
    - wc -c /etc/passwd: 统计/etc/passwd文件有多少个字节    
    - ps -ef | wc -l:带着管道符，统计共有多少个进程 

9. du命令:查看目录使用空间      
    du -sh : 显示指定目录的磁盘占用率   
    du -ah : 显示指定目录及子目录和文件的磁盘占用率

10. split：文件分割操作 
    split [-dl] 文件 前缀   
    缺省按行分割，缺省前缀为x   
    -b ：设定分割完成后的文件大小，单位为b,k,m      
    -l ：以行数进行分割，例如  -l 5         
    -a ：指明后缀长度       


## 文件权限管理
1. Linux用户，用户组：/etc/passwd 
   root用户 
   普通用户     
   系统用户  

2. chmod命令
    - chmod [who][op][permission] file...       
        例如：      
        chmod u+x file1     
        chmod ug+w test     
        chmod a-x abc.c     
        chmo u+rwx aaa.txt      

        who项表示用户类型，它的内容为以下的一项或多项          

        who | 用户类型
        -- | --
        `u` | 拥有者(user---owner)   
        `g` | 与拥有者同一组的用户(group)
        `o` | 其他人(others)
        `a` | 所有人(all)   

    - chmod u=rwx myfile       
      chmod u=rwx,g=rx,o=r myfile   

    - chmod 755 myfile   

## 进程管理
1. ps 命令查看进程  
    - 同一个用户同一个终端  
    - ps -ef    
        e表示所有，f表示full-format，尤其是PPID和command内容
    - ps axu    
        ax表示所有，u表示user-oriented

2. 执行一个进程时加& ，表示在后台执行       
    eg:python runfor.py 60 &    

3. nohup 与后台进程     
    例：nohup python runfor.py & ：此时关闭终端不会退出，适合做长时间的备份的运行程序。  
    原因：关闭终端时候有的shell会发送SIGHUP信号给子进程，子进程就会退出；加上nohup,关闭终端时，子进程就不会收到SIGHUP信号       

4. jobs 列出后台进程   
    jobs 显示后台进程id号<nums>        
    fg <nums> ：将后台进程调到前台运行 
    Ctrl + z：将进程挂起，此时jobs查看被挂起的进程显示是stopped 
    bg <nums> ：可让进程在后台执行  

5. 进程的两种终止方式   
    - 自行终止
        - 任务执行完成，比如ps查看
        - 用户让其退出，比如 shell exit
        - 异常退出，比如 程序里有除0的代码
    - 用户手动杀死进程  
        - kill PID : SIGTERM
        - kill -9 PID : SIGKILL
        - Ctrl+C : SIGINT(前台进程)
        - 只能是owner和root才能杀死进程 

## 管道和重定向
1. 重定向
    - `>`:覆盖
    例：ps -ef > out 或者 ps -ef 1 > out   
    0:stdin(标准输入)  1:stdout(标准输出)  2:stderr(标准错误)
    例：ps -ef > /dev/null:感觉是将输出丢弃掉
    - `>>`:追加

2. 同时重定向stdout和stderr到同一个文件     
    Command > both 2 >&1 (反过来不行，&是转义符：把2标准错误重定向到1标准输出)     
    Command & > both(bash 4支持)        
   同时重定向stdout,stderr到不同的文件        
    command > out 2 > err       

3. 管道     
    经常需要将一个命令的输出内容，给另一个命令作为输入的内容进行处理        
    例：ps -ef | grep python        

4. 环境变量     
    - 什么是shell变量   
        a=1;b=2 有名字的对象    echo $a：查看变量的值       
    - 什么是shell环境变量       
        特殊意义的变量，用来影响进程的行为，可以传递给子进程  
    - printenv：查看所有环境变量   
      echo $PATH：查看PATH环境变量  
      export PATH=./:$PATH(将当前路径./加入环境变量)：临时有效，此时再执行一下source .bash_profile，就可以永久有效

      vim  .bash_profile:将文件里的PATH变量修改：永久有效            
    

## 网络接口配置     
1. ifconfig 

2. 禁用、启用网络接口   
    - ifdown eth0 / ifup eth0    
    - ifconfig eth0 down / ifconfig eth0 up

3. 直接查看IP地址   
    ip addr ：显示IPV4和IPV6地址        
    ip -4 addr      
    ip -6 addr   

4. 命令行方式配置IP（IP对应网络接口，而不是网卡)
    - ifconfig eth0 192.168.79.10 netmask 255.255.255.0 up      
        **重启就会失效**    
        eth0一般对应的是第一个网卡，192.16.0.1是给eth0配置的ip地址      
        netmask 255.255.255.0 配置的是子网掩码，不加这个命令表示不修改子网掩码      
        up是表示立即激活，现在的版本也可不加                 
    - 一块网卡配置多个IP地址    
        ifconfig eth0:1 192.168.79.11 netmask 255.255.255.0      
        ifconfig eth0:2 192.168.79.12 netmask 255.255.255.0     

    - 永久生效的配置方法：修改/etc/sysconfig/network-scripts/ifcfg-eth0文件 
        ```
        DEVICE=eth0             #物理设备名     
        TYPE=Ethernet       
        HWADDR="00:0C:29:1B:8A:2E"
        BOOTPROTO:static        #[static|dhcp]      
        IPADDR=192.168.79.111   #IP地址
        NETMASK=255.255.255.0   #掩码值
        NETWORK=192.168.79.0    #网络地址
        GATEWAY=192.168.79.1    #网关地址
        ONBOOT=yes
        NM_CONTROLLED=no    
        ```
        修改完内容： service network restart    
        建议：每种配置脚本都新创建一个做备份    

5. Ping命令     
    - 连通性检查；网速检查  

    - ping -c <测试数据包数量> <目的主机地址>   
        例如：ping www.163.com  
        关注time字段

6. 域名查询：
    - nslookup <域名>
    - host <域名>





    













