1、pwd:显示当前所在的目录

2、cd 进入到某个目录(敲首字母 按tab键自动补全)

   cd /  转到根目录中 

   cd ~  转到当前登录用户的家目录 

   cd /目录   绝对路径

   cd test 相对路径 相对当前所在的位置来说

   

   建用户:useradd test

​         给密码：passwd test

3、ls：显示当前目录下的所有文件(包括目录)

   选项：ls -l:看文件或者目录的详细信息

​         ls -a:查看目录下的所有文件（包括隐藏文件）

4、cat命令：查看文件的内容  适合看文件内容比较少的（一屏能显示的）	

5、grep命令：到文件中搜索所要的内容

​        支持正则

6、touch命令：创建文件

7、cp命令：拷贝

​    拷贝文件: cp a.txt a_bak.txt

​	拷贝目录：cp -r aa aa_bak

​	拷贝一个文件到另外一个目录下:cp a.txt aa/

8、mv命令：移动

​    重命名：mv a_bak.txt b_bak.txt  

9、rm命令：删除

​     删除文件： rm 文件名

​	          rm -f 文件名  ：强制删除，不给确认信息

​	 删除文件夹：rm -r 文件夹

​	           rm -fr 文件夹：强制删除，不给确认信息

10、du：显示文件的大小情况

​    df：显示磁盘的情况	

11、压缩：tar -cvf 压缩包 压缩的文件	

​          tar -cvf abc.tar aa/ bb/

​	解压:tar -xvf abc.tar	

​	

​	tar -zcvf dd.tar.gz aa/ bb/   将aa bb这两个目录打到dd.tar.gz这个包中

​	tar -zxvf dd.tar.gz -C ee/   将dd.tar.gz这个包解压到ee这个目录

12、关机 ： shutdown -h now

   	重启:reboot

​	查看进程：ps -ef   ps -ef | grep java   在ps -ef的结果中搜索java

​	tomcat启动了之后又想关闭  tomcat启动了之后会占用8080端口 

​	需要去查看8080端口是否被占用 netstat -nltp就能找到进程号

​	这时只需要将该进程杀死  kill 进程号  kill -9 进程号

​	

​	查看java进程 :jps

​	

​	top：查看系统的负载情况

​	

13、文件的权限操作

   方式一：

   	文件类型   当前用户的权限(u)    用户所在组的权限(g)   其他用户的权限(o)

​	1、对文件所有者增加执行权限

​	   chmod u+x a.txt

​	2、对文件所有者去掉执行权限

​	   chmod u-x a.txt

​	3、对文件所有者所在组的用户增加权限

​	   chmod g+w a.txt

​	4、对其他用户增加(减少权限)权限

​	  chmod o-r a.txt

​	  chmod o+r a.txt

​	5、如果要对所有的用户(文件所有者  组  其他用户)

​	   chmod a+r a.txt

​	   chmod a-r a.txt

​			

   方式二：

​	 chmod 775 a.txt 

​	  rwx   rwx  r-x

​		7    7    5

14、用户的操作

​    添加用户:useradd 用户名

​	设置密码:passwd 用户名

​	切换用户：

​	  su 用户名 (用户名可以省略，省略表示的是root用户)

​	  

15、vi命令的使用

​      几种模式：

​       编辑模式  输入模式   末行模式

​       1、几种模式转换

​	      1、编辑模式--->输入模式

​	         i: 在当前光标所在字符的前面，转为输入模式；

​	         a: 在当前光标所在字符的后面，转为输入模式；

​	         o: 在当前光标所在行的下方，新建一行，并转为输入模式；

​		

​	         I：在当前光标所在行的行首，转换为输入模式

​	         A：在当前光标所在行的行尾，转换为输入模式

​	         O：在当前光标所在行的上方，新建一行，并转为输入模式；

​	     2、输入模式--->编辑模式 

​	         ESC

​	     3、编辑模式-->末行模式

​	         ：

​	        可以用!执行命令，比如 :!ls -l /etc

