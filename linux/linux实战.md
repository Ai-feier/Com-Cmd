### 帮助命令:
man, help, info
```bash
man cd

help cd  # 仅内部命令
ls --help  # 外部命令

info ls
```
### 区分命令
```bash
type man
```

## 文件管理
ls:
![Alt text](assets/linux%E5%AE%9E%E6%88%98/image.png)
- -h: 显示 文件大小

cd:
```bash
cd -  # 回到上一个目录
```

mkdir
![Alt text](assets/linux%E5%AE%9E%E6%88%98/image-1.png)

rmdir, rm 删除目录
![Alt text](assets/linux%E5%AE%9E%E6%88%98/image-2.png)

cp
![Alt text](assets/linux%E5%AE%9E%E6%88%98/image-3.png)

mv
![Alt text](assets/linux%E5%AE%9E%E6%88%98/image-4.png)

rm
![Alt text](assets/linux%E5%AE%9E%E6%88%98/image-5.png)

通配符
![Alt text](assets/linux%E5%AE%9E%E6%88%98/image-6.png)

### 文本查看命令
![Alt text](assets/linux%E5%AE%9E%E6%88%98/image-7.png)
及 more, less more

### 打包压缩解压
tar
![Alt text](assets/linux%E5%AE%9E%E6%88%98/image-8.png)
```bash
tar cvf /etc.back.tar /etc
tar czvf /etc.back.tar.gz /etc
tar czvf /etc.back.tar.bz2 /etc

tar xzvf /etc.back.tar.gz -C /tmp/etc
# c 打包
# x 解包
# z gzip 压缩算法
# v 详细显示
# f 对文件
```

## 用户与权限管理
![Alt text](assets/linux%E5%AE%9E%E6%88%98/image-9.png)
- id 查看用户信息
- g 用户组

用户组
![Alt text](assets/linux%E5%AE%9E%E6%88%98/image-10.png)

![Alt text](assets/linux%E5%AE%9E%E6%88%98/image-11.png)

为用户(组)赋予权限
```bash
visudo
%group ALL=/sbin/shutdown -c
user ALL=/sbin/shutdown -c
user ALL=(ALL) NOPASSWD: ALL
# % 是否为用户组
# ALL 允许本机(localhost)和远程
# (ALL) 所有权限
```

#### /etc/passwd 配置
7 段式
```
用户名:是否密码:uid:gid:注释:起始文件地址:终端解释器
```
/etc/shadow: 用于保存密码

#### /etc/group 配置
4 段
```
组名称:是否需要密码:gid:其他组设置
```

### 文件权限
![Alt text](assets/linux%E5%AE%9E%E6%88%98/image-12.png)

文件类型
![Alt text](assets/linux%E5%AE%9E%E6%88%98/image-13.png)

修改权限
> 权限冲突以属主为主

![Alt text](assets/linux%E5%AE%9E%E6%88%98/image-14.png)
```bash
chmod 777 filea
# 改所属主/组
chown user /test
chown :group /test
```
![Alt text](assets/linux%E5%AE%9E%E6%88%98/image-15.png)


网络管理
![Alt text](assets/linux%E5%AE%9E%E6%88%98/image-16.png)
![Alt text](assets/linux%E5%AE%9E%E6%88%98/image-17.png)
![Alt text](assets/linux%E5%AE%9E%E6%88%98/image-18.png)
网卡命名
![Alt text](assets/linux%E5%AE%9E%E6%88%98/image-19.png)
![Alt text](assets/linux%E5%AE%9E%E6%88%98/image-20.png)
查看网线连接情况
![Alt text](assets/linux%E5%AE%9E%E6%88%98/image-21.png)
```bash
mii-tool eth0
```
![Alt text](assets/linux%E5%AE%9E%E6%88%98/image-22.png)
修改网络配置
![Alt text](assets/linux%E5%AE%9E%E6%88%98/image-23.png)
```bash
ifconfig eth0 101.101.20.1 netmask 255.255.255.0

# 配置乱了可以重启
ifup eth0
ifdown eth0
```
网关配置
![Alt text](assets/linux%E5%AE%9E%E6%88%98/image-24.png)
```bash
route del default gw 10.251.20.51
route add default gw 10.251.20.52

# 添加明细路由
# 要发送到 10.0.0.1 时, 会把数据包发送到 10.251.20.51, 而不是默认的网关
route add -host 10.0.0.1 gw 10.251.20.51
# 添加网段明细路由
route add -net 192.168.0.0 netmask 255.255.255.0 gw 10.251.20.53
```
ip 工具(新代centos):
![Alt text](assets/linux%E5%AE%9E%E6%88%98/image-25.png)

