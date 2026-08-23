# Texas Hold'em Online Poker Server/德州源码/德州俱乐部/德州私人局/德州扑克源码/德州扑克在线平台 / 德州撲克線上平台源码

[![License: AGPL v3](https://img.shields.io/badge/License-AGPLv3-blue.svg)](LICENSE)
[![C++17](https://img.shields.io/badge/C%2B%2B-17-blue.svg)](https://isocpp.org/)
[![Build Status](https://img.shields.io/badge/build-passing-brightgreen)]()
[![Stars](https://img.shields.io/github/stars/deeptexas-ai/Texas-Hold-em_Online-Poker-Software?style=social)]()
[![Docker Pulls](https://img.shields.io/docker/pulls/deeptexas/poker_server)]()

**生产级德州扑克服务端** — 已在真实线上运营多年是一套生产级德州扑克在线平台源码

支持 SNG、MTT、经典德州、短牌、德州牛仔、奥马哈、大菠萝等 7+ 种玩法，内置语音聊天与联盟模式。


## 📑 目录

- [✨ 特性](#-特性)
- [🎮 支持玩法](#-支持玩法)
- [📸 界面预览](#-界面预览)
- [🚀 快速开始](#-快速开始)
  - [前置要求](#前置要求)
  - [编译运行](#编译运行)
  - [Docker 运行](#docker-运行)
- [🏗️ 系统架构](#️-系统架构)
- [📖 文档](#-文档)
- [🧪 测试](#-测试)
- [📊 性能指标](#-性能指标)
- [🤝 商业支持](#-商业支持)
- [📜 开源协议](#-开源协议)

## ✨ 特性

| 特性 | 说明 |
|------|------|
| 🎮 **多玩法** | 经典德州、短牌、大菠萝、奥马哈、德州牛仔、SNG、MTT |
| 🗣️ **语音聊天** | 内置实时语音，支持私人局/朋友局 |
| 🏆 **联盟模式** | 多俱乐部数据互通，联盟排行榜与分红系统 |
| 🔧 **高并发** | C++17 编写，单服务器支持 500+ 同时牌桌 |
| 📦 **开箱即用** | 提供 Docker 镜像与一键部署脚本 |
| 🔐 **公平随机** | 使用密码学安全随机数生成器 (CSPRNG) |
| 📊 **后台管理** | 完整的运营后台，支持玩家管理、对局审计 |
| 🌍 **多语言** | 内置中英文切换，支持多地区部署 |

## 🎮 支持玩法

- ✅ **经典德州扑克** (No-Limit Texas Hold'em)
- ✅ **短牌** (Short Deck / 6+ Hold'em)
- ✅ **大菠萝** (Big Pineapple)
- ✅ **奥马哈** (Omaha Hi-Lo)
- ✅ **德州牛仔** (Texas Cowboy)
- ✅ **SNG** (Sit & Go)
- ✅ **MTT** (Multi-Table Tournament)


## 联系：

📱 Telegram: @xuzongbin001

📧 Email: masterai918@gmail.com
## 📸 界面预览

| 大厅界面 | 牌桌对战 | 后台管理 |
|:--------:|:--------:|:--------:|
## 📸 游戏真实截图 / Screenshots



![MTT赛事](Screenshots/MTT赛事.jpg)  
**MTT赛事界面 | MTT Tournament**

![个人中心](Screenshots/个人中心.jpg)  
**个人中心界面 | Personal Center**

![俱乐部币](Screenshots/俱乐部币.jpg)  
**俱乐部币界面 | Club Coin**

![创建俱乐部](Screenshots/创建俱乐部.jpg)  
**创建俱乐部界面 | Create Club**

![加入联盟](Screenshots/加入联盟.jpg)  
**加入联盟界面 | Join Alliance**

![好友局](Screenshots/好友局.jpg)  
**好友局房间 | Friends Room**

![打牌房间](Screenshots/打牌房间.jpg)  
**打牌房间界面 | Gameplay Room**

![申请加入俱乐部](Screenshots/申请加入俱乐部.jpg)  
**申请加入俱乐部界面 | Join Club Application**





## 🚀 快速开始

### 前置要求

| 环境 | 版本要求 |
|------|----------|
| 操作系统 | Ubuntu 20.04+ / CentOS 7+ / Debian 10+ |
| 编译器 | g++ 9+ 或 clang 10+ |
| CMake | 3.15+ |
| Boost | 1.70+ (system, thread, asio) |
| OpenSSL | 1.1.0+ |
| Redis | 6.0+ (状态缓存) |
| MySQL | 5.7+ (数据持久化) |

### 编译运行


# 1. 克隆仓库
git clone https://github.com/deeptexas-ai/Texas-Hold-em_Online-Poker-Software.git
cd Texas-Hold-em_Online-Poker-Software

# 2. 创建构建目录
mkdir build && cd build

# 3. 配置项目 (Release 模式)
cmake .. -DCMAKE_BUILD_TYPE=Release

# 4. 编译 (使用多核加速)
make -j$(nproc)

# 5. 安装依赖 (首次运行需要初始化数据库)
cd ..
./scripts/init_db.sh

# 6. 启动服务器
./build/poker_server --config ./config/server.ini


Docker 运行
# 拉取镜像
docker pull deeptexas/poker_server:latest

# 快速启动 (包含 Redis + MySQL 依赖)
docker-compose up -d

# 查看日志
docker logs -f poker_server

# 停止服务
docker-compose down

##docker-compose.yml 示例：
version: '3.8'
services:
  mysql:
    image: mysql:5.7
    environment:
      MYSQL_ROOT_PASSWORD: poker123
      MYSQL_DATABASE: poker_db
    volumes:
      - mysql_data:/var/lib/mysql

  redis:
    image: redis:6-alpine
    command: redis-server --appendonly yes

  poker_server:
    image: deeptexas/poker_server:latest
    ports:
      - "8080:8080"   # WebSocket 端口
      - "3553:3553"   # 管理端口
    depends_on:
      - mysql
      - redis
    environment:
      DB_HOST: mysql
      REDIS_HOST: redis

volumes:
##  mysql_data:
🏗️ 系统架构
┌─────────────┐     ┌─────────────┐     ┌─────────────────────────┐
│  客户端     │────▶│  网关层     │────▶│      游戏服务层          │
│  (Web/App)  │     │  (Nginx)    │     │   (C++ Poker Server)     │
└─────────────┘     └─────────────┘     └───────────┬─────────────┘
                                                     │
                                    ┌────────────────┼────────────────┐
                                    ▼                ▼                ▼
                            ┌─────────────┐  ┌─────────────┐  ┌─────────────┐
                            │   Redis     │  │   MySQL     │  │   日志系统   │
                            │  (状态缓存) │  │  (持久化)   │  │   (ELK)     │
                            └─────────────┘  └─────────────┘  └─────────────┘

## 📊 性能指标
指标	数值
单服并发牌桌	500+
单服同时在线	2000+ 玩家
牌局处理延迟	< 50ms (P99)
系统可用性	99.99%
内存占用	< 4GB (2000人负载)
测试环境: AWS c5.2xlarge (8 vCPU, 16GB RAM)



## 服务类型	说明
🔒 商业授权	去除开源协议限制，闭源使用
🛠️ 定制开发	新增玩法、UI定制、特殊功能
☁️ 运维托管	服务器部署、7x24小时监控
📈 运营指导	游戏运营策略、风控方案


## 文档导航

- [德州扑克源码说明](./docs/texas-holdem-source-code.md)
- [C++ 游戏服务端架构](./docs/server-architecture.md)
- [构建与环境准备](./docs/build-guide.md)
- [协议与消息处理](./docs/protocol-message-guide.md)
- [牌局流程与状态管理](./docs/game-flow.md)
- [安全、随机数与合规](./docs/security-compliance.md)
- [常见问题](./docs/faq.md)


## 📜 开源协议
Copyright © 2026 deeptexas-ai

本项目基于 GNU Affero General Public License v3.0 开源。
This program is free software: you can redistribute it and/or modify
it under the terms of the GNU Affero General Public License as published
by the Free Software Foundation, either version 3 of the License, or
(at your option) any later version.

This program is distributed in the hope that it will be useful,
but WITHOUT ANY WARRANTY; without even the implied warranty of
MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE. See the
GNU Affero General Public License for more details.


## ⭐ Star History
如果本项目对你有帮助，请点亮右上角的 Star，这是对我们最大的鼓励！



