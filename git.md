# Git

## 用仓库的内容覆盖本地

```shell
git fetch --all
git reset --hard origin/master
```

## 同步 fork 项目原仓库的更新

1. 验证远程分支可以 fetch 或 push

    ```shell
    git remote -v
    ```

1. 指明我们需要同步的仓库

    ```shell
    git remote add upstream https://github.com/OriginalRepo/OriginalProject.git
    ```

1. 验证

    ```shell
    git remote -v
    ```

1. 拉取更新的 branches 和 commits

    ```shell
    git fetch upstream
    ```

1. Checkout 本地分支

    ```shell
    git checkout master
    ```

1. 合并

    ```shell
    git merge upstream/master
    ```

1. 提交

    ```shell
    git push origin master
    ```

## cookiecutter 拉取特定 commit

```shell
cookiecutter https://github.com/tiangolo/full-stack-fastapi-postgresql --checkout 30c722339b4fa6d4c2bd3deb7cca6fc3d9568f83
```

## git Bash 中设置 git 全局设置

```shell
git config --global user.name 用户名
git config --global user.email 邮箱
```

## 设置让 VSCode 记住 Git 账号和密码

```shell
git config --global credential.helper store
```

## 忽略文件权限

```shell
git config core.filemode false
```