网络故障排除命令
![Alt text](assets/linux%E5%AE%9E%E6%88%98/image-27.png)
```bash
tarceroute -w 1 www.baidu.com
# w 等待秒数

mtr 
# 比 traceroute 跟详细

nslookup www.baidu.com
# 域名解析

telnet www.baidu.com 80
# 端口是否畅通

tcpdump -i any -n port 80
tcpdump -i any -n host 10.0.0.1
tcpdump -i any -n host 10.0.0.1 and port 80 -w /tmp/file
# 抓包工具
# -i any: 任意网卡
# -n: 以 IP 形式显示
# port 80: 端口
# host 10.0.0.1: 抓取到该 IP 的 tcp 包
# and 
# -w: 保存下来

# netstat/ss
netstat/ss -ntpl
# -n: 显示 ip 不显示域名
# -t: 以 tcp 协议显示
# -p: 端口对应的进程
# -l: tcp 的 listen 状态
```

网络服务管理
![Alt text](assets/linux%E5%AE%9E%E6%88%98/image-28.png)

网络配置文件
![Alt text](assets/linux%E5%AE%9E%E6%88%98/image-29.png)
/etc/sysconfig/network-scripts/ifcfg-*

网络管理工具(两者仅用一个)
network(Centos6)
NetworkManager(Centos7)
```bash
systemctl list-unit-files NetworkManager.service
```
关闭 network
```bach
chkconfig --list network
chkconfig --level 开启数 network off
```
NetworkManager 启动关闭
```bash
systemctl disable NetworkManager
systemctl enable NetworkManager
```

静态网卡配置
![Alt text](assets/linux%E5%AE%9E%E6%88%98/image-30.png)
```bash
# 修改网卡配置后
service network restart
systemctl restart NetworkManager.service
```
修改后查看 DNS
```bash
nslookup
    server
```

主机名
```bash
hostname  # 查看

# 临时修改主机名
hostname you.name

# 永久更改主机名
hostnamectl set-hostname you.name

# 主机名修改后必须在 /etc/hosts 追加
vim /etc/hosts
    # 文件最后: 127.0.0.1 you.name
reboot
```

## 软件安装
![Alt text](assets/linux%E5%AE%9E%E6%88%98/image-31.png)
rpm 包
![Alt text](assets/linux%E5%AE%9E%E6%88%98/image-32.png)
```bash
rpm -qa | more
rpm -q vim-common
# -q: 查询
# -a: all
# | more: 分屏显示
rpm -i vim-com...  # 安装
rpm -e vim-com...  # 卸载
```

挂载光盘
![Alt text](assets/linux%E5%AE%9E%E6%88%98/image-33.png)

yum:
![Alt text](assets/linux%E5%AE%9E%E6%88%98/image-34.png)
```bash
yum makecache

# yum 的扩展库
yum install epel-release -y
```
![Alt text](assets/linux%E5%AE%9E%E6%88%98/image-35.png)

二进制安装
![Alt text](assets/linux%E5%AE%9E%E6%88%98/image-36.png)

升级内核
```bash
uname -r  # 查看内核版本
yum install kernel-3.10.0  
yum update
```
源代码安装
![Alt text](assets/linux%E5%AE%9E%E6%88%98/image-39.png)
![Alt text](assets/linux%E5%AE%9E%E6%88%98/image-37.png)
![Alt text](assets/linux%E5%AE%9E%E6%88%98/image-38.png)
```bash
lscpu  # 查看内核个数

df -h  # 查看占用内存
```

