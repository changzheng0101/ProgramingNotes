# man 

* 后加命令 调出帮助文档



# touch 

主要更新时间和修改次数,可创建文件



# rm

* -v 有详细输出
* -r 递归删除
* -f 强制删除
* -i 互动



## open

open(其他平台) 

xdg-open linux平台打开文件



# mv

* rename作用:mv file new_file

* 移动文件：mv file destination_folder



## cp

* cp file position
* -r recursive copy

## head tail

* 用于打印文件
* -n number 指定number-行数
* -f 持续输出

### >

* 重定向
* 会覆盖原来的内容

## >>

* 重定向
* 往原来的内容附加内容



## cat

* cat filename 输出整个文件
* 多个文件  一起输出
* -n 显示行号

# less

* less <filename> 用less打开文件 方便查看

# wc

* word count 
* wc <filename> 
* output : lines words bytes



# pipe

* 用一个命令的输出当第二个命令的输入
* 符号 -->|



# sort

* -n 按照数字顺序
* -r 逆序
* -u 多个值变成一个 unique

# uniq

* 当连续两行一样，只输出一行



# echo

* ~ 和 $ 代表特殊字符
* echo *.txt 输出当前路径下的所有txt文件
* {1..99}  1到99
* {a,b,c}.txt ==== a.txt b.txt c.txt

# diff

* 传入两个文件 比较差别
* -u 类似于github显示
* -y 

# find

* find . -name '*.js' 在当前目录下寻找名字为js的
* find . -type d 找出所有路径
* find . -type f -name '*.py' 找出所有文件 以py结尾
* find .  -size +100k -size -1M
* find .  -name '*.py' or -name '\*.js'
* find . -type f -exec cat {} \; 找出所有文件，并且执行cat {} 为占位符，用来放找到的文件，\;代表命令的结束

# grep

* 用在文件内部进行搜索
* grep ‘green’ test.txt 在test.txt中查找green
* -n  打印行号
* -C 2 打印出每个匹配的前后两行
* -i 不匹配大小写

# du

* 估计文件体积
* disk usage
* -h human readable

# df

* 用于获取磁盘信息
* -h  方便理解

# history

* ！序号 直接运行历史中某条命令

# ps

* 列出所有程序
* 和grep结合使用可以找进程



# top

* top -o %MEM 按照mem的大小来进行排序显示

# kill

* kill -l 列出可以发送的信号
* 15 温和的杀死程序方式
* 9 直接中断程序的执行
* kill -9 PID
* kill -KILL PID
* 默认是15

# killall

* 杀死所有进程
* killall -9 node 杀死所有node
* 不是精确匹配

## jobs

* 查看所有停止的进程
* 用crtl 加z 进行停止
* fg/bg 加程序id让其重新运行
  * foreground -- background



# gzip

* gzip filename 会删除原来文件
* 结尾gz
* -d 用于解压
* 或者用gunzip

# tar

* -c create
* -f 文件名称 最终合并的名字
* tar -cf result.tar file.txt file2.txt
* 只是打包 并未压缩
* -x extract 
* -C 解压的位置
* tar -xf result.tar -C test  result.tar解压到当前的test目录下
* tar -tf result.tar
* tar -xf result.tar 会解压到当前面目录

* tar -czf resultl.tar.gz file1 file2 将一堆文件打包解压
* tar -xf resultl.tar.gz



# xargs

* cat test.txt | xargs rm 将test.txt中的内容当rm的参数

# ln

* link 快捷方式

* hard link

  -- 两个指向相同的一个对象

  -- ln origin.txt hardlink.txt 创建origin的hardlink，两者指向同一个文件，删除其中一个，另一个不受影响，改变一个会同时改变两个

* soft link  -s参数

  *  连接到文件
  * 当文件删除后无法使用
  * 软连接和文件都指向相同的内存地址