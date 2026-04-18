# Texas Hold'em Online Poker Server

[![License: AGPL v3](https://img.shields.io/badge/License-AGPLv3-blue.svg)](LICENSE)
[![C++17](https://img.shields.io/badge/C%2B%2B-17-blue.svg)](https://isocpp.org/)
[![Build Status](https://img.shields.io/badge/build-passing-brightgreen)]()
[![Stars](https://img.shields.io/github/stars/deeptexas-ai/Texas-Hold-em_Online-Poker-Software?style=social)]()
[![Docker Pulls](https://img.shields.io/docker/pulls/deeptexas/poker_server)]()

**生产级德州扑克服务端** — 已在真实线上环境盈利运营多年，与 HHpoker、WPK 等头部产品直接竞争。

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

## 📸 界面预览

| 大厅界面 | 牌桌对战 | 后台管理 |
|:--------:|:--------:|:--------:|
| ![大厅](https://via.placeholder.com/400x250?text=Lobby+Screen) | ![牌桌](https://via.placeholder.com/400x250?text=Table+Screen) | ![后台](https://via.placeholder.com/400x250?text=Admin+Panel) |

> 真实界面截图请联系获取演示地址。

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

## 🤝 商业支持
本项目为 AGPL v3 开源协议免费使用。如需以下商业服务，请联系：

## 服务类型	说明
🔒 商业授权	去除开源协议限制，闭源使用
🛠️ 定制开发	新增玩法、UI定制、特殊功能
☁️ 运维托管	服务器部署、7x24小时监控
📈 运营指导	游戏运营策略、风控方案

## 产品截图
[我们的德州项目不是网上那种外包团队的德州产品：没有在市场上盈利过，中看不中用，代码中漏洞不少的德州产品；是真正在市场上盈利过，运营多年的德州]
![3联盟-加入主页](https://github.com/user-attachments/assets/205c0b50-5600-4ab4-a954-e361311a4b9a)
![3联盟-充值联盟币](https://github.com/user-attachments/assets/e0fc4fe0-61ca-480a-a099-dde20cf38f5a)
![03赛事4](https://github.com/user-attachments/assets/a755bbb1-70c0-4f3c-9c69-b89377dbbb59)

![02创建1](https://github.com/user-attachments/assets/acc0fa3a-d864-41a3-9d91-a669cf5de648)
![1管理俱乐部币](https://github.com/user-attachments/assets/722fa342-865b-410b-801b-e5cd11488d12)
![1房间列表](https://github.com/user-attachments/assets/4ac89b79-94de-4903-8a5a-ed080d5ec24d)
![01](https://github.com/user-attachments/assets/d1a5299a-ac9a-47e6-9206-d0ebae3a1dec)
![05牌桌-查看头像1](https://github.com/user-attachments/assets/349d9333-fe5c-46ca-913d-39bc35bc95e0)
![4房间2-9人桌](https://github.com/user-attachments/assets/0d709180-2259-45b4-9f99-17f0dcb41e3a)
![4房间2-6人桌](https://github.com/user-attachments/assets/1549d61a-2dc4-4059-ad86-a68464e78d88)
## 联系方式：

📱 Telegram: @xuzongbin001

📧 Email: masterai918@gmail.com



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



