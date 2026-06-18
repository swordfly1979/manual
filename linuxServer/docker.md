# Podman,docker容器常用命令

```bash
docker compose up -d #起动docker容器
docker compose down #结束容器
docker rm -f <image>  #删除容器
docker ps #查看容器运行状态
docker logs <image> #查看运行中容器

podman images  # 查看已有镜像
podman rmi <image>	#删除指定镜像
podman rmi -a	#删除所有镜像
podman image prune	#删除悬空镜像
podman image prune -a	#删除所有未使用镜像
podman system prune	#清理所有未使用资源
podman system prune -a -f	#强制清理所有
podman image tree <image>  # 查看镜像的层级关系
podman inspect <image>  # 查看镜像详细信息
```
