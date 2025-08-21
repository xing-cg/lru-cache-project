## 一、背景与目的

为降低开发者搭建 trpc-cpp 编译环境的复杂度，同时提供隔离、可复现的开发环境，我将编译依赖打包为 Docker 镜像，支持开箱即用的 trpc-cpp 框架编译与开发。



## 二、Docker 镜像信息

- [trpc-cpp-env 镜像仓库地址](https://hub.docker.com/r/woodycpp/trpc-cpp-env)

- 支持平台

  该镜像为多平台镜像，兼容以下两种 CPU 架构：

  - linux/amd64（Intel/AMD 64 位架构）
  - linux/arm64（Apple M 系列芯片）

Docker 镜像仓库地址： 

- 镜像版本示例： woodycpp/trpc-cpp-env:13.3.0 

- 支持平台：该镜像为多平台镜像，兼容以下两种 CPU 架构： 

  - x86-64（Intel/AMD 64 位架构）

  - ARM64/V8（如 Apple M 系列芯片、ARM 服务器等）

  > Bazel 构建工具在不同架构下的安装方式存在差异，镜像已内置适配逻辑，开发者无须手动处理。



## 三、编译环境搭建步骤

1. 拉取 trpc-cpp 源码

   ```shell
   git clone https://github.com/trpc-group/trpc-cpp.git
   ```

2. 启动编译容器

   推荐使用  docker-compose 工具快速启动开发容器，docker-compose.yaml 配置文件如下：

   ```yaml
   services:
     trpc-cpp:
       image: woodycpp/trpc-cpp-env:13.3.0
       container_name: trpc-cpp
   
       stdin_open: true
       tty: true
   
       entrypoint: ["bash"]
       working_dir: /trpc-cpp
   
       volumes:
         - ${TRPC_SRC_PATH}:/trpc-cpp
   ```

   其中，${TRPC_SRC_PATH} 是一个变量，需替换为本地的 trpc-cpp 源码目录绝对路径。

   执行以下命令启动容器：

   ```shell
   docker-compose up -d
   ```

3. 进入容器

   执行以下命令进入容器的交互式 Shell：

   ```shell
   docker exec -it trpc-cpp bash
   ```

4. 编译 trpc-cpp 项目

   执行官方提供的构建脚本编译 trpc-cpp 项目：

   ```shell
   ./build.sh
   ```

   该脚本包含 Bazel 构建命令及相关构建参数。

   首次编译时，Bazel 会下载依赖并构建工具链，耗时可能较长，请耐心等待。

   如遇到构建错误，请结合错误日志排查，编译相关错误可以参考官方文档 [bazel cmake faq](https://github.com/trpc-group/trpc-cpp/blob/main/docs/zh/faq/bazel_and_cmake_problem.md) 或提交 issue。

   