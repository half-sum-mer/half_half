十一、虚拟机网络

(一)配置网络

1. 检查虚拟网络编辑器
- 以管理员方式运行VMware
- 打开虚拟网络编辑器
- 查看NAT方式下，虚拟子网的网段 如 192.168.148.1

2\.检查虚拟网卡

控制面板，“网络与共享中心 | 更改适配器设置”

默认地，有VMnet1和VMnet8两个虚拟网卡

(\*)如果没有找到VMnet1/VMnet8，请卸载VMware重装

注意：以管理员方式运行安装程序，会更好

3\.检查虚拟机的网络配置：NAT模式

首先，Ubuntu在“继续运行此虚拟机”下面有编辑

网络适配器            NAT

网络连接处选择“NAT模式”

(\*)一般可以选择“桥接模式”，子网是随即分配的

(二)联网设置

1. 检查虚拟机硬件是否为NAT方式

1. 登录Ubuntu系统，右上角设置

设置面板左侧，“网络”

检查IPv4/DHCP设置(默认即可)

1. 检查IP地址

1. 访问外网测试

在终端输入：

ping www.baidu.com

按CTRL+C中断

我们经常使用ping操作检查丢包率来判断一个主机是不是可以连通

注意：宿主本机必须已经连接外网

(四)与宿主机的互联

检查IP地址(每个人的地址不同)

虚拟机：192.168.148.128

宿主机：192.168.148.1

(i)虚拟机与宿主机的互联

在宿主机的cmd终端：

ping 192.168.148.128

(ii)宿主机与虚拟机连接则不支持ping，但可以直接上网输入地址

(\*)

大概原理：

宿主机通过与路由器的LAN连接，路由器的WAN连接了外网

虚拟机通过虚拟网络连接宿主机，然后宿主机上网

(五)手动配置网络

在终端里，以命令行方式来配置网络

常用命令：ifconfig,netstat等

(\*)默认地，Ubuntu下面不带ifconfig命令

需要使用 apt软件包管理器,有些版本要apt-get

(i)安装一个软件包

apt install net-tools

(ii)移除一个软件包

apt remove net-tools

(iii)搜索

apt search xxx

(iv)列表

apt list | grep xxx

(\*)xxx为网络接口名

1. 查看网络配置

ifconfig

其中，if表示interface网络接口

会列出所有的网络接口，及各个接口的状态

1. 开启/禁用网络

sudo ifconfig xxx up

sudo ifconfig xxx down

—————————————————————————————————————————————————————————————————————

十二、FTP服务器

(一)把文件传到Ubuntu主机上的方法

1. U盘拷贝
1. 网络传输
- FTP
- SFTP

演示：使用FTP来1传输文件

客户端 FileZilla(Windows)

服务器 vsftpd(Ubuntu)

—————————————————————————————————————————————————————————————————————

十三、SSH服务器

使用SSH协议，可以实现：

1. 远程终端
1. 文件传输

演示：

1. 使用Xshell远程登录

(i)sudo apt update

(ii)sudo apt install openssh-server(安装ssh)

(iii)sudo systemctl start ssh(启动ssh)

(iv)sudo systemctl status ssh(检查ssh运行情况)

(v)sudo systemctl enable ssh(重启后也自动启动ssh)

(vi)sudo netstat -tln(查看tcp监听状态,t表示TCP,l表示listen，l表示ip状态)

(vii)sudo ufw status(查看防火墙状态)

(\*)如果防火墙激活：sudo ufw allow 22开启22端口流量

(\*\*)sudo ufw enable(开启)，sudo ufw disable(关闭)

(viii)ifconfig(查看ens33的inet的ip地址)

(ix)在Xshell文件新建，配置完后，左侧“用户身份验证”输入Ubuntu登录密码

(\*)在windows里cmd中输入：ssh galaxfy@(虚拟机地址) 也可以登录

(\*\*)如果报错，输入: ssh-keygen -R (虚拟机地址) 即删除此ip密钥重新登录

(\*\*\*)然后输入yes，之后输入用户密码

1. 使用Xftp传输文件

(i)sudo apt update

(ii)sudo apt install openssh-server(因为xftp基于ssh协议)

(iii)sudo apt install net-tools(必装网络工具)

(iv)Xftp操作同Xshell一样

(\*)配置静态ip：有线网络设置->"+"->IPv4选手动配置(网关用ip route查看)

