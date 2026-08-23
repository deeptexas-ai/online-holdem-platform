# online-holdem-platform 完整优化方案

## 当前问题

1. README 标题和 About 重复堆叠“德州源码”等关键词。
2. 克隆命令指向 `Texas-Hold-em_Online-Poker-Software.git`，与当前仓库地址不一致。
3. 根目录未显示 `CMakeLists.txt`、`Dockerfile`、`docker-compose.yml`、`scripts/init_db.sh` 或 `config/server.ini`，但 README 将它们写成可直接使用。
4. 许可证文件名为 `License.md`，徽章和正文却引用 `LICENSE`。
5. Build Status 和 Docker Pulls 徽章没有指向真实构建或镜像数据。
6. 多玩法、后台、CSPRNG、性能和可用性声明缺少对应源码入口或可复现报告。
7. Topics 使用第三方品牌词，并存在多个同义重复词。

## 建议源码目录

```text
.
|-- README.md
|-- License.md
|-- CONTRIBUTING.md
|-- SECURITY.md
|-- CHANGELOG.md
|-- docs/
|   |-- texas-holdem-source-code.md
|   |-- server-architecture.md
|   |-- build-guide.md
|   |-- protocol-message-guide.md
|   |-- game-flow.md
|   |-- security-compliance.md
|   `-- faq.md
|-- config/
|   `-- example.conf          # 不含密码和密钥
|-- examples/                 # 最小协议或调用示例
|-- tests/                    # 状态机、消息和牌型测试
|-- scripts/                  # 可复现构建脚本
|-- benchmarks/               # 性能测试代码与原始结果
`-- .github/workflows/        # 真实 CI，而非装饰性徽章
```

## 必须补充的工程内容

- 将 Makefile 中的本机绝对路径改为变量，并列出经过验证的系统、编译器和 Tars 版本。
- 添加去除凭据的配置样例，说明端口、日志、服务发现和依赖项。
- 添加消息编解码、非法请求、状态转换、断线重连和并发操作测试。
- 若确实支持 CMake、Docker、MySQL 或 Redis，再提交对应文件并恢复文档；否则删除这些运行命令。
- 性能数字必须附测试代码、机器配置、数据规模、持续时间和原始结果。
- 随机数安全必须指出具体实现文件、算法与审计状态。
- 建立 `v0.1.0` 等 Release，写明公开源码范围、构建方法和校验值。

## 搜索内容布局

主关键词：`德州源码`、`德州扑克源码`。

辅助关键词：`在线德州扑克服务端`、`C++ 扑克游戏源码`、`Texas Hold'em source code`、`online poker server`。

每个 docs 页面只回答一个具体问题，并从 README 链接。不要批量复制相同正文后替换关键词。

## 下载转化优化

1. README 首屏明确说明公开仓库到底包含什么。
2. 提供正确的 Download ZIP 与 Git 克隆命令。
3. 增加真实可复现构建步骤和 CI 状态。
4. 展示 3 至 5 张清晰截图，不用截图代替源码范围说明。
5. 提供最小可运行测试或协议示例。
6. 使用 GitHub Release 承载版本下载，并附变更记录。
7. FAQ 直接回答是否含客户端、数据库和后台。

## Google 收录

GitHub 仓库可被 Google 抓取，但独立文档站更容易控制标题、description、canonical、sitemap 和结构化数据。建议使用 GitHub Pages 建立文档站，通过 Google Search Console 提交 sitemap。外部文章应链接具体技术文档，不要发布重复广告文本或购买垃圾外链。

## 执行顺序

1. 替换 README、About 与 Topics。
2. 修复错误仓库地址、许可证链接和虚假徽章。
3. 删除无法验证的运行命令及性能结论。
4. 补齐构建、配置、测试和安全说明。
5. 发布首个规范 Release。
6. 建立 GitHub Pages 文档站并提交 Google。

