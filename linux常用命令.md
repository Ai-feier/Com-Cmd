防火墙命令，开启端口, 需重启防火墙：
```bash
firewall-cmd --zone=public --add-port=22/tcp --permanent
firewall-cmd --reload
```


tar 命令
```bash
# x: 解压
# c: 压缩
# z: 一种压缩格式
# vf: 显示详细信息

tar -czvf abc.gz.tar abc/ # 压缩

tar -xzvf abc.gz.tar # 解压 -C 'destination' 

# 删除解压后的文件，并删除文件夹
rm -rf abc
```

rm 命令:
> -i 删除前逐一询问确认。
>
> -f 即使原档案属性设为唯读，亦直接删除，无需逐一确认。
>
> -r 将目录及以下之档案亦逐一删除。
```bash
# 删除当前目录下的所有文件及目录，并且是直接删除，无需逐一确认命令行为：

rm  -rf  # 要删除的文件名或目录

#删除文件名 test.txt:
rm  -rf   test.txt

#删除目录 test，不管该目录下是否有子目录或文件，都直接删除:
rm  -rf   test/
```

rpm 命令:
> -i: 安装
> -vh: 多显示一些内容
>
> -e: 卸载
>
> --force: 强制
>
> --nodeps: 不检查依赖
```bash

```


配置 java:
```bash
export JAVA_HOME=java-1.8.0-openjdk-1.8.0.262.b10-1.el7.x86_64
export PATH=$PATH:$JAVA_HOME/bin
```

tree 命令：
```bash
# 显示目录结构
tree .
```

brctl 命令（网络设备相关）
```bash
brctl show
```
