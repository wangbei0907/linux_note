#   Linux学习笔记
 ##  基本的shell命令
  - linux分类
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
	- mount 挂载命令 
	- mount –t type device directory 手动挂载媒体设备命令
	- mount –t vfat /dev/sdb1 /media/disk
	- umount 卸载命令
	- umount [directory| device]
	- df 查看所有磁盘空间
	- df –h
	- du 特定目录的磁盘情况
	- sort 排序命令
	- grep [option ] pattern [file]
	- grep –n a test.111 搜索包含a的行显示行号
	- grep –n –v a test.111 反向搜索、
	- gzip myfile 压缩文件
	- 解压缩 tar –zxvf filename.tgz 解压

### 环境变量
 