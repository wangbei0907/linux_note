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
   - 命令行参数  $0是程序名 $1是第一个参数 $2是第二个参数 