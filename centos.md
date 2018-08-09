# Docker

## 同步时间

    ntpdate 0.asia.pool.ntp.org
    hwclock --systohc

## 列出已经安装的包

    yum list installed | grep docker

## 查看内核版本及位数

    uname -a

## 查看 centos 版本

    cat /etc/os-release

## 查看 CPU 内存

    top
    #top命令按1，看到几个CPU就代表是几核的。

## 修改机器名

    hostnamectl set-hostname <hostname>