### grub 配置文件
![Alt text](assets/linux%E5%AE%9E%E6%88%98/image-41.png)
启动默认内核
```bash
grub2-editenv list  # 查看默认启动内核
grep ^menu /boot/grub2/grub.cfg  # 查找 grub.cfg 下以 menu 开头的行

# 根据 grep 的行(按顺序)
grub2-set-default 0
```
忘记 root 密码
- reboot 选择合适内核按 e
- 找到第一个 linux16 的行(从什么地方加载系统的配置), 结尾加上 `rd.break`(`single`), 后 Ctrl-x
- 进入到内存中的虚拟根, 要重新挂载 mount -o remount,rw /sysroot
- 换根目录 chroot /sysroot
- echo 123456 | passwd --stdin root
- 还需要关闭 SELinux `/etc/selinux/config` (SELINUX=disable)

## 进程管理
![Alt text](assets/linux%E5%AE%9E%E6%88%98/image-42.png)
![Alt text](assets/linux%E5%AE%9E%E6%88%98/image-43.png)
```bash
ps -eLf 
# -e 
# -f 显示更多信息(PPID:父进程)
# -L 显示线程信息
```
pstree(ps 的树形显示)

top
![Alt text](assets/linux%E5%AE%9E%E6%88%98/image-44.png)
```bash
top -p <pid>
```
> 按`1`显示具体 cpu
>
> 按`s`更改刷新时间

### 进程的控制
![Alt text](assets/linux%E5%AE%9E%E6%88%98/image-45.png)
![Alt text](assets/linux%E5%AE%9E%E6%88%98/image-46.png)
```bash
nice -n <nice-val> ./a.sh
renice -n <new-nice> <pid>
```

### 程序作业控制
让任务后台运行
```bash
./a.sh &  # 让任务后台运行

# 让前台的任务, 在保存到后台 Ctrl-z

jobs  # 查看后台运行的任务
fg <job-number>  # 调回前台
bg <job-number>  # 调回后台运行
```
杀死进程 kill
```bash
kill -l  # 显示所有信号
kill -9 <pid>
```

守护进程
开机随 linux 启动
![Alt text](assets/linux%E5%AE%9E%E6%88%98/image-47.png)

日志 /var/log
- messages: 系统常规日志
- dmsg: 内核启动状态
- secure: 安全日志
- cron: 计划日志

### 服务管理工具
service 脚本位置: /etc/init.d/...



systenctl 脚本位置: /usr/lib/systemd/system/...
![Alt text](assets/linux%E5%AE%9E%E6%88%98/image-48.png)

更改级别
```bash
systemctl get-default 
systemctl set-default multi-user.target
```

Selinux /etc/selinux/config
![Alt text](assets/linux%E5%AE%9E%E6%88%98/image-49.png)
```bash
# 查看标签
ps -Z
ls -Z
```

### 内存磁盘管理
![Alt text](assets/linux%E5%AE%9E%E6%88%98/image-50.png)

内存查看命令
```bash
free 
# -m M显示

top```

磁盘查看命令
```bash
fdisk -l
parted -l
df -h 
du -h  # 紧凑的大小
ls -h  # 文件大小含空洞大小

dd if=/dev/zero bs=4M count=10 seek=20 of=afile
# if, of  输入,输出文件
# bs  块大小, block-size
# count  实际多少块
# seek  跳过过少块, 制造空洞文件
```

文件系统
![Alt text](assets/linux%E5%AE%9E%E6%88%98/image-51.png)



i 节点 对应文件名

ln链接
```bash
ln afile bfile  # 硬链接, i 节点相同
ln -s afile bfile  # 软链接, i 节点不同
```

facl 文件权限控制
```bash
getfacl afile
setfacl -m u:user1:r afile
# -m, x  赋予, 回收权限
# u:user1:rwx  用户
# g:group1:rwx
```


