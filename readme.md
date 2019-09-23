#   Linux学习笔记
 ##  基本的shell命令
  - [linux命令分类](#linux命令分类)
  - [shell类型](#shell类型)
  - [shell的内建命令](#shell的内建命令)
  - [结构化命令](#结构化命令)
  - [创建函数](#创建函数命令)
  - ####linux命令分类
    - cd  指向文件目录列表  
	- ls –l 查看文件基本信息
	- touch 新建文件
	- cp 复制文件  cp –R XXX/  XX2
	- ls –l aaa
	- ln 链接文件 ln –s 
	- mv aa aa1 修改文件名称
	- rm –ir directory 删除多个文件目录和文件 有删除提示
	- rm –rf directory 删除文件没有提示 
	- file 查看文件
	- cat  -n aaa 查看文件内容带行号 
	- more /etc/aa 显示文本文件内容 
	- less 查看文件内容
	- head -5 aaa 显示前五行
	- tail –n 2 aa只显示文件最后两行
	- ps –ef 显示所有进程信息
	- top 显示实时cpu的概括信息
	- kill 结束进程
	- mount 挂载命令 挂载存储设备
	- mount –t type device directory 手动挂载媒体设备命令
	- mount –t vfat /dev/sdb1 /media/disk
	- umount 卸载命令
	- umount [directory| device]
	- df 查看所有磁盘空间
	- df –h
	- du 特定目录的磁盘情况
	- sort 排序命令 对大数据文件进行排序
	- grep [option ] pattern [file] 搜索数据   快速检索大数据文件来查找特定信息
	- grep –n a test.111 搜索包含a的行显示行号
	- grep –n –v a test.111 反向搜索、
	- gzip myfile 压缩文件
	- 归档文件  tar –zxvf filename.tgz 解压
  - #### shell类型
    -  归档文件  tar –zxvf filename.tgz 解压
    -  ls -l /bin/sh =>bash
    -  bash 创建新的shell程序子shell ps -f 查看新增的子shell bash命令输入三次，创建三个子bash 
    -  ps -forest 查看子shell之间的嵌套关系 exit 退出子shell 和退出当前用户登录
  - #### shell内建命令 
    - which ps
    - type -a ps
### 环境变量
  环境变量分为局部环境变量和全局环境变量
  - echo 显示变量的值 
  局部环境变量只有在定义它的进程中可见。
  系统环境变量都是大写，用户环境变量均使用小写字母，变量名区分大小写，赋值不允许空格
   echo $my_variable
   $my_variable="aaaa"
   export  （变量名） 命令使其变成全局变量
   子shell改变变量的值不会反映到父shell中
  - 删除环境变量,如果在子shell中删除环境变量 再父shell中依然有效
   unsert  my_variable
  - 数组变量 
   mytest=( a b c dd e) 
   echo ${mytest[2]}  显示所有环境变量echo ${mytest[*]}
   unset mytest[2] 删除数组中的某个值
   ### Linux 文件权限
   ##### linu用户
   - /etc/passwd 查看所有用户
   - /etc/shadow 系统密码管理
   - 添加新用户
     - useradd -m test -m创建home目录
   - 删除用户 
     - userdel -r 删除用户 -r会删除home目录以及邮件目录
   - 修改用户 
      - 1、usermod 
      - 2、passwd 和chpasswd 修改用户密码
       passwd test  修改自己的密码 
       chpasswd 批量修改用户密码
       chpasswd < users.txt
       - chsh 修改用户登录的shell
       - chfn 将用户的finger命令的信息存进备注字段
   ##### linu组
   - /etc/group
   - groupadd 创建新组
   - groupmod 修改组
   ### 文件的权限
   - rwx 文件的属主
   - rwx 文件的属组
   - r-x系统的其他人
   umask设置所创建的文件和目录的默认权限
   - chmod 760 修改文件和目录的安全设置 ，只有文件的属主才能改变文件或目录的权限
   - chmod u+x filname
   - chown options owner[.group] file改变文件的属主
   - chgrp shared newfile  更过文件或目录的默认属组
   - usermod -aG groupname username 修改用户组，归档到某个组里
   ### 管理文件系统
   - fdisk /dev/sdb 创建分区
   ### 安装软件程序
   - 其他系统
     - aptitude 查看已经安装哪些软件
       - aptitude show  包名 查看包名的详情
   - redhat系统
     - yum list installed 查看已经安装哪些软件
      - yum list installed xxx 查看包是否安装
      - yum provides /etc/yum.conf 查看配置文件归属
     - yum 安装文件
      - yum localinstall package_name.rpm
     - yum 更新文件
      - yum update package_name
     - yum 卸载软件
       yum remove package_name
       yum erase package_name 删除软件和它所有文件
       yum clean all 处理损坏的包依赖关系
     - tar 源码安装
      - tar -zxvf package_name.tar.gz
   - 编辑文件
     - vim filename q!退出不保存 q:退出 wq保存文件并退出
     - 替换命令 :s/old/new/  
     - :s/old/new/g: 一行命令替换所有old
     - :n,ms/old/new/g: 替换行号n和m之间所有的old
     - :%s/old/new/g: 替换整个文件的所有的old
     - nano编辑器
     - gedit 编辑器
   - 结构化命令
     - if-then
     - if-then-else 
     - fi 代表说明语句结束了
     -  嵌套if-then-elif-then-else-then-fi
     - test 命令提供if-then语句中测试不同条件的途径，如果test命令中列出的条件成立，test命令就好退出
     if test condition -then commands -fi 或者 if [ condition ]-then-commands-fi 方括号定义了测试条件
     - 数值比较
       - n1 -eq n2 检查n1是否与n2相等
       - n1 -ge n2 检查n1是否大于或等于n2
       - n1 -gt n2 检查n1是否大于 n2
       - n1 -le n2 检查n1是否小于或等于 n2  
       - n1 -lt n2 检查n1是否小于n2 
       - n1 -ne n2 检查n1是否不等于n2 
       if [ $value -gt 5 ]
   - 字符串比较 
      - str1 = str2 str != str2 检查str1是否和str2不同  
      - -n str1 检查str1的长度是否非0  
      - -z str1 检查str1的长度是否为0
      - str1 < str2 检查str1是否比str2小
       字符串比较 小写字母ascii大于大写字母
   - 文件比较
     - -d file 检查file是否存在并是一个目录
     - -e file 检查file是否存在
     - -f file 检查file是否存在并是一个文件
     - -r file 检查file是否存在并可读
     - -s file 检查file是否存在并非空    
     - -w file 检查file是否存在并可写
     - -x file 检查file是否存在并可执行 
     - -O file 检查file是否存在并属当前用户所有
     - -G file 检查file是否存在并且默认组与当前用户相同
     - file1 -nt file2 检查file1是否比file2新
     - file1 -ot file2  检查file1是否比file2旧
   - 复合条件测试
     -  if-then [ condition1 ] && [ condition2 ] 或者[ condition1 ] || [ condition2 ]
     - ((expression))双括号允许比较过程使用高级数学表达式   
     - [[ expression ]] 双方括号命令提供了针对字符串比较的高级特性 if [[ $USER == r* ]] then 
     - case 命令 case variable in pattern1 |   pattern2 ) commands1 ;; pattern3) commands2;; *} default commands;;esac
   ###结构化命令
   - for 命令
     - for  var in list; do.
   - 读取列表的复杂值
     - 使用转移字符（\）来将单引号转义；
     - 使用双引号来定义用到单引号的值。
     - for命令用空格来划分列表中的每个值，如果在单独的数据值中有空格，就必须用双引号将这些值圈起来
     - 从变量读取列表  $list 变量包含用于迭代的标准文本值列表，代码还是用了理你个赋值语句向$list变量包含的已有列表中添加了一个值。
     -  从命令读取值 
     - IFS环境变量定义了bash shell用作字段分隔符的一系列字符
     IFS=$'\n'
     - 用通配符读取目录 for file in /home/wt/* do done
     - 循环处理文件数据
     - 创建多个用户账户
        input="users.csv"
        while IFS=',' read -r userid name
          do 
            echo "add $userid"      
            useradd -c "$name" -m $userid
          done < "$input"          
     
   ### 处理用户输入
   - 命令行参数 ${ 10 } $0是程序名 $1是第一个参数 $2是第二个参数 如果参数中包好空格 必须使用引号(单引号或者双引号均可)
   如果脚本参数不止9个，需要修改一下变量名，第9个变量之后必须在变量数字周围加上花括号，
   - $0 是获取脚本名称 
   - $( basename $0) basename 命令返回不包含路径的脚本名。
   - 特殊参数变量
     - $# 参数统计  可以统计输入了多少个参数可以在脚本任何地方使用这个变量，跟普通变量一样
     - ${!#}代表最后一个命令行参数变量,当命令行没有任何参数时，$#为0 ${!#}变量返回命令行用到的脚本名
   - 抓取所有数据
     $*和$@可访问所有参数，$*变量会将所有参数当成单个参数，而$@变量会单独处理每个参数，这是遍历命令行参数的绝妙方法
   - 移动变量
    shift 命令 会将所有参数的位置移动一个位置，如果某个参数被移出，它的值就被丢弃了，无法再恢复！
    shift +移动的位置数 shift 2 移动2位、
   - 处理选项
     - 查找选项 （--）双破折线表明选项列表结束。在双破折线之后，脚本就可以放心的将剩下的命令行参数当做参数，而不是选项来处理了！
     要检查双破折线，只要在case语句中加一项就行了。当脚本遇到双破折线时 它会停止处理选项，并将剩下的参数都当做命令行参数。
      case "$1" in
       -a) echo "found -a"
       -b) echo "found -a"
       --) shift 
           break;;
         *) echo "$1 is not an option";;
        esac
        shift
      - 处理带值的选项
       有些选项会带上一个额外的参数值，在这种情况下，命令行看起来像下面这样./test.sh -a test1 -b -c -d test2
       当命令行选项要求额外的参数时，脚本必须能检测到并正确处理。 
      - 使用getopt命令 getopt 可以接收一系列任意形式的命令行选项和参数，并自动将他们转换成适当的格式。
        getopt optstring parameters 处理命令行选项和参数时非常方便的工具，能够识别命令行参数
        getopt ab:cd -a -b  
        set命令的选项之一是双破折号(--),将命令行参数替换成set命令的命令行值，该方法会将原是脚本的命令行参数传给getopt命令，之后再将getopt命令的输出传给set命令，用getopt格式化后的命令行参数来替换原始的命令行参数
      - set -- $(getopt -q ab:cd "$@")  
      - getopts optstring variable 每次调用它时，它一次只处理命令行上检测到的一个参数，处理完所有的参数后，它会退出并返回一个大于0的退出状态码，非常适合用解析命令行所有参数的循环中
     - 选项标准化
      - -a 显示所有对象
      - -c生成一个计数
      - -d 指定一个目录 -e 扩展一个对象 -f 指定读入数据的文件 -h显示命令的帮助信息 -i忽略文本大小写
      - -l产生输出的长格式文本
     ### 呈现数据
     - 获得用户输入
      - 基本的读取   read命令会将数据放进一个变量 
      echo -n 该选项不会在字符串末尾输出换行符，允许脚本用户紧跟其后输入数据，而不是下一行。
      read -p 指导提示符 
      read命令行中不指定变量，read命令会将它收到的任何数据都放进特殊环境变量REPLY中，REPLY环境变量会保存输入的所有数据，可以像其他变量一样使用。
      - 超时 read -t 5 -p ,-t选项指定了read命令等待输入的秒数，过期后，read命令会返回一个非零退出状态码。read -nl ,-n和l一起使用，告诉read命令在接受单个字符后退出，只要按下单个字符回答后，read命令就会接受输入并将它传给变量，无需回车。
      - 隐藏方式读取 read -s -p 输入的内容就会设置成背景色一样，不被显示出来。
      - 从文本读取 cat test |while read line  将文件的数据传给read
        do
        done 
     - stdout 代表shell的标准输出
       - >> 重定向符号，通常会显示到显示器的所有输出会被shell重定向到指定的重定向文件
      例如who >> test ,会把who的结果追加到test文件
     - stderr 通过特殊的stderr文件描述符来处理错误消息，shell或shell中运行的程序和脚本出错时生成的错误消息都会发送到这个位置、
     - 重定向错误
     - stderr   ls -al badfile 2> test ,stderr文件描述符被设成2，可以选择只重定向错误消息，将该文件描述符值放在重定向符号前
     错误信息会保存在test中，不会输出到屏幕上。
     - 重定向错误和数据
      如果想重定向错误和正常输出，必须用两个重定向符号。需要在符号前面放上待重定向数据所对应的文件描述符，然后指向用于保存数据的输出文件。
      ls -al test test2 test3 badtest 2> test6 1>test7
      错误信息输出到了test6 正常数据输出到test7
      分离了正常输出数据和错误消息
      ls -al test test2 test3 badtest &> test7 如果将STDERR和STDOUT输出重定向到一个文件使用&>
      当使用&>符时，命令生成的所有输出都会发送到同一位置，包括数据和错误。
     - 临时重定向
     将单独的一行输出重定向到STDERR,需要在文件描述符数字之前加一个&，
     echo "this is an error" >&2 echo "this is nomal ouput"
     ./test8 2> test9 结果是this is an normal output，STDOUT显示的文本显示在屏幕上，而发送给STRERR的echo语句则重定向到了输出文件test9
     此方式适合在搅拌中生成错误信息、
     - 永久重定向
       当有大量数据要重定向时， excec告诉shell在脚本执行期间重定向某个特定文件描述符。重定向每个echo语句会很繁琐，就可以用exec
        exec 2>testerror exec 1>testout
      - 在脚本中重定向输入 exec命令允许你讲stdin重定向到linux中。
      exec 0< testfile ,从testfile中获得输入数据
       while read line 
         do
            echo "line #$count:$line" 
         done
        - 创建自己的重定向
        - 创建输出文件描述符  
          exec 3>test3out 将文件描述符重定向另一个文件追加到test3out
          而不是创建一个新文件、
     - 重定向文件描述符
     stdout重定向到另一个文件描述符，再利用该文件描述符重定向回stdout
     exec 3>&1  //脚本将文件描述符3重定向到文件描述符1的当前位置
     exec 1>test14out //将stdout重定向到文件test14out,shell会将发送给stdout的输出直接重定向到输出文件，但是文件描述符3依然指向stdout原来的位置（显示器）
     echo "this is out file" 
     exec 1>&3  //脚本将stdout重定向到文件描述符3的当前位置，stdout又指向的它原来的位置显示器。
     echo "now thing should be back to normal"
     - 创建输入文件描述符
      exec 6<&0 //文件描述符6用来保存strin的位置，
      exec 0< testfile //然后脚本将stdin重定向到一个文件
        while read line
        do echo "line #$count: $line"
        count=$[ $count+1 ]
        done 
        exec 0<&6 //脚本会将stdin重定向到文件描述符6，从而将stdin恢复到原先的位置
        read -p "are you done now?" answer
        case $answer in
        y|Y) echo "goodbye"
        N|n) echo "sorry this is the end"
     - 创建读写文件描述符
    exec 3<> testfile 将文件描述符3分配给文件testfile以进行读写，
   read line <&3它通过分配好的文件描述符，使用read命令读取文件中的第一行，然后显示在
   echo "this is a test line "<&3 
   - 关闭文件描述符
   exec 3>&- 该语句会关闭文件描述符3 不再在脚本中使用它
  - 列出打开的文件描述符
   lsof
  - 清除日志文件的常用方法
   cat /dev/null > log
   cat log 
 ### 信号
 - 信号
   - Linux信号 
   1 SIGHUP 挂起进程
   2 SIGINT 终止进程
   3 SIGQUIT 停止进程
   4 SIGKILL 无条件终止进程
   15 SIGTERM 尽可能终止进程
   17 SIGSTOP 无条件停止进程，不是终止
   18 SIGTSTP 停止或暂停进程，不终止进程
   19 SIGCONT 继续运行停止的进程
   - 生成信号 Ctrl+c 会生成SIGINT 信号，并发送给shell中运行的所有进程
   - 捕获信号 trap commands signals 捕获这些信号会组织用户用ctrl+c来停止进程。
   - 捕获脚本退出 trap "echo goodbye" exit 捕获脚本的退出
   - 修改或移除捕获 在脚本不同位置进行不同的捕获处理，只需重新使用trap命令即可、
     - trap -- SIGINT 删除已设置好的捕获，恢复默认行为加上两个破折号。
     - trap - 但破折号可以恢复信号的默认行为
   - 后台模式运行脚本 ./test.sh &
   - nohup 如果关闭终端会话，后台进程也会退出，nohup可以阻止这种情况，该命令会拦截任何发送给某个命令来停止其运行的信号。
   -  查看作业 $$ 查看当前正在处理的作业process id ，./test.sh > test.out &作业作为后台进程启动，输出结果到test.out文件
   - jobs -l 查看作业pid
   bg +作业号 fg 前台模式重启作业 用ctrl+z 组合挂起前台进程，使用bg将其置入后台进程
   - 调度谦让度 优先级越高值越低 -20最高优先级 19最低优先级
   - nice 命令提高进程优先级 nice  -10 ./test.sh -> test.out &
   - renice 改变系统上已经运行命令的优先级，
   renice -n 10 -p 1011 (进程id)
   - at计划执行作业 at [-f filename] time 
   - 获取作业的输出 at -f test.sh now 
   - atq 查看等待的作业 会列出作业号 atrm 删除等待中的作业
   - cron时间表 * * * * * * （分 时  天 月 周）（min hour dayofmouth month dayofweek)
   三字符的文本值(mon tue wed thu fri sat sun)(1,2,3,4,5,6,0)
   00 12 * * * if ['date +%d -d tomorrow' = 01 ];then;command 每个月最后一天中午12点执行命令
   - 构建cron时间表
   crontab -l 查看所有的时间表，浏览cron目录，如果脚本每天需要执行，将脚本复制到daily目录即可
  ### 创建函数
   - function 函数名 获取函数返回值 用echo语句来显示计算的结果，脚本函数使用echo语句返回值。
   - 函数中使用变量 
   function fun1{ echo $[ $1 * $2 ]}函数中使用了1,2两个变量，它与脚本主体中的$1和$2不同，要在函数中使用这些值必须在调用函数的时手动传过去、
   - 函数中处理变量 $value 在函数外定义并被赋值，当函数db1被调用时，该变量及其值在函数中都有效，如果变量在函数中赋予了新值，那么新值依然有效。
   - 局部变量 local关键字 只能在函数中使用
   - 数组变量作为函数参数 函数只会取数组变量的第一个值
   - 创建库，创建包含脚本中所需函数的公用库文件，在用到这些函数的脚本文件中，使用在脚本中运行库文件source命令，. ./test。
   - 在.bashrc文件中定义函数，shell每次启动都会在主目录下查找这个文件，自动启动这个函数。
 ### sed和gawl
  - sed option script file (sed命令) script参数制定了应用于流数据上的单个命令，如果需要多个命令，要么使用-e选项在命令行中指定，要么使用-f选项在单独的文件中指定
 ### 编写脚本实用工具
 - 归档 tar -zcf new.tar /wt/server/*.*  创建工作目录归档文件(压缩文件)
 - 创建归档文件的存放位置 
 