# Docker

## 安装 docker

1. [Install Docker Engine on Debian](https://docs.docker.com/engine/install/debian/)
2. [Install Docker Engine on Ubuntu](https://docs.docker.com/engine/install/ubuntu/)
3. [开源欧拉 ( openEuler ) 下 Docker 部署与使用【华为根技术】](https://bbs.huaweicloud.com/blogs/472381)

## 修改国内镜像

```bash
# 写入镜像加速配置
sudo tee /etc/docker/daemon.json <<EOF
{
    "registry-mirrors": [
        "https://docker.xuanyuan.me",
        "https://docker.1ms.run",
        "https://docker.m.daocloud.io"
    ]
}
EOF
# 重新加载配置
sudo systemctl daemon-reload
# 重启 Docker
sudo systemctl restart docker
# 验证配置
sudo docker info | grep -E "Registry Mirrors|Cgroup Driver|Storage Driver"
```

## 制作镜像时常用参数

```bash
docker compose build --no-cache --progress plain
```

| 参数                  | 作用                             |
| --------------------- | -------------------------------- |
| `--no-cache`          | 不使用构建缓存，所有层重新构建   |
| `--progress plain`    | 显示详细构建日志，逐层输出       |
| `--pull`              | 构建前拉取最新基础镜像           |
| `--parallel`          | 并行构建多个服务镜像             |
| `--build-arg KEY=VAL` | 传入构建参数                     |
| `--no-rm`             | 构建失败时保留中间容器，方便排查 |

## 进入容器内部

```bash
docker-compose exec container_name bash
```

## 删除所有容器

```bash
docker rm $ ( docker ps -qa )
```

## 删除所有镜像

```bash
docker rmi $ ( docker images -qa )

# 无法删除时，删除该目录中的文件
rm /var/lib/docker/image/devicemapper/imagedb/content/sha256/
```

## 导入导出镜像

```bash
# 导出
docker save -o images.tar image01:tag01 image02:tag02
# 批量导出
docker save -o images.tar $(docker images | grep -v REPOSITORY | grep -v '<none>' | awk 'BEGIN{OFS=":";ORS=" "}{print $1,$2}')
# 导入
docker load -i images.tar
```

## 镜像重命名

```bash
docker tag id label:tag
```

## 避免容器自动退出

```yml
tty: true
stdin_open: true
```
