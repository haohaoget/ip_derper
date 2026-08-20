# docker-compose部署方法

## 创建docker-compose.yml文件，添加如下内容
```
version: "3.8"

services:
  derper:
    image: haohaodc/ip_derper
    container_name: derper
    restart: always
    ports:
      - "3478:3478/udp"
      - "43562:43562"
    volumes:
      - /var/run/tailscale/tailscaled.sock:/var/run/tailscale/tailscaled.sock
    environment:
      - DERP_ADDR=:43562
      - DERP_VERIFY_CLIENTS=true
  ```
使用命令 `docker compose up -d` 部署

# 更新方法
下载最新镜像：`docker pull haohaodc/ip_derper:latest`

停止运行中的容器：`docker stop derper`

删除停止的容器：`docker rm derper`

删除停止容器的镜像：`docker images` 找到old容器的镜像的id，使用`docker rmi id`

使用命令 `docker compose up -d` 部署
