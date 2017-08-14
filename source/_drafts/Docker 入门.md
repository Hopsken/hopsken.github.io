## Docker 入门

#### 常用命令
1. docker run - 运行容器

2. docker images - 列出镜像

   镜像 ID 是镜像的唯一标识，一个镜像可以对应多个 TAG（标签）

   虚悬镜像：被覆盖的旧镜像，名称为<none>，`docker images -f dangling=true`来显示。使用`docker rmi $(docker images -q -f dangling=true)`来删除这些没有存在价值的虚悬镜像。

   -a：显示中间层镜像

   -f：过滤

   <name>：根据仓库名列出镜像

3. docker exec - 进入容器

   `docker exec -it <container> bash`进入 bash 环境

4. docker diff  <container> - 显示容器文件变动

5. docker commit —options <container>  <repo:tag> - 提交对容器的更改至镜像

   —author  指定修改的作者，可留空

   —message 记录本次修改，可留空

6. docker history <image:tag> - 查看镜像内的历史记录

7. docker build [options] [context] - 构建镜像

### Dockerfile
使用 Dockerfile 来在已有镜像的基础上定制镜像。
`From` 指定基础镜像
`RUN` 执行命令 - 类似 Shell，把同一目的的操作合并为一条语句，来避免产生的镜像过于臃肿。使用`&&`将各个所需命令串联起来。每一层构建的最后一定要清理掉无关文件。

### 操作容器
新建并启动
docker run
1. 打开 bash，`docker run -t -i ubuntu:14.04 bash`
2. 后台运行 -d 参数

docker start
启动已经终止的容器

docker stop
终止运行中的容器

docker ps
显示在运行的容器
-a 显示终止状态的容器

docker restart

.bashrc_docker
使用 nsenter 进入 docker
docker-enter <container>
或者使用 `docker attach`

导入导出（快照）
导出 - `docker export <container_id> > name.tar`
导入 - `cat name.tar | docker import - name/image:tag `或者`docker import URL`

删除容器
docker rm <container> - 删除终止状态容器
-f 删除运行中的容器
* 删除所有终止状态容器 `docker rm $(docker ps -a -q)`
