<p align="center"><img src="./static/logo.png" alt="Torpedo Logo" width="420" /></p>

# Torpedo — 更好的闲鱼运营自动化平台

[![License](https://img.shields.io/github/license/mung6lung4/torpedo?style=flat-square)](./LICENSE)
[![Release](https://img.shields.io/github/v/release/mung6lung4/torpedo?display_name=tag&style=flat-square)](https://github.com/mung6lung4/torpedo/releases)
[![Stars](https://img.shields.io/github/stars/mung6lung4/torpedo?style=flat-square)](https://github.com/mung6lung4/torpedo/stargazers)
[![Issues](https://img.shields.io/github/issues/mung6lung4/torpedo?style=flat-square)](https://github.com/mung6lung4/torpedo/issues)
[![Last Commit](https://img.shields.io/github/last-commit/mung6lung4/torpedo?style=flat-square)](https://github.com/mung6lung4/torpedo/commits/main)

Torpedo 是一个面向闲鱼卖家的运营自动化系统，覆盖「消息处理、自动回复、自动发货、订单管理、Webhook/通知」等核心链路，支持多账号、多用户隔离与 Docker 一键部署。

## 文档入口

- Torpedo 官方文档：[https://docs.torpedo.homes](https://docs.torpedo.homes)

<div align="center">
  <h1>现开放尝鲜试用，卡密领完为止</h1>
  <p><strong>新用户限量开放体验资格，建议先体验后部署。</strong></p>
  <p><a href="https://shop.torpedo.homes">立即领取试用资格</a></p>
</div>

## 适合谁

- 个人卖家：稳定自动回复、自动发货，减少重复劳动
- 工作室/团队：多账号管理、通知联动、Webhook 接入业务系统

## 功能概览

- 多账号并行：一个面板管理多个闲鱼账号，独立运行、互不影响
- 消息处理：WebSocket 实时接收消息，内置防抖、去重与任务队列
- 自动回复：商品专用回复、关键词回复、默认回复、AI 回复（可选）
- 自动发货：规则匹配、延时发货、API 卡券/文本/图片等多种发货方式
- 订单管理：订单详情拉取、状态维护、发货/确认发货链路
- Webhook：订单完成等事件回调；支持按 HTTP 状态码执行「回发消息动作」
- 通知系统：多渠道通知；支持「渠道 → 绑定账号 → 触发点」全链路配置与排障
- 运维友好：日志轮转、健康检查、数据库自动迁移、容器化部署


## 贡献

欢迎提交 Issue / PR（请尽量附上日志与复现步骤）。


## 示例功能体验

为便于快速了解 Torpedo 在真实业务场景下的能力边界与交互流程，已提供在线示例环境，建议先行体验后再进行正式部署评估。

- 体验地址：`torpedo.homes`
- 登录账号：`Torpedo`
- 登录密码：`Torpedo`

说明：示例环境用于功能演示与流程验证，请勿录入真实业务数据或敏感信息。

## 部署方式

### 方式一：单命令部署（docker run）

```bash
docker run -d --name torpedo-latest --restart unless-stopped --init --user 0:0 -p 8080:8080 -v ./data:/app/data:rw -v ./logs:/app/logs:rw -v ./backups:/app/backups:rw -v ./static/uploads:/app/static/uploads:rw -v ./static/uploads:/app/static-dist/uploads:rw -v /etc/localtime:/etc/localtime:ro -e STATIC_DIR=/app/static-dist -e ACTIVATION_MASTER_KEY=123456 -e API_SECRET_KEY=123456 --log-driver json-file --log-opt max-size=1m --log-opt max-file=3 --health-cmd "curl -f http://localhost:8080/health" --health-interval 30s --health-timeout 10s --health-retries 3 --health-start-period 40s mung6lung4/torpedo:latest
```

### 方式二：YAML 部署（docker compose）

```bash
docker compose -f docker-compose.yml up -d
```

