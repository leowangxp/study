# CentOS

## 同步时间

```shell
ntpdate 0.asia.pool.ntp.org
hwclock --systohc
```

## 列出已经安装的包

```shell
yum list installed | grep docker
```

## 查看内核版本及位数

```shell
uname -a
```

## 查看 centos 版本

```shell
cat /etc/os-release
```

## 查看 CPU 内存

```shell
top
# top命令按1，看到几个CPU就代表是几核的。
```

## 修改机器名

```shell
hostnamectl set-hostname <hostname>
```

## 移动文件和目录，包含隐藏文件

```shell
mv * .[^.]* target/
```

## 修改 DNS

1. 修改文件

    ```shell
    cd /etc/sysconfig/network-scripts/
    # 找到类似 ifcfg-eth0 的文件 vim 打开, 添加一行
    DNS1=114.114.114.114
    ```

1. 重启网络服务

    ```shell
    service network restart
    ```

1. 验证

    ```shell
    vim /etc/resov.conf
    # 就可以看到添加的dns生效了
    ```