磁盘分区与挂载
![Alt text](assets/linux%E5%AE%9E%E6%88%98/image-52.png)
挂载磁盘步骤: 一块磁盘->分区->格式化->挂载
磁盘大于 2TB 是使用 parted
分区
```bash
fdis sda  # 制作分区

# 使用 mkfs 把分区做成什么类型的文件系统
# 格式化
mkfs.ext4 sda1

# 使用 mount 挂载
mount /dev/sda1 /mnt/sda1
```
以上 mount 仅为单次可用, 要修改配置文件 /etc/fstab
![Alt text](assets/linux%E5%AE%9E%E6%88%98/image-53.png)


### 用户磁盘配额
![Alt text](assets/linux%E5%AE%9E%E6%88%98/image-54.png)


交换分区
![Alt text](assets/linux%E5%AE%9E%E6%88%98/image-55.png)
```bash
# 利用硬盘分区扩展 swap 
mkswap /dev/sda1
swapoff /dev/sda1

# 以文件方式扩展分区
dd if=/dev/ziro bs=4M count=1024 of=/swapfile
mkswap /swapfile
chmod 600 /swapfile
swapon /swapfile

# 永久生效
vim /etc/fstab
# /swapfile swap swap defaults 0 0
```

磁盘高级应用
RAID
![Alt text](assets/linux%E5%AE%9E%E6%88%98/image-56.png)
```bash
# /dev/md0 是上层设备, 其余为下层, 不直接操作
mdadm -C /dev/md0 -a yes -l1 -n2 /dev/sd[b,c]1
# -l1 -l0  RAID级别
# -n2  多少分区

# 查看
mdadm -D /dev/md0

# 停掉 RAID
mdadm --stop /dev/md0
# 同时破坏其下的超级卷
dd if=/dev/zero of=/dev/sdb1 bs=1M count=1
dd if=/dev/zero of=/dev/sdc1 bs=1M count=1
```

LVM 逻辑卷
```bash
pvcreate /dev/sd[b,c,d]1
pvs  # 查看

# 卷组
vgcreate ...
vgs  # 查看

# 创建新逻辑卷
lvcreate -L 100M -n lv1 vg1

# 要使用逻辑卷, 也需要格式化, 和挂载
```

扩展逻辑卷 (root)
```bash
vgextend centos /dev/sdb1

# 查看
pvs  # 物理
vgs  # 卷组
lvs  # 逻辑卷

# 扩大逻辑卷
lvextend -L +50G /dev/centos/root
lvs
df -h
# 还要扩大文件系统
xfs_growfs /dev/centos/root
```

系统综合状态查询
![Alt text](assets/linux%E5%AE%9E%E6%88%98/image-57.png)
sar
```bash
sar -u 1 10
# cpu 每 1 秒采样一次, 总 10 次
sar -r 1 10  # 内存
sar -b 1 10  # IO
sar -d 1 10  # 每块磁盘
sar -q 1 10  # 进程的使用
```
iftop
```bash
iftop -P
```

# Shell
![Alt text](assets/linux%E5%AE%9E%E6%88%98/image-58.png)

管道与重定向

管道与管道符
![Alt text](assets/linux%E5%AE%9E%E6%88%98/image-59.png)
cat 与 ps 均为外部命令, 创建的两个进程, | 为为这两个进程创建了连接
![Alt text](assets/linux%E5%AE%9E%E6%88%98/image-60.png)

重定向符号
![Alt text](assets/linux%E5%AE%9E%E6%88%98/image-61.png)

变量
![Alt text](assets/linux%E5%AE%9E%E6%88%98/image-62.png)
![Alt text](assets/linux%E5%AE%9E%E6%88%98/image-63.png)

变量的引用
![Alt text](assets/linux%E5%AE%9E%E6%88%98/image-64.png)

变量的作用范围
![Alt text](assets/linux%E5%AE%9E%E6%88%98/image-65.png)

### 环境变量
![Alt text](assets/linux%E5%AE%9E%E6%88%98/image-66.png)
配置文件:
![Alt text](assets/linux%E5%AE%9E%E6%88%98/image-67.png)
> su - username(login shell): 
>
> 加载顺序: /etc/profile, ~/.bash_profile, ~/.bashrc, /etc/bashrc
>
> su username(no login shell):
>
> 加载顺序: ~/.bashrc, /etc/bashrc



