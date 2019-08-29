#   Linux学习笔记
 ##  基本的shell命令
  - [linux命令分类](#linux命令分类)
  - [shell类型](#shell类型)
  - [shell的内建命令](#shell的内建命令)
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
  - ####shell类型
    -  归档文件  tar –zxvf filename.tgz 解压
    -  ls -l /bin/sh =>bash
    -  bash 创建新的shell程序子shell ps -f 查看新增的子shell bash命令输入三次，创建三个子bash 
    -  ps -forest 查看子shell之间的嵌套关系 exit 退出子shell 和退出当前用户登录
  - ####shell内建命令 
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
   ###Linux 文件权限
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
   ###文件的权限
   - rwx 文件的属主
   - rwx 文件的属组
   - r-x系统的其他人
   umask设置所创建的文件和目录的默认权限
   - chmod 760 修改文件和目录的安全设置 ，只有文件的属主才能改变文件或目录的权限
   - chown options owner[.group] file改变文件的属主
   - chgrp shared newfile  更过文件或目录的默认属组
   