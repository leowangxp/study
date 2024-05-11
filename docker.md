# Docker

## 修改国内镜像

```shell
vim /etc/docker/daemon.json
```

```json
{
    "registry-mirrors": [
        "https://dockerhub.azk8s.com",
        "https://docker.mirrors.ustc.edu.cn"
    ]
}
```

```shell
 systemctl reload docker
```

## 制作镜像时不使用缓存

```shell
docker-compose build --no-cache
```

## 进入容器内部

```shell
docker-compose exec container_name bash
```

## 删除所有容器

```shell
docker rm $(docker ps -qa)
```

## 删除所有镜像

```shell
docker rmi $(docker images -qa)

# 无法删除时，删除该目录中的文件
rm /var/lib/docker/image/devicemapper/imagedb/content/sha256/
```

## 导入导出镜像

```shell
# 导出
docker save -o images.tar image01:tag01 image02:tag02
# 批量导出
docker save -o images.tar $(docker images | grep -v REPOSITORY | grep -v '<none>' | awk 'BEGIN{OFS=":";ORS=" "}{print $1,$2}')

#导入
docker load -i images.tar
```

## 避免容器自动退出

```yml
tty: true
```

## 构建新的镜像，并用新的镜像运行容器

```shell
docker-compose up [service] --build --force-recreate
```