—————————————————————————————————————————————————————————————————————

十四、文本编辑

(一)vim的用法

vi / vim,一个基于控制台的文本编辑器

gedit,一个基于GUI的文本编辑器

其中，vim是vi的升级版

1. 打开文本编辑

vim （文件名.txt）

如果目标文件存在，则打开编辑；如果不存在，会新建一个文件

(\*)如果系统上没有vim：sudo apt install vim(安装vim)

1. 切换模式

编辑模式Insert Mode:按i键

命令模式Command Mode:按ESC键

1. 推出编辑

(i)按ESC键，进入命令模式

(ii)输入":wq" 推出并保存；":q" 退出；":q!" 不保存并退出

(\*)输入：cat (文件名.txt) 查看具体内容

(二)vim的更多用法(用CSDN)

快捷键多，用法多，但vim本身就是一个低效率的工具

Linux文本文件的编辑

1. 桌面环境:gedit
1. 终端环境:
- 少量修改：vim
- 大量修改:在Windows上编辑，然后上传到Linux

(三)文本文件的上传

用notepad++可以编辑，或者其他编辑器

文本文件的换行符

Windows:\r\n

Linux:\n

可以在Notepad++里观察到此区别

视图|显示符号|显示行尾符

(\*)所以Linux到Windows传输要转换

换行符转换(notepad++里):

编辑|文档格式转换|转换为UNIX格式

(\*)注意：只有在编辑SHELL脚本时，才需要转换

其他格式的文件一般都不需要转换，如\*.xml , \*.java

示例：

Shell脚本的编辑

1. 用Notepad++打开编辑
1. 转成Unix格式(以\n结尾)
1. 上传至Linux
1. chmod +x(终端修改权限)

—————————————————————————————————————————————————————————————————————

十五、Ubuntu下的java环境

在Ubuntu下的java环境

1. JDK/JRE的安装
1. Java的环境变量
1. 运行普通Java程序
1. Java程序的运行脚本

(一)首先安装Java的软件包(sudo apt install (版本))

JRE：

openjdk-8-jre-headless

JDK:

openjdk-8-jdk-headless

其中，openjdk是JDK的免费版本，推荐JDK8

"headless"指无头模式，是在没有图形用户界面(GUI)的情况下运行

可以节省系统资源并提高稳定性

(二)Java环境的运行

安装openjdk-8-jre-headless

ls /usr/bin/java

默认放在/usr/bin下，不需要额外设置PATH

提示：

如果放在自定义位置，需要设置PATH

export PATH=$PATH:(你想放的地址)

1. 在Windows上开发和调试
1. 发布
- class文件
- 普通JAR文件/可执行JAR文件

两种JAR文件的运行方式不同：

java -cp your\_program.jar your.MainClass

java -jar your\_prgram.jar

3\.上传至Linux:FTP/SFTP

4\.运行程序

java -jar simple.jar

5\.权限因素，自行检查

- 程序里需要访问系统文件，如/etc/，得用root运行
- 程序里需要开启TCP端口，如80,得用root运行

(\*)注意：JavaGUI的程序不能在终端里运行

(三)Java启动脚本

一般地，需要创建一个脚本，以便快捷地启动程序

参考run\_java.sh

- 设置工作目录
- 设置必要的环境变量
- 设置JVM运行参数
- 运行程序

—————————————————————————————————————————————————————————————————————

十六、Tomcat服务器

(\*)Tomcat本身是一个Java程序，必须要有Java的运行环境

(一)下载tomcat的Linux版本

http://tomcat.apache.org/

apache-tomcat-8.5.54.tar.gz

(\*)注意：Tomcat的版本和JDK版本有对应关系

tomcat8.5对应jdk8

(以下以root身份运行)

1. 上传到Ubuntu
1. 解压缩

tar -zxvf apache-tomcat-8.5.54.tar.gz

mv apache-tomcat-8.5.54 tomcat

1. 运行Tomcat

tomcat/bin/startup.sh

1. 检查tomcat进程是否在运行

ps -ef | grep java(ps -ef列出所有进程“|”表示管道)

netstat -anp | grep 8080(查看8080端口)

6\.关闭防火墙ufw disable

7\.访问网站http://192.168.148.128:8080(个人IP地址和8080端口)

8\.关闭Tomcat

tomcat/bin/shutdown.sh

