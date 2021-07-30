---
layout: "post"
title: "docker&virtualization"
date: "2017-01-18 11:21"
categories: technique
tags: [docker, tool]
keywords: docker
toc:
---

### 设置docker加速器
1. Docker版本为1.12或更高
创建或编辑/etc/docker/daemon.json, 修改成如下形式：
```json
{
    "registry-mirrors": [
        "加速地址"
    ],
    "insecure-registries": []
}

```

<!-- more -->

2. Docker版本在1.8或1.11
您可以找到 Docker 配置文件（一般为/etc/default/docker），不同的 Linux 发行版的配置路径不同，具体路径请参考 Docker官方文档，
在配置文件中的 DOCKER_OPTS 加入以下内容：
```json
--registry-mirror=加速地址
```

**最后都重启docker服务**
`service docker restart`


### docker commands
1. docker images  
    列出所有的镜像文件

2. docker pull  [repository][:tag]  
    拉取镜像

    docker search [image_name]  
    搜索官网的镜像

    docker tag local-image:tagname new-repo:tagname
    docker push new-repo:tagname
    上传镜像

3. docker rm [container_id/contaner_name]    
    删除容器
   
   docker rm  \`docker ps -aq\`  
    删除所有容器

4. docker rmi [image_id/image_name]  
    删除镜像

   docker rmi \`docker images -q\`    
    删除所有镜像

   docker rmi \`docker images -f "dangling=true" -q\`
    删除dangling的镜像

5. docker ps -a  
    列出当前运行的容器

   docker run [-it] [image_id/image_name] command  
    根据镜像，创建运行容器

   docker rename oldname newname

   docker start [container_id/container_name]
   docker stop [container_id/container_name]

   docker stop \`docker ps -q\`    
   停止所有运行的容器


6. docker exec [-it] [container_id/container_name]  
    进入容器

    exit  
    退出容器


7. docker diff [container_id/container_name]  
    查看容器做了什么更改

    (应该用Dockerfile来实现新的镜像的制作)
      docker commit [options] [container_id/container_name] [repository][:tag]  
    根据在容器所做的修改发布新的镜像  
    note： options， --author "wens"   --message "i add new index html"



8. docker build [image_name][:tag] [context path]  
    制作镜像

    note: context path should contain Dockerfile


9. docker log [container_id/container_name]  
    查看container的输出

10. docker inspect [-f "双花括号dot Id双花括号"] [container_id/container_name]  
    查看容器的内容(只查看长Id)

11. [XXXX(container_name)]  env


