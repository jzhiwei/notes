- [常用命令](#常用命令)
    - [文件相关](#文件相关)
        - [输入输出重定向](#输入输出重定向)
        - [打包与压缩](#打包与压缩)
            - [打包与解包](#打包与解包)
            - [压缩与解压缩](#压缩与解压缩)
    - [用户与组](#用户与组)
        - [用户](#用户)
        - [工作组](#工作组)
    - [文件权限](#文件权限)
        - [chmod](#chmod)
        - [chown](#chown)
        - [chgrp](#chgrp)
        - [默认权限](#默认权限)
    - [网络相关](#网络相关)
        - [网络配置](#网络配置)
            - [网卡配置](#网卡配置)
            - [主机名配置](#主机名配置)
            - [DNS配置](#DNS配置)
    - [防火墙](#防火墙)

- - -
### 文件相关命令
|[ln](#lnlink链接文件)|[ls](#ls)|[mkdir](#mkdir)|[rmdir](#rmdirremove-empty-directory)|[rm](#rm)|[cd](#cdchange-directory)|[touch](#touch)|[pwd](#pwdprint-working-directory)|[cp](#cp)|[mv](#mv)|[cat](#cat)|[more](#more)|
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
|[less](#less)|[echo](#echo)|[file](#file)|[wc](#wc)|[grep](#grep)|[locate](#locate)|[find](#find)|[sed](#sedstream-editor)|[awk](#awk)|

### 用户与组相关命令
|[id](#id)|[whoami](#whoami---who-am-i)|[who](#who)|[last](#last---lastlog)|[w](#w)|[su](#su)|[logout](#logout)|[exit](#exit)|
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|

### 网络相关命令
|[ifconfig](#ifconfig)|[ifup](#ifup)|[ifdown](#ifdown)|[netstat](#netstat)|[nslookup](#nslookup)|[traceroute](#traceroute)|[wget](#wget)|[tcpdump](#tcpdump)|[ssh](#ssh)|[scp](#scp)|
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|



# 常用命令

## 文件相关
### ln（Link）链接文件

源文件与链接文件会相互影响，无论修改哪一个，都会同步到另一个。

    # ln [-s] source_filename dist_filename
    无参数:  创建一个硬链接文件
    -s:  创建一个符号链接文件

#### 硬链接:  
- 拥有相同的inode和存储block，文件大小、内容与目标文件相同，可以看作是一个文件
- 不能针对目录使用
- 删除源文件，不会影响硬链接文件

#### 符号链接:  
- 与Windows中的快捷方式完全一样
- 拥有自己的indoe和存储block，但是block中只保存目标文件的文件名和inode，没有实际数据
- 软链接的文件权限都为777
- 删除源文件软链接文件失效
        
#### inode

分区表中的inode号，相当于文件ID

#### 存储block

文件在硬盘中实际的存储位置。硬盘分区后是由排列的存储块所组成，一般每个存储块的大小是4KB。一个大于4KB的文件由多个存储块存储，存储块位置不是连续的。

用户查找文件的流程是先去查看分区表，通过分区表中的inode找到该文件所对应的存储块，然后再取出存储块中的数据返回给用户。
- - -
### ls

查询目录中的文件

    # ls [-aldhi] file|dir
    -a:  显示所有文件，包括隐藏文件
    -l:  显示详细信息
    -d:  查看目录属性
    -h:  人性化显示文件大小
    -i:  显示文件inode
- - -
### mkdir

创建目录

    # mkdir [-p] dir_name
    -p:  递归创建目录
- - -
### rmdir（Remove empty Directory)

删除空目录
- - -
### rm

删除文件或目录

    rm [-rif] file|dir
    -r:  递归删除目录
    -i:  交互式操作，删除前询问是否删除
    -f:  忽略不存在的文件和参数
- - -
### cd（Change Directory）

切换目录

    # cd ~:  切换到家目录
    # cd -:  进入上次目录
- - -
### touch

创建文件
- - -
### pwd（Print Working Directory）

查看当前所在路径
- - -
### cp

拷贝文件

    # cp [-adprfi] source destination
    -a:  相当于 -pdr
    -d:  若源文件是链接文件，则复制链接属性
    -p:  连同文件属性一起复制
    -r:  递归复制（用于目录）
    -f:  覆盖已经存在的目标文件，不会询问
    -i:  交互式操作，询问用户是否覆盖已经存在的目标文件
- - -
### mv

剪切或重命名文件、目录

    # mv [-if] source destination
    -i:  交互式操作，询问用户是否覆盖已经存在的目标文件
    -f: 覆盖已经存在的目标文件，不会询问
- - -
### cat 

查看文件内容

    # cat /etc/centos-release: 查看系统发行版本
    # cat /proc/meminfo: 查看内存大小
- - -
### more 

分页显示文件内容

    # more file
    空格: 向下翻页
    b: 向上翻页
    回车: 向下翻一行
- - -
### less

分页显示文件内容，与more类似
- - -
### echo


    echo -e: 输出转义字符
    # echo -e "\e[1;31mHello World.\e[0m"
    Hello World.

    echo 'value': 单引号，不能识别变量和命令，都当作普通字符串来处理
    # echo 'echo ${PS1}'
    echo ${PS1}

    echo "value": 双引号，能识别变量，不能识别命令
    # echo "echo ${PS1}"
    echo [\u@\h \W]\$ 

    echo `value`: 反引号 = $(value)，能识别变量和命令
    # echo `echo ${PS1}`
    # echo $(echo ${PS1})
    [\u@\h \W]\$

    echo {1..10}: 打印数字1~10
    echo {000..020..2}: 打印000~020，每隔两个数字打印一次

|字符|说明|
|:-:|:-:|
|\a|输出提示音|
|\b|退格键|
|\v|垂直制表符|
|\0|以八进制格式输出|
|\x|以十六进制格式输出|
|\e|改变字体颜色，\e[1; 开启颜色，\e[0m 关闭颜色|

|颜色编号|颜色值|
|:-:|:-:|
|30m|黑色|
|31m|红色|
|32m|绿色|
|33m|黄色|
|34m|蓝色|
|35m|洋红|
|36m|青色|
|37m|白色|

- - -
### file

查看文件类型

- - -
### wc

监听键盘输入，统计输入的行数、单词数和字符数。

使用Ctrl + d结束监听，统计输出结果。

- - -
### 输入输出重定向

#### 输入重定向

    wc < filename = wc filename
    wc << value: 监听键盘输入，直到输入的内容与value值匹配，会统计输入结果

#### 输出重定向

|命令|说明|
|:-:|:-:|
|命令 > 文件 2>&1 = 命令 &> 文件|以覆盖的方式把正确的输出和错误的输出都保存在一个文件中|
|命令 >> 文件 2>&1 = 命令 &>>文件|以追加的方式把正确的输出和错误的输出都保存在一个文件中|
|命令 >> 文件1 2>>文件2|把正确的输出追加到文件1中，把错误的输出追加的文件2中|
|命令 > /dev/null|把输出的结果删除掉|

#### 标准输入输出

|设备|设备名称|编号|说明|
|:-:|:-:|:-:|:-:|
|键盘|/dev/stdin|0|标准输入|
|显示器|/dev/stdout|1|标准输出|
|显示器|/dev/stderr|2|标准错误输出|

- - -
### grep

在指定文件中搜索内容

    # grep [-vni] search_content file
    -v: 显示不包含搜索内容的所有行（取反）
    -n: 显示匹配行的行号
    -i: 忽略搜索内容的大小写

- - -
### locate

在后台的数据库中搜索文件，搜索速度更快，但是只能按文件名搜索。

配置文件/etc/updatedb.conf，可以修改搜索规则。

    # locate locate: 查找用于搜索的后台数据库位置
    # updatedb: 更新后台数据库。对于新建的文件不在数据库中，需要更新。

- - -
### find

按不同条件查找文件

    # find path [option] [value]

    # find ./ [-name | iname] '[A-Z]'
    -name: 在当前目录下查找以大写字母开头的文件或目录
    -iname: 不区分大小写

    # find ./ -size [+|-]大小及单位
    +2M: 在当前目录下查找大于2M的文件或目录。M必须大写
    -50k: 在当前目录下查找小于50k的文件或目录。k必须小写
    默认: 如果不指定单位，默认是硬盘扇区的大小

    # find ./ -size +20k [-ao] -size -50k -exec ls -lh {} \;
    -a = and: 查找当前目录下大于20k并且小于50k的目录或文件
    -o = or: 查找当前目录下大于20k或者小于50k的目录或文件
    -exec 命令 {} \;: 固定格式，对搜索的结果执行操作

    # find ./ -perm 0777: 查找当前目录下权限为777的文件或目录

    # find ./ -inum 262322: 根据文件inode查找

    # find ./ [-user|-nouser]
    -user root: 搜索当前目录文件所有者为root的文件或目录
    -nouser: 表示没有所有者的文件。
        1. 可能是内核产生的文件，会保存在/sys或/proc目录下
        2. 可能是外来文件，例如从Windows拷贝的文件，因为Windows没有所有者的概念
        除了以上两种情况，没有所有者的文件是垃圾文件，需要手动删除

    # find ./ [-mtime|-atime|-ctime] [+|-]数量
    -atime: 文件访问时间
    -ctime: 修改文件属性的时间
    -mtime: 修改文件内容的时间
    +10: 10天内修改的文件
    10: 第10天修改的文件
    -10: 10天前修改的文件
    也可以按照分钟来查找

- - -
### sed（Stream Editor）

对内容批量替换

    # sed -i 's/^Str/String/' replace.java: 表示把以Str开头的字符串替换成String
    -i: 替换的内容会写入到文件中
    s: 表示操作的内容是字符串

    # sed -i 's/\.$\;/' replace.java: 把以.结尾替换成以;结尾

    # sed -i 's/Jack/me/g' replace.java: 把句子中的Jack全局替换成me
    g: 表示全局替换，没有g只替换第一个

    # sed -i '/^ *$/d' replace.java: 删除空行
    ^ *$: 表示空行
    d: 表示对匹配的内容进行删除

- - -
### awk

处理表格类型的数据和统计

    # awk '{print $1,$4}' netstat.txt: 打印表格第一列和第四列数据

    # awk '($1=="tcp" && $2==1) || NR==1{print $0}' netstat.txt: 打印第一列等于tcp并且第二列等于1的所有列
    NR==1: 表示打印表头

    # awk -F "," '{print $2}' split.txt: 按逗号分割并打印第二列

    # awk '{array[$1]++}END{for(i in array) print i "\t" array[i]}': 统计每一列出现的次数

- - -
### 打包与压缩

tar与gzip、tar与bzip2

    # tar -zcvf target.tar.gz source: 打包文件或目录并压缩成.gz文件。多个源文件使用空格分开
    # tar -zxvf target.tar.gz [-C path]: 解压缩.gz文件并解包
    -C path: 指定解包后的文件路径，参数必须放在目标文件后

    # tar -jcvf target.tar.bz2 source: 打包文件或目录并压缩成.bz2文件。多个源文件使用空格分开
    # tar -jxvf target.tar.bz2: 解压缩.bz2文件并解包

#### 打包与解包

tar

    # tar [-cvfxt] target source
    -c: 打包文件
    -v: 显示过程
    -f: 指定打包后的文件名
    -x: 解包
    -t: 查看包中的内容

#### 压缩与解压缩

常用的压缩文件格式有zip、bzip2、gzip等。

    # zip [-r] newfile.zip source: 自动生成.zip结尾的压缩文件
    -r: 压缩目录
    # unzip target.zip: 解压缩.zip文件

    # bzip2 [-kd] target: 压缩文件，生成.bz2结尾的压缩文件，不保留源文件
    -k: 保留源文件
    -d: 解压缩文件
    # bunzip2 [-k] target.bz2: 解压缩bz2文件
    -k: 保留压缩文件
    * bzip2不能压缩目录

    # gzip [-crd] target: 压缩文件并生成一个.gz结尾的文件，不保留源文件
    -c: 把压缩结果输出到标准控制台，不会影响源文件。 gzip -c source > target.gz
    -r: 压缩目录下的所有子文件，不能压缩目录
    -d: 解压缩文件
    # gunzip [-r] target.gz: 解压缩文件
    -r: 解压缩目录下的所有压缩文件

- - -
## 用户与组

### id

    # id -u: 查看用户ID。0为管理员
- - -
### whoami - who am i

    # whoami: 查看当前用户
    # who am i: 查看当前用户完整信息

- - -
### who

    # who: 查看当前登录的终端
- - -
### last - lastlog

    # last: 查看用户登录的信息记录，默认读取/var/log/wtmp文件
    # lastlog:  查看所有用户最后一次登录的时间，默认读取/var/log/lastlog文件

- - -
### w

查看当前登录的用户信息

    # w
    USER: 登录的用户名
    TTY: 登录终端
    FROM: 登录的IP地址
    LOGIN@: 登录时间
    IDLE: 用户闲置时间
    JCPU: 该终端连接的所有进程占用的时间
    PCPU: 当前进程所占用的时间
    WHAT: 当前正在运行的命令

- - -
### su

切换用户

    # su -: 切换到root用户并指向/root目录
    # su - user: 切换到指定用户并指向该用户的家目录

- - -
### logout

    # logout: 注销用户
- - -
### exit

    # exit: 退出控制台

- - -
### 用户

    # useradd [-d home_dir] user [-g group_name] -m [-s shell]
    -d home_dir: 指定该用户的根目录，默认为/home/user
    -g group_name: 指定用户所属组，不指定组名与用户名相同
    -m: 创建用户根目录 
    -s /sbin/nologin: 表示用户没有登录权限

    # userdel -r user: 删除用户同时删除用户根目录

    # passwd user: 修改用户密码

    # cat /etc/passwd: 查看系统中的所有用户

    # usermod -g group_name user: 修改用户所在组
- - -
### 工作组

    # groupadd group_name: 创建工作组(root用户)

    # groupdel group_name: 删除工作组

    # gpasswd [-ad] user group_name
    -a: 添加用户到组
    -d: 从组删除用户
- - -

## 文件权限

drwxrw-r--. 5 mac root 4096  May  6 08:43  http

    首字母d表示文件的类型
    d: 目录文件
    -: 普通文件
    c: 硬件字符设备
    b: 硬件块设备
    s: 管道文件
    l: 符号连接文件

    rwxrw-r--: 代表三组权限
    rwx: 表示文件所有者有rwx权限
    rw-: 表示文件所属用户组内成员有rw权限
    r--: 表示其他用户有r权限

    5: 文件的引用计数，表示硬连接的数量

    mac: 文件所有者
    root: 文件所属用户组（文件所有者和文件所属用户组没有关联）

    4096: 文件大小

    May 6 08:43: 文件最后一次修改时间

    http: 文件名

- - -

### chmod

修改文件权限。常用权限为777、755、644

    # chmod [-R] [421][421][421] file|dir
    -R: 递归修改权限
    r: 4
    w: 2
    x: 1

    # chmod [ugoa] [+-=] [rwx] file|dir
    u: 表示文件所有者
    g: 表示同组用户
    o: 表示其他用户
    a: 表示所有（u+g+o)
    +: 表示追加权限
    -: 表示删除权限
    =: 表示赋值权限（覆盖旧权限）

    # chmod 765 file = chmod u+rwx,g=rw,o=rx file

- - -
### chown

修改文件所有者和所属组

    # chown user[:group] file

### chgrp

修改文件所属组

    # chgrp group file

    

#### 权限对文件的作用，要慎用x权限

    r: 读取文件内容（cat、more、head、tail）
    w: 新增、编辑和修改文件内容（不包括删除文件）。对一个文件的上级目录有w权限，才可以删除该文件。
    x: 可执行

#### 权限对目录的作用，慎用w权限

    r: 可以查询目录（ls）。如果只对目录赋予只读权限没有意义，最低要赋予rx权限
    w: 修改目录结构。如新建、删除、重命名、剪切文件或目录（touch、rm、mv、cp）等。写权限表示修改文件的内容，目录中的内容就相当于子文件。
    x: 可以进入目录（cd）

### 默认权限

    # umask: 查询文件默认权限，第一位表示特殊权限
    # umask 0002: 临时修改权限默认值
    # /etc/profile: 在配置文件中永久修改权限默认值

文件默认权限

    文件默认最大权限为666，umask的默认值为022，把两个权限换算成字母再相减等到文件的默认权限为644
        rw- rw- rw- 
    -   --- -w- -w-
    --------------------
        rw- r-- r--

目录默认权限

    目录默认最大权限为777，umask的默认值为022，把两个权限换算成字母再相减等到目录的默认权限为755
        rwx rwx rwx
    -   --- -w- -w-
    --------------------
        rwx r-x r-x

- - - 
## 网络相关

### ifconfig

    查看网络状态

    # ifconfig eth0 192.168.1.100
    netmask 255.255.255.0: 临时设置网卡IP地址和子网掩码
- - - 
### ifup 

    # ifup 网卡设别名: 启用网卡
### ifdown 

    # ifdown 网卡设备名: 禁用网卡
- - - 
### netstat 

    # netstat [-tunla][-rn]
    -t: 列出TCP协议端口
    -u: 列出UDP协议端口
    -n: 不使用域名和服务名，而使用IP和端口号
    -l: 仅列出监听状态的网络服务
    -a: 列出所有网络连接
    -rn = route -n: 显示路由信息
- - -
### nslookup

查询DNS、解析IP或域名

    # nslookup
    输入server，查询本地DNS，输入exit退出
    输入域名查询指定域名DNS解析结果

- - -
### traceroute

跟踪路由信息

    # traceroute 域名|IP
- - -
### wget

根据链接下载软件包

    # wget URL

- - -
### tcpdump

抓包命令

    # tcpdump -i eth0 -nnX port 21
    -i: 指定网卡接口
    -nn: 将数据包中的域名转成IP和端口
    -X: 以十六进制和ASCII码显示数据包内容
    port: 监听端口

- - -
### ssh

连接远程服务器

    # ssh user@host
- - -
### scp

上传或下载文件到远程服务器

    # scp [-r] user@host:remote_file local_path
    从远程服务器下载文件到本地
    
    # scp [-r] local_file user@host:remote_path
    上传本地文件到远程服务器

    -r: 操作目录

- - -

### 网络配置

#### 网卡配置

/etc/sysconfig/network-scripts/ifcfg-eth0

    DEVICE=eth0 -> 网卡设备名

    BOOTPROTO=none -> 是否自动获取IP(none、static、dhcp)

    HWADDR=00:0c:29:17:c4:09 -> MAC地址

    NM_CONTROLLED=yes -> 是否可以由Network Manager图形管理工具托管

    ONBOOT=yes -> 是否随网络服务启动

    TYPE=Ethernet -> 网络类型为以太网

    UUID="44b76c8a-b59f-445d-83fa-7f98fda86b3d" -> 唯一识别码
    如果UUID冲突，删除网卡信息文件中的MAC地址行，然后删除/etc/udev/rules.d/70-persistent-net.rules网卡和MAC地址绑定文件

    IPADDR=192.168.1.100 -> IP地址

    NETMASK=255.255.255.0 -> 子网掩码

    GATEWAY=192.168.1.1 -> 网关地址

    DNS1=202.106.0.20 -> DNS地址

    IPV6INIT=no -> IPv6没有启用

    USERCTL=no -> 不允许非root用户控制此网卡

#### 主机名配置

/etc/sysconfig/network

    # hostname: 查看和配置临时主机名

#### DNS配置

/etc/resolv.conf

















