# centos

## 修改国内镜像

    vim /etc/docker/daemon.json

    {
        "registry-mirrors": ["https://docker.mirrors.ustc.edu.cn"]
    }

    systemctl reload docker

## 进入容器内部

    docker-compose exec container_name bash

## 删除所有容器

    docker rm $(docker ps -qa)

## 删除所有镜像

    docker rmi $(docker images -qa)

    无法删除时，删除该目录中的文件
    rm /var/lib/docker/image/devicemapper/imagedb/content/sha256/