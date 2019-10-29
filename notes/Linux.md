# 常用命令

## 文件相关
### ln（Link）链接文件

源文件与链接文件会相互影响，无论修改哪一个，都会同步到另一个。

    # ln [-s] source_filename dist_filename
    无参数：创建一个硬链接文件
    -s：创建一个符号链接文件

#### 硬链接：
- 拥有相同的inode和存储block，文件大小、内容与目标文件相同，可以看作是一个文件
- 不能针对目录使用
- 删除源文件，不会影响硬链接文件

#### 符号链接：
- 与Windows中的快捷方式完全一样
- 拥有自己的indoe和存储block，但是block中只保存目标文件的文件名和inode，没有实际数据
- 软链接的文件权限都为777
- 删除源文件软链接文件失效
        
#### inode

分区表中的inode号，相当于文件ID

#### 存储block

文件在硬盘中实际的存储位置。硬盘分区后是由排列的存储块所组成，一般每个存储块的大小是4KB。一个大于4KB的文件由多个存储块存储，存储块位置不是连续的。

用户查找文件的流程是先去查看分区表，通过分区表中的inode找到该文件所对应的存储块，然后再取出存储块中的数据返回给用户。

### ls

查询目录中的文件

    # ls [-aldhi] file|dir
    -a：显示所有文件，包括隐藏文件
    -l：显示详细信息
    -d：查看目录属性
    -h：人性化显示文件大小
    -i：显示文件inode

### mkdir

创建目录

    # mkdir [-p] dir_name
    -p：递归创建目录

### rmdir（Remove empty Directory)

删除空目录

### rm

删除文件或目录

    rm [-rif] file|dir
    -r：递归删除目录
    -i：交互式操作，删除前询问是否删除
    -f：忽略不存在的文件和参数

### cd（Change Directory）

切换目录

    # cd ~：切换到家目录
    # cd -：进入上次目录

### touch

创建文件

### pwd（Print Working Directory）

查看当前所在路径

### cp

拷贝文件

    # cp [-adprfi] source destination
    -a：相当于 -pdr
    -d：若源文件是链接文件，则复制链接属性
    -p：连同文件属性一起复制
    -r：递归复制（用于目录）
    -f：覆盖已经存在的目标文件，不会询问
    -i：交互式操作，询问用户是否覆盖已经存在的目标文件

### mv

剪切或重命名文件、目录

    # mv [-if] source destination
    -i：交互式操作，询问用户是否覆盖已经存在的目标文件
    -f：覆盖已经存在的目标文件，不会询问

### cat 

查看文件内容

    # cat /etc/centos-release：查看系统发行版本
    # cat /proc/meminfo：查看内存大小

### more 

分页显示文件内容

    # more file
    空格：向下翻页
    b：向上翻页
    回车：向下翻一行

### less

分页显示文件内容，与more类似

### echo


    # echo -e：输出转义字符
    [parallels@localhost Test]$ echo -e "\e[1;31mHello World.\e[0m"
    Hello World.

    # echo 'value'：单引号，不能识别变量和命令，都当作普通字符串来处理
    [parallels@localhost Test]$ echo 'echo ${PATH}'
    echo $PATH



|字符|说明|
|:-|-:|
|\a|输出提示音|
|\b|退格键|
|\v|垂直制表符|
|\0|以八进制格式输出|
|\x|以十六进制格式输出|
|\e|改变字体颜色，\e[1; 开启颜色，\e[0m 关闭颜色|

|颜色编号|颜色值|
|:-|-:|
|30m|黑色|
|31m|红色|
|32m|绿色|
|33m|黄色|
|34m|蓝色|
|35m|洋红|
|36m|青色|
|37m|白色|















