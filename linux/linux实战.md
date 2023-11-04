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










