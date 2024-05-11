# Ubuntu

## 修改时区

```shell
timedatectl list-timezones |grep Shanghai    #查找中国时区的完整名称
```

> Asia/Shanghai

```shell
timedatectl set-timezone Asia/Shanghai    #其他时区以此类推
```

## 更换源

```shell
sudo cp /etc/apt/sources.list /etc/apt/sources.list.backup #backup
sudo sed -i "s/archive.ubuntu.com/mirrors.aliyun.com/g" /etc/apt/sources.list #更换阿里云源
```

## 挂载远程文件

```shell
apt install cifs-utils -y #安装组件
mkdir /mnt/nas_share #建立挂载目录
nano ~/.smbcredentials #创建密码文件
```

> username=smb_share
>
> password=share_password

```shell
nano /etc/fstab
```
> //$smb_server/share /mnt/nas_share cifs credentials=/root/.smbcredentials,iocharset=utf8 0 0
>
> //192.168.91.1/pcdn /mnt/nas_share cifs vers=2.0,credentials=/root/.smbcredentials,iocharset=utf8 0 0