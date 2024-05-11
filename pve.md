# PVE

## 安装 pvetools

```shell
# 强烈建议先删除企业源：
rm /etc/apt/sources.list.d/pve-enterprise.list

export LC_ALL=en_US.UTF-8
apt update && apt -y install git && git clone https://github.com/ivanhao/pvetools.git
cd pvetools
./pvetools.sh
```

## 修改CT模板源

```shell
cp /usr/share/perl5/PVE/APLInfo.pm /usr/share/perl5/PVE/APLInfo.pm.bak
sed -i 's|http://download.proxmox.com|https://mirrors.tuna.tsinghua.edu.cn/proxmox|g' /usr/share/perl5/PVE/APLInfo.pm
systemctl restart pvedaemon.service
```

## 通过SSH连接到lxc容器

> 打开 /etc/ssh/sshd_config ，并将PermitRootLogin更改为yes。

```shell
# Authentication:
LoginGraceTime 120
PermitRootLogin yes
StrictModes yes
```

## 调整lxc磁盘大小

```shell
lvs
lvdisplay

# 运行e2fsck 检查lxc的磁盘
e2fsck -fy /dev/local-lvm/vm-102-disk-0

# 运行resize2fs 调整lxc磁盘空间
resize2fs /dev/local-lvm/vm-102-disk-0 10G

# 运行lvreduce 缩小磁盘空间
lvreduce -L 10G /dev/local-lvm/vm-102-disk-0

# 修改LXC的配置文件
nano /etc/pve/lxc/102.conf
# rootfs: local-lvm:vm-102-disk-0,size=20G   =>
# rootfs: local-lvm:vm-102-disk-0,size=10G

```

## IP 地址

```shell
sudo dhclient -r    # 清除IP
sudo dhclient       # 重新获取IP
```

## 无法关机

## 修改 LXC 容器密码

```
pct enter ID
```

## 挂载 smb/cifs

```shell
pvesm add cifs nas100 --server 10.8.201.31 --share your_nas_storage_dir --username your_username --password your_password --smbversion 2.0
```

pvesm add cifs smb-cat --server 192.168.91.9 --share pve --username nasadmin --password Smtl@2008 --smbversion 2.0

pvesm add cifs smb-ikuai --server 192.168.91.1 --share pve --username client01 --password Client@01 --smbversion 2.0

## lxc 的 docker,外网可以访问

iptables -P FORWARD ACCEPT

## ssh 访问 lxc

在容器内，打开/ etc / ssh / sshd_config并将PermitRootLogin更改为yes。

```shell
# Authentication:
LoginGraceTime 120
PermitRootLogin yes
StrictModes yes
```