​	    2、打开文件

​	         1、vim /path/file

​	         2、vim +# /path/file 打开文件，并定位于第#行

​	         3、vim +：打开文件，定位至最后一行

​	         4、vim +/PATTERN : 打开文件，定位至第一次被PATTERN匹配到的行的行首

​	    3、关闭文件

​	          首先进入到末行模式(:)

​	          :q  退出

​				:wq 保存并退出

​				:q! 不保存并退出

​				:w 保存

​				:w! 强行保存

​				:wq --> :x

​		4、光标移动

​		   在编辑模式下

​		   1、逐字符移动：

​				h: 左

​				l: 右

​				j: 下

​				k: 上

​     

​     			#h: 移动#个字符

​     		2、以单词为单位移动

​				w: 移至下一个单词的词首

​				e: 跳至当前或下一个单词的词尾

​				b: 跳至当前或前一个单词的词首

​			3、行内跳转：

​				0: 绝对行首

​				^: 行首的第一个非空白字符

​				$: 绝对行尾

​			4、显示行号

​				:set number

​				:set nu

​				:set nonu（不显示行号）

​			5、行间跳转

​				#G：跳转至第#行；

​				G：最后一行

​				末行模式下，直接给出行号即可

​			6、翻屏

​				Ctrl+f: 向下翻一屏

​				Ctrl+b: 向上翻一屏

​			7、删除

​			   x: 删除光标所在处的单个字符

​			   #x: 删除光标所在处及向后的共#个字符

​			   dw:删除光标所在处的单词

​			   #dw

​				dd: 删除当前光标所在行

​				#dd: 删除包括当前光标所在行在内的#行；

​			8、复制命令

​			     y

​			9、粘贴

​			    p(P)

​			10、撤销

​			    u

​			11、查找

​			   /PATTERN

​				?PATTERN

​					n 下一个

​					N  上一个

​			12、替换

​			    将a替换为b

​			   ：%s/a/b/g

16、jdk的安装

​	1、在/opt下建两个目录 (software modules)

​	2、将本地的jdk传到/opt/software下

​	3、解压jdk压缩包 解压到/opt/modules中

​	4、配置环境变量

​		配置到/etc/profile.d下 ，新建java.sh 里面配置 JAVA_HOME和PATH

​		

​		export JAVA_HOME=/opt/modules/jdk1.8.0_171

​		export PATH=$PATH:$JAVA_HOME/bin

​	5、重新加载java.sh	

​	   source java.sh

​	卸载：

​	    rpm -qa | grep java

​	    rpm -e --nodeps  文件名

17、创建目录

   创建单个目录：mkdir 目录名 

   创建目录及子目录 ：mkdir -p 目录/子目录

18、查看文件：

​     head ：从前向后看    使用格式 head 文件名   默认看前10行

​	         如果需要看前20行   head -20 文件名

​     tail命令：tail -f 日志文件  查看日志

​	           tail -200 日志文件  

​     more命令: more 文件：  空格后翻一屏  b键前翻一瓶

​	           退出： q键退出  ctrl+c键退出

19、telnet ip 端口 :来查看端口是否可以使用

20、查看端口的使用情况: netstat -nltp

21、echo : 输出字符串 echo 字符串

​           输出变量  echo $变量名

​		   输出内容到文件中 echo 内容 > 文件名   （覆盖）

​		                    echo 内容 >> 文件名  (追加)

22、关闭防火墙

   service iptables stop

   chkconfig iptables off

修改网卡

vim /etc/udev/rules.d/70-persistent-net.rules

修改网址

vim etc/sysconfig/network-scripts/ifcfg-eth0

修改主机名

vim /etc/sysconfig/network

HOSTNAME=zookeeper01

ip配置失败后在使用此命令重启服务

service NetworkManager stop

chkconfig NetworkManager off

mkdir /opt/modules/

mkdir /opt/software

从此主机文件拷贝到主机位置

scp -r 文件位置/ root@主机名：文件位置

   