# C++ 在线扑克服务端架构

仓库可见代码由游戏服务、牌局状态、消息、协议、业务流程和工具模块组成。

```text
客户端/房间消息
       |
       v
onclientmessage / onroommessage
       |
       v
process / gameroot / gamestation
       |
       v
sendclientmessage / sendroommessage / PushServant
```

这是阅读方向，不代表完整运行时拓扑。二次开发前应从实际调用关系确认线程模型、对象生命周期、服务发现、持久化和错误处理。

建议将网络协议、牌局状态机、数据访问和日志分离，为每个状态转换建立测试，并记录服务启动与关闭顺序。

