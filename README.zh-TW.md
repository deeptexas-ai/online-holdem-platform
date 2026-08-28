# Texas Hold'em Online Poker Platform | 德州撲克線上平台源碼

[簡體中文](README.md) | [English](README.en.md) | [繁體中文](README.zh-TW.md)

Texas Hold'em Online Poker Platform 是一套面向商业化评估和二次开发的線上德州撲克服務端源碼項目，核心包含 C++ 遊戲服務端、即時多人牌局、房间消息、客户端消息、推送服务、协议文件、牌局状态、俱乐部/私人局、比赛玩法和後台營運对接方向。

## 核心定位

- 德州撲克源碼 / Texas Hold'em poker source code
- 線上扑克平台 / online poker platform
- C++ 即時遊戲服務端 / C++ poker game server
- 多人即時牌局、金币大厅、私人局、俱乐部和联盟模式
- SNG、MTT、短牌、奥马哈、大菠萝等扩展玩法方向
- 适合商业评估、私有化部署、源碼学习和二次开发

## 核心功能

- 牌局服务：牌局状态、玩家动作、下注轮次、结算逻辑和房间生命周期
- 消息处理：客户端消息、房间消息、推送服务、协议资源和业务处理模块
- 多玩法扩展：经典德州、短牌、SNG、MTT、奥马哈、大菠萝和德州牛仔
- 社交玩法：私人局、朋友局、俱乐部、联盟、语音聊天和战绩统计
- 營運能力：後台管理、玩家管理、对局审计、奖励配置和營運數據
- 技术基础：C++ 服務端、Tars/协议文件、MySQL、Redis、日志和部署文檔

## 項目结构建议

```text
Doc/                    # 原有说明文檔
Screenshots/            # 产品截图
docs/                   # GitHub Pages 产品与技术文檔
message/                # 消息与协议处理模块
process/                # 业务流程处理模块
protos/                 # 协议资源
utils/                  # 通用工具
config.example/         # 脱敏配置示例
scripts/                # 构建、部署和维护脚本
tests/                  # 规则、结算、接口和压力测试
.github/workflows/      # CI 与 GitHub Pages 自动发布
```

## 公開仓库安全建议

公開仓库适合展示产品结构、部分源碼、截图和技术文檔。不要公開真實用戶數據、支付密钥、後台帳號、生产數據库、私有營運數據、风控参数、线上配置、真實订单或未授权素材。

## 文檔

- [項目主页](docs/index.html)
- [功能介绍](docs/features.html)
- [架构说明](docs/architecture.html)
- [部署指南](docs/deployment.html)
- [合规使用](docs/responsible-use.html)

## 联系方式

Telegram：`@xuzongbin001`  
Email：`masterai918@gmail.com`

## License

具体以仓库 License 文件为准。公開使用、商业部署和闭源集成前，请确认授权边界。
