配置静态 IP

```sh
sudo apt install network-manager
```

- 网关最后一位`2`,  dns为`1`(经验)

1.  /etc/netplan/00-installer-config.yaml

```yaml
network:
  version: 2
  renderer: NetworkManager
  ethernets:
    ens33:
      addresses: [192.168.1.104/24]
      dhcp4: no
      optional: true
      gateway4: 192.168.1.2
      nameservers:
        addresses: [114.114.114.114, 8.8.8.8]
  version: 2
```

2. 还需要配置 DNS

> 首先修改 /etc/systemd/resolved.conf 文件，在其中添加dns信息，例如：
>
> DNS=8.8.8.8 114.114.114.114 223.5.5.5
> 然后退出保存。
>
> 然后以root身份在ubuntu终端中依次执行如下命令：
>
> ```sh
> systemctl restart systemd-resolved
> systemctl enable systemd-resolved
> 
> mv /etc/resolv.conf /etc/resolv.conf.bak
> ln -s /run/systemd/resolve/resolv.conf /etc/
> ```
>
>
> 再查看/etc/resolv.conf文件就可以看到新的dns信息已经写入其中了。