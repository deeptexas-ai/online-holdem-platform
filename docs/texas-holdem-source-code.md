# 德州扑克源码说明

当前公开仓库以 C++ 在线德州扑克服务端源码为主，包含游戏服务、牌局状态、客户端与房间消息、推送接口、协议、业务流程和工具模块。

## 推荐阅读顺序

1. 从 `gameserver.cpp` 查看服务入口。
2. 阅读 `gameroot.cpp` 与 `gamestation.cpp` 理解对象和状态。
3. 查看 `onclientmessage.cpp`、`onroommessage.cpp` 的消息入口。
4. 对照 `sendclientmessage.cpp`、`sendroommessage.cpp` 查看响应。
5. 阅读 `PushServant.tars` 与 `protos/` 理解协议。
6. 检查 `process/`、`message/` 和 `utils/` 的调用关系。

[前往 GitHub 下载德州扑克源码](https://github.com/deeptexas-ai/online-holdem-platform)

客户端、数据库、后台及商业组件是否包含，应以实际目录和授权范围为准。

