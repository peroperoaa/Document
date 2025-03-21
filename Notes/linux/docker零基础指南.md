# Docker 零基础指南

Docker 是一种应用库容器化平台，帮助开发者将应用及其依赖进行打包，以便在任何环境中确保一致性。本指南为零基础学习者提供了如何使用 Docker、简单 Dockerfile 编写和基础操作的教程。

#### 一、Docker 基本概念

1. **镜像 (Image)**：镜像是一个只读的模板，包含应用程序及其运行所需的所有依赖。镜像用于创建容器，可以看作是容器的蓝图。
2. **容器 (Container)**：容器是镜像的一个运行实例，提供了一个独立的环境来运行应用程序。容器是轻量级的，支持快速启动和销毁，并且相互隔离，确保运行环境的独立性。
3. **Dockerfile**：Dockerfile 是一个文本文件，包含一系列指令，用于描述如何创建一个 Docker 镜像。通过 Dockerfile，可以自动化镜像的构建过程，例如安装依赖、配置环境等。
4. **守护进程 (Daemon)**：Docker 守护进程是运行在后台的服务，负责管理 Docker 容器、镜像、网络等资源。守护进程在 Docker 服务启动时自动启动，是 Docker 的核心部分。

#### Docker 的架构

Docker 采用 C/S（客户端/服务器）架构，主要包括以下几个部分：

- **客户端-服务器架构 (Client-Server Architecture)**

  - **Docker 客户端 (Client)**：用户通过命令与 Docker Daemon 通信，主要用于向守护进程发送命令，如创建容器、管理镜像等。
  - **Docker 守护进程 (Daemon)**：Docker 的核心后台服务，负责处理容器的创建、管理、网络、存储等操作，是 Docker 生态系统中的核心部分。

- **Docker 镜像和容器**

  - **Docker 镜像 (Images)**：包含应用及其所需环境的模板，用于创建容器。镜像可以理解为容器的蓝图，用户可以通过镜像快速启动容器。
  - **Docker 容器 (Containers)**：镜像的运行实例，用于运行应用程序。每个容器都是从镜像创建并运行的，具有自己的文件系统和网络环境，彼此隔离，轻量级且灵活。

- **Docker Registry (镜像仓库)**

  - **Docker Registry**：用于存储和分发镜像的服务，例如官方的 Docker Hub。用户可以将自己创建的镜像推送到 Docker Registry 中，其他用户也可以从 Registry 拉取这些镜像。

#### 二、Docker 安装和启动

1. 安装 Docker：可前往 [Docker官网](https://www.docker.com/get-started) 下载适合的系统版本并进行安装。
2. 启动 Docker ：
   - **Linux 系统**：`sudo apt-get install docker`
   - **Windows 和 macOS**：安装时通常自动启动。

#### 三、Docker 基本操作

1. **查看 Docker 版本**：

   ```sh
   docker --version
   ```

2. **拉取镜像**：

   ```sh
   docker pull <镜像名>
   ```

   例如：

   ```sh
   docker pull ubuntu
   ```

3. **列出本地镜像**：

   ```sh
   docker images
   ```

4. **运行容器**：

   ```sh
   docdocker run -it <镜像名> /bin/bash // -i 让容器保持标准输入打开，-t 为容器分配一个伪终端
   ```

5. **列出正在运行的容器**：

   ```sh
   docker ps
   ```

6. **查看所有容器 (包括已结束的)**：

   ```sh
   docker ps -a
   ```

7. **停止容器**：

   ```sh
   docker stop <容器ID>
   ```

8. **删除容器**：

   ```sh
   docker rm <容器ID>
   ```

9. **删除镜像**：

   ```sh
   docker rmi <镜像ID>
   ```

#### 四、Dockerfile 简单编写

Dockerfile 用于定义如何创建一个镜像，下面是一个示例。

```Dockerfile
# 使用官方的基础镜像
FROM ubuntu:latest

# 更新系统并安装一些基础软件
RUN apt-get update && apt-get install -y curl

# 创建应用目录
WORKDIR /app

# 将主机的文件复制到容器中
COPY . /app

# 暴露端口
EXPOSE 8080

# 容器启动时运行的命令
CMD ["echo", "Hello, Docker!"]
```

#### 五、使用 Dockerfile 构建镜像

使用下面的命令来构建镜像：

```sh
docker build -t my-ubuntu-app .
```

#### 六、使用容器的基础管理

1. **启动容器并进入交互模式**：

   ```sh
   docker run -it my-ubuntu-app /bin/bash
   ```

2. **将容器以后台守护进程的形式运行**：

   ```sh
   docker run -d my-ubuntu-app
   ```

3. **查看容器日志**：

   ```sh
   docker logs <容器ID>
   ```

4. **进入一个正在运行的容器**：

   ```sh
   docker exec -it <容器ID> /bin/bash
   ```

#### 七、Docker 的常用选项

1. **-p**：用于端口映射。

   ```sh
   docker run -p 8080:80 my-ubuntu-app
   ```

2. **-v**：用于数据卷映射，将主机目录挂载到容器。

   ```sh
   docker run -v /path/on/host:/path/in/container my-ubuntu-app
   ```

3. **--name**：指定容器名称，便于管理。

   ```sh
   docker run --name my-container my-ubuntu-app
   ```

4. **-e**：设置环境变量。

   ```sh
   docker run -e MY_ENV_VAR=value my-ubuntu-app
   ```

### 总结

1. Docker 为应用提供了轻量化的容器，帮助开发者确保在各种环境中的一致性。
2. Dockerfile 用于定义如何构建镜像的过程。
3. Docker 进行容器的创建、启动和管理。