```bash
$$  # 当前进程 PID
$0  # 当前进程名称
$?  # 上一个命令的错误数
${num}  # 参数
${2-_}  # 第二个参数为空, 替换为 _
```

数组
![Alt text](assets/linux%E5%AE%9E%E6%88%98/image-68.png)

特殊字符
![Alt text](assets/linux%E5%AE%9E%E6%88%98/image-69.png)
引用符
![Alt text](assets/linux%E5%AE%9E%E6%88%98/image-70.png)
双引号: 不完全引用, 可以有 $
单引号: 完全引用
反引号: 可以接命令

测试与判断
测试命令
![Alt text](assets/linux%E5%AE%9E%E6%88%98/image-76.png)

if 
![Alt text](assets/linux%E5%AE%9E%E6%88%98/image-77.png)

case
![Alt text](assets/linux%E5%AE%9E%E6%88%98/image-78.png)
![Alt text](assets/linux%E5%AE%9E%E6%88%98/image-79.png)
循环
![Alt text](assets/linux%E5%AE%9E%E6%88%98/image-80.png)
for
![Alt text](assets/linux%E5%AE%9E%E6%88%98/image-81.png)
批量改名
![Alt text](assets/linux%E5%AE%9E%E6%88%98/image-82.png)
C 语言风格
![Alt text](assets/linux%E5%AE%9E%E6%88%98/image-83.png)

while
![Alt text](assets/linux%E5%AE%9E%E6%88%98/image-84.png)
> until 循环与 while 相反, 条件为 false 执行

案例: 判断并执行文件
![Alt text](assets/linux%E5%AE%9E%E6%88%98/image-85.png)

命令行参数
![Alt text](assets/linux%E5%AE%9E%E6%88%98/image-86.png)

