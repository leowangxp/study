#修改国内镜像

    vmi /etc/docker/daemon.json

    {
        "registry-mirrors": ["https://docker.mirrors.ustc.edu.cn"]
    }

    systemctl reload docker

