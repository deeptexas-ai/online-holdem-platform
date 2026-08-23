# 构建与环境准备

仓库当前根目录提供 `makefile`，未显示 `CMakeLists.txt`。应以 Makefile 中的真实依赖和目标为准。

## 获取源码

```bash
git clone https://github.com/deeptexas-ai/online-holdem-platform.git
cd online-holdem-platform
```

## 构建检查

- 操作系统和 CPU 架构
- GCC/G++ 版本与 C++ 标准
- Tars 工具、头文件与运行库版本
- Makefile 的包含路径和链接路径
- 依赖的内部服务及配置

```bash
make
```

若失败，请记录系统、编译器、依赖版本、完整命令和第一处错误。仓库中不存在的 CMake、Docker、数据库初始化命令不应直接写进快速开始。

