#   Linux学习笔记
 ##  基本的shell命令
  - [linux命令分类](#linux命令分类)
  - [shell类型](#shell类型)
  - [shell的内建命令](#shell的内建命令)
  - [结构化命令](#结构化命令)
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