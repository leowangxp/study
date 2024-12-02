# openEuler

## 安装 docker

```shell
dnf config-manager --add-repo=https://repo.huaweicloud.com/docker-ce/linux/centos/docker-ce.repo
sed -i 's+download.docker.com+repo.huaweicloud.com/docker-ce+' /etc/yum.repos.d/docker-ce.repo
sed -i 's+$releasever+9+' /etc/yum.repos.d/docker-ce.repo
dnf makecache
dnf install docker-ce -y
systemctl enable docker
tee /etc/docker/daemon.json <<EOF
{
    "registry-mirrors": [
        "https://docker.m.daocloud.io",
        "https://dockerhub.icu"
    ]
}
EOF
systemctl daemon-reload
systemctl restart docker
```