函数
自定义函数
![Alt text](assets/linux%E5%AE%9E%E6%88%98/image-87.png)
![Alt text](assets/linux%E5%AE%9E%E6%88%98/image-88.png)
> [ -d "/proc"/$i" ] && return 0
> 
> if 的简单写法([ ] &&:then ) proc 下的文件夹及对应一个进程

系统函数库
![Alt text](assets/linux%E5%AE%9E%E6%88%98/image-89.png)

### 特殊符号
![Alt text](assets/linux%E5%AE%9E%E6%88%98/image-71.png)
![Alt text](assets/linux%E5%AE%9E%E6%88%98/image-72.png)
![Alt text](assets/linux%E5%AE%9E%E6%88%98/image-73.png)
![Alt text](assets/linux%E5%AE%9E%E6%88%98/image-74.png)
![Alt text](assets/linux%E5%AE%9E%E6%88%98/image-75.png)
```bash
(( 5 > 4 && 6 > 5 ))
```

脚本控制优先级
![Alt text](assets/linux%E5%AE%9E%E6%88%98/image-90.png)

fork 炸弹
```bash
func() { func | func& } ; func
# 简写
.(){.|.&};.

# root 用户不受限制, 普通用户受到影响, 通过以下命令查看最大可创建进程数
ulimit -a
```

捕获信号
![Alt text](assets/linux%E5%AE%9E%E6%88%98/image-91.png)
![Alt text](assets/linux%E5%AE%9E%E6%88%98/image-92.png)

计划任务
![Alt text](assets/linux%E5%AE%9E%E6%88%98/image-93.png)

一次性计划任务
运行时没有终端, 如需外部命令, 需要 source 导入, 没有输入(用 > )
```bash
at <data-time>
cmd
<EOF>  # 结束

atq  # 查询任务
```

周期性计划任务
位置: /var/spool/cron/
![Alt text](assets/linux%E5%AE%9E%E6%88%98/image-94.png)
![Alt text](assets/linux%E5%AE%9E%E6%88%98/image-95.png)

延时计划任务
/etc/cron.d/0hourly
/etc/anacrontab
![Alt text](assets/linux%E5%AE%9E%E6%88%98/image-96.png)

为脚本加锁
```bash
flock -xn "/tmp/f.lock" -c "/a.sh"
```

正则表达式与文本搜索
元字符
![Alt text](assets/linux%E5%AE%9E%E6%88%98/image-97.png)
> 注意: shell 的通配符与正则表达式的区别
> 
> 使用 `\` 时, 需要使用 "", 没有会被 shell 解释器解释, 达不到正则效果

find
```bash
find *txt -exec rm -v {}\;
# => rm -vf {*txt}
# -exec  不带交互, 相反  -ok
```

cut 
```bash
cut -d ":" -f7 /etc/passwd | sort | uniq -c | sort -r
```

行编辑器 sed, awk
sed: 一般用于文本替换
awk: 一般用于文本内容统计, 可替换 cut

### sed
![Alt text](assets/linux%E5%AE%9E%E6%88%98/image-98.png)
sed 替换命令
![Alt text](assets/linux%E5%AE%9E%E6%88%98/image-99.png)
![Alt text](assets/linux%E5%AE%9E%E6%88%98/image-100.png)
标志位
![Alt text](assets/linux%E5%AE%9E%E6%88%98/image-101.png)
寻址
![Alt text](assets/linux%E5%AE%9E%E6%88%98/image-102.png)
分组
![Alt text](assets/linux%E5%AE%9E%E6%88%98/image-103.png)

sed 脚本
```bash
sed -f sedscript filename
```

删除( d 会删除一整行)
![Alt text](assets/linux%E5%AE%9E%E6%88%98/image-104.png)
追加, 插入, 更改
![Alt text](assets/linux%E5%AE%9E%E6%88%98/image-105.png)
读写文件
![Alt text](assets/linux%E5%AE%9E%E6%88%98/image-106.png)
下一行
![Alt text](assets/linux%E5%AE%9E%E6%88%98/image-107.png)
![Alt text](assets/linux%E5%AE%9E%E6%88%98/image-108.png)
多行模式
![Alt text](assets/linux%E5%AE%9E%E6%88%98/image-109.png)
保持空间
![Alt text](assets/linux%E5%AE%9E%E6%88%98/image-110.png)


awk
![Alt text](assets/linux%E5%AE%9E%E6%88%98/image-111.png)
控制流程
![Alt text](assets/linux%E5%AE%9E%E6%88%98/image-112.png)
![Alt text](assets/linux%E5%AE%9E%E6%88%98/image-113.png)
字段引用
![Alt text](assets/linux%E5%AE%9E%E6%88%98/image-114.png)
表达式
![Alt text](assets/linux%E5%AE%9E%E6%88%98/image-115.png)
![Alt text](assets/linux%E5%AE%9E%E6%88%98/image-116.png)
awk 的系统变量
![Alt text](assets/linux%E5%AE%9E%E6%88%98/image-117.png)


# 服务管理
## 防火墙
![Alt text](assets/linux%E5%AE%9E%E6%88%98/image-118.png)
防火墙分类
![Alt text](assets/linux%E5%AE%9E%E6%88%98/image-119.png)
iptables 表和链:
![Alt text](assets/linux%E5%AE%9E%E6%88%98/image-120.png)

基本使用
![Alt text](assets/linux%E5%AE%9E%E6%88%98/image-121.png)
```bash
# 查看规则链
iptables -t filter -L
iptables -t filter -nL
iptables -t filter -nvL
iptables -nvL
iptables -t nat -nvL  # nat 表

# 添加一个 ip 能发送数据包到本机
iptables -t filter -A INPUT -s 10.0.0.1 -j ACCEPT
iptables -t filter -A INPUT -s 10.0.0.0/24 -j ACCEPT
```
iptable 过滤规则使用
    ip 匹配以匹配到的第一条为准
    - 全部允许, 阻止一部分 ip
    - 全部阻止, 允许一部分 ip
```bash
# 修改 ip 规则链默认配置
iptables -P INPUT DROP

# 清空规则链, 不会修改规则链默认配置
iptables -F

# 可一个 -D 序号/完整规则名/正则 删除
# -i  进入的网络接口
# -o  出去的网络接口
# -p  可指定协议
# --dport  指定端口
```

nat 表使用
![Alt text](assets/linux%E5%AE%9E%E6%88%98/image-122.png)
```bash
# 目的地址转换
# 用户把数据包发送给我, 当前主机把数据包转给一个 ip
iptables -t nat -A PREROUTING eth0 -d 114.115.141.131 -p tcp --dport 80 -j DNAT --to-destination 10.0.0.1

# 源地址转换
# 把一个内网地址伪造成 iptables 主机的地址
iptables -t nat -A POSTROUTING -s 10.0.0.0/24 -o eth1 -j SNAT --to-source 111.122.122.131

service iptables stop
```
iptables 配置文件 ( /etc/sysconfig/iptables )
![Alt text](assets/linux%E5%AE%9E%E6%88%98/image-123.png)


### firewalld
firewalld 与 iptables 仅一个
![Alt text](assets/linux%E5%AE%9E%E6%88%98/image-124.png)
```bash
firewall-cmd state
firewall-cmd --list-all
firewall-cmd --zone=public --list-interfaces
firewall-cmd --list-interfaces
firewall-cmd --list-services
firewall-cmd --get-zone
firewall-cmd --get-default-zone
firewall-cmd --get-active-zone

# 添加
firewall-cmd --add-service=https
firewall-cmd --add-port=81/tcp  # 临时
# 要永久添加, 要使用 reload
firewall-cmd --add-port=82/tcp --permanent
firewall-cmd --reload
firewall-cmd --list-all

# 移除
firewalld --remove-source=10.0.0.1
```

### ssh 服务
talnet: 明文传输
```bash
yun install telnet telnet-server xinetd -y
systemctl start xinetd.service
systemctl start talnet.service

# 查看服务端口
grep telnet /etc/services

# iptables 打开方式
iptables -I INPUT -p tcp -dport 23 -j ACCEPT
iptables -vnL | grep 23
# firewalld
firewall-cmd --premanent --add-port=23/tcp
firewall-cmd --reload
firewall-cmd --list-all

# 验证 talnet 明文传输
tcpdump -i any port 23 -s 1500 -w /tmp/a.dump  # -s 1500: 1500 字节
talnet localhost
# 抓包图形工具 wireshark
yum install wireshark-gnome
```

ssh 配置文件:
服务端 /etc/ssh/sshd_config
客服端 /etc/ssh/sshd_config
![Alt text](assets/linux%E5%AE%9E%E6%88%98/image-125.png)
```bash
# 查看端口监听
netstat -ntpl | grep 22

who
whoami
```

ssh 秘钥认证
只能是客户端产生
```bash
# 生成
ssh-keygen -t rsa

# 把公钥拷贝到目的主机
ssh-copy-id -i /root/.ssh/id_rsa.pub root@10.23.124.2
```

ssh 远程拷贝 scp (隧道功能)
```bash
# 把本地文件拷贝到远程
scp /tmp/a.txt root@12.023.132.1:/tmp/b.txt

# 把远程拷贝到本地
scp root@12.023.132.1:/tmp/b.txt /tmp/c.txt
```

FTP 服务: 文件传输协议
命令链路: 21 端口
数据链路: 主动模式和被动模式

vsftpd 服务
![Alt text](assets/linux%E5%AE%9E%E6%88%98/image-126.png)
```bash
ftp localhost
# 登录, 如果使用匿名登录, 回进到 /var/ftp, 该目录是共享的
# 如使用已存在的用户名, 则来到用户的家目录
```
vsftpd 配置文件
![Alt text](assets/linux%E5%AE%9E%E6%88%98/image-127.png)
```bash
# 注意 selinux 保护
getsebool -a | grep ftpd

# 开启  -P(永久生效)
setsebool -P ftpd_use_nfs 1

firewall-cmd --permanent --add-service=ftp
firewall-cmd --reload  # 永久添加要 reload, 临时不用

# !cmd 执行本地命令

put file
get file

man 5 vsftpd.conf  # 第 5 章是配置文件的帮助
```

虚拟用户
![Alt text](assets/linux%E5%AE%9E%E6%88%98/image-128.png)
```bash
# 该虚拟用户只用于做映射, 所以指定终端: /sbin/nologin
useradd vuser -d /data/ftp -s /sbin/nologin
# -d  指定用户家目录
# -s  指定终端

# 写虚拟用户名密码, u1\n123456\nu2....
vim /etc/vsftpd/vuser/temp  
# 转换为一个 db
db_load -T -t hash -f /etc/vsftpd/vuser.temp /etc/vsftpd/vuser.db
chmod 600 /etc/vsftpd/vuser.db
# 配置可插拔...
# 添加 auth, accout 两行
vim /etc/pam.d/vsftpd.vuser
# 修改 vsftpd 配置, 打开虚拟用户
vim /etc/vsftpd/vstpd.conf  
# 项: guest_enable=yes, guest_username, 新的 pam 服务

mkdir -p /etc/vsftpd/vuserconfig
vim u1  # 一个虚拟用户对应一个文件
```
u1:
![Alt text](assets/linux%E5%AE%9E%E6%88%98/image-129.png)

samba, nfs
![Alt text](assets/linux%E5%AE%9E%E6%88%98/image-130.png)

samba
/etc/samba/smb.conf
![Alt text](assets/linux%E5%AE%9E%E6%88%98/image-131.png)
![Alt text](assets/linux%E5%AE%9E%E6%88%98/image-132.png)
![Alt text](assets/linux%E5%AE%9E%E6%88%98/image-133.png)
```bash
useradd user1
smbpasswd -a user1  # 添加 smb 用户
subpasswd -x user1  # 删除 smb 用户
pdbedit -L  # 查看所用用户

# linux 挂载
mount -t cifs -o username=user1 //127.0.0.1/user1 /mnt
# -t cifs  指定协议, 可以为 auto, 可以省略
mount | tail 1
umount /mnt

# 挂载配置文件中的其他项
mount -t cifs -o username=user1 //127.0.0.1/share /mnt
```

NFS 服务的配置与启动
![Alt text](assets/linux%E5%AE%9E%E6%88%98/image-134.png)
![Alt text](assets/linux%E5%AE%9E%E6%88%98/image-135.png)
```bash
# 查看
showmount -e localhost

mount -t nfs localhost:/data/share /mnt
```

selinux 故障
- 通过 grub 进入单用户模式(`rb.break`), 后执行`genhomedircon`, 重新根据家目录权限产生 selinux 标签
- 也可用`touch /.autorelabel`, selinux 会重新打标签


## Nginx
OpenResty
配置文件: /usr/local/openresty/nginx/conf/nginx.conf
```bash
yum-config-manager --add-repo https://openresty.org/package/centos/openresty.repo
yum install openresty

# openresty 没有写 systemd 服务脚本
service openresty start
```

基于域名的虚拟主机
![Alt text](assets/linux%E5%AE%9E%E6%88%98/image-136.png)


LNMP

DNS
正向解析: 主机名 -> IP 
反向解析: IP -> 主机名
![Alt text](assets/linux%E5%AE%9E%E6%88%98/image-137.png)
bind: /etc/named.conf
```bash
yum install bind bind-utils -y
systemctl start named.service

# 缓存域名服务器
named-checkconf
```

NAS
多块 raid 
![Alt text](assets/linux%E5%AE%9E%E6%88%98/image-139.png)
![Alt text](assets/linux%E5%AE%9E%E6%88%98/image-140.png)
![Alt text](assets/linux%E5%AE%9E%E6%88%98/image-141.png)
![Alt text](assets/linux%E5%AE%9E%E6%88%98/image-142.png)
vsftpd 服务
![Alt text](assets/linux%E5%AE%9E%E6%88%98/image-143.png)
修改 nfs 配置
统一脚本
![Alt text](assets/linux%E5%AE%9E%E6%88%98/image-145.png)
![Alt text](assets/linux%E5%AE%9E%E6%88%98/image-144.png)