(二)Tomcat启动服务器

Tomcat的配置文件：

/opt/tomcat/conf/server.xml

至少需要修改：端口，应用目录

(i\*)修改Tomcat的端口号

网站服务一般指定80端口

<Connector port="80"protocol="HTTP/1.1"

connectionTimeout="20000"

redirectPort="8443"/>

(ii\*)指定应用目录

1. 上传网站应用

mkdir -p /opt/www/ROOT(需创建目录)

使用xftp将网站应用上传到/opt/www/ROOT(\*注意“ROOT”大写)

1. 指定应用目录

修改conf/server.xml

`	`<Host name="localhost" appBase="/opt/www"

`	      `unpackWARs="true" autoDeploy="true">



`	 `<Valve className="org.apache.catalina.valves.AccessLogValve"

`	 	`directory="logs"

`	 	`prefix="localhost\_access\_log"suffix=".txt"

`	 	`pattern="%h %l %u %t &quot;%r&quot;%s %b /">

`	`</Host>

1. 上传 server.xml

把修改后的 server.xml，传到服务器上

(iii\*)启动网站

1. 重启网站

/home/summer/tomcat/bin/shutdown.sh

/home/summer/tomcat/bin/startup.sh

1. 观察启动日志

cat /home/summer/tomcat/logs/catalina.out

1. 打开浏览器，访问(部署在/opt/www/ROOT的程序)

http://192.168.148.128

http://192.168.148.128/time

(三)Tomcat启动日志

启动tomcat服务后，应观察一下日志，看有没有错误提示

cat /home/summer/tomcat/logs/catalina.out

认识catalina.sh

1. 启动Tomcat,相当于startup.sh

tomcat/bin/catalina.sh start

1. 停止Tomcat

tomcat/bin/catalina.sh stop

1. 前台运行Tomcat(用于调试)

tomcat/bin/catalina.sh run

(四)Tomcat启动脚本

Tomcat自带的脚本：

shutdown.sh(停止，间接使用catalina.sh)

startup.sh(启动，间接使用catalina.sh)

catalina.sh

(i)创建一个脚本 run\_tomcat.sh

以后台方式运行服务

./run\_tomcat.sh start

停止服务

./run\_tomcat.sh stop

在前台方式运行  (当前窗口运行，方便打印调试)

./run\_tomcat.sh run(用ctrl+c可以终止一个前台进程)

其中，参数start/stop/run会间接地传给catalina.sh

—————————————————————————————————————————————————————————————————————

十七、程序与进程

(\*)

程序Program：指一个程序文件，如notepad.exe

进程Process：当一个程序运行起来，在操作系统内创建

一条记录，用于描述和控制它的运行

比如，打开多个notepad.exe，则得到多个进程

(一)查找进程

演示：运行多个/usr/bin/vim，并观察进程信息

ps -ef

其中，各个字段的含义：

User:执行者

PID:进程ID

PPID:父进程ID

STIME:启动时间

CMD:启动时调用的命令行

按名称查找某个进程

ps -ef | grep (进程字段)

其中，将前者输出的信息，重定向给grep命令过滤处理

(二)进程监视

top命令，相当于Windows的任务管理器

(i)查看所有进程

top

- 按上下键翻阅
- 按q或CTRL+C中止退出

(ii)查看某个进程

top -p NNN

其中，NNN为目标进程的PID

所以，可以先用ps命令查找目标进程的PID

(iii)杀死进程

使用kill命令，杀死一个进程

kill -9 NNN

或者

pkill (进程的名)

(三)前台与后台进程

前台进程：运行在前台

后台进程：运行在后台

演示：

./run\_tomcat run 以前台方式运行(CTRL+C中止)

./run\_tomcat start 以后台方式运行

(\*)

区别1：有无控制台

前台进程：

有控制台，输出至当前终端

后台进程：

无控制台，看不到输出

区别2：有无父进程

前台进程：

有父进程，父进程即为当前终端

当终端关闭时，前台进程被一同关闭

后台进程：

父进程为系统进程(1号进程，一般为初始化进程)

当终端关闭时，后台进程不受影响

(\*)前台进程可以用CTRL+C强行中止，后台进程可以用kill -9 NNN强行中止

—————————————————————————————————————————————————————————————————————

十八、Redis服务器

—————————————————————————————————————————————————————————————————————

十九、MySQL服务器
