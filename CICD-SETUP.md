# CI/CD 工作流配置指南 🚀

本仓库已配置完整的 CI/CD 流水线，包含测试、构建、部署、监控和通知功能。

## 📋 工作流概览

```
push → CI 测试 → 构建 Docker → 推送 Docker Hub → 部署 → 健康检查 → Discord 通知
```

## 🔐 需要配置的 Secrets

在 GitHub 仓库 Settings → Secrets and variables → Actions 中添加以下 Secrets：

| Secret 名称 | 说明 | 是否必需 |
|------------|------|---------|
| `DOCKER_USERNAME` | Docker Hub 用户名 | ✅ 必需 |
| `DOCKER_PASSWORD` | Docker Hub 访问令牌 | ✅ 必需 |
| `DISCORD_WEBHOOK` | Discord 频道 Webhook URL | ⚠️ 推荐 |
| `SSH_PRIVATE_KEY` | 服务器 SSH 私钥 | ⚠️ 如需自动部署 |
| `DEPLOY_SERVER` | 部署服务器地址 (user@host) | ⚠️ 如需自动部署 |

## 🛠️ 配置步骤

### 1. Docker Hub 配置

```bash
# 获取 Docker Hub Access Token
# 访问 https://hub.docker.com/settings/security
# 创建 New Access Token
```

### 2. Discord Webhook 配置

1. 进入 Discord 服务器频道设置
2. 编辑频道 → 集成 → Webhooks
3. 创建 Webhook → 复制链接

### 3. SSH 部署配置（可选）

```bash
# 生成 SSH 密钥
ssh-keygen -t ed25519 -C "github-actions"

# 将公钥添加到服务器 ~/.ssh/authorized_keys
# 将私钥添加到 GitHub Secrets (SSH_PRIVATE_KEY)
```

## 📊 工作流说明

| Job | 说明 |
|-----|------|
| `ci-test` | 运行代码测试和 lint 检查 |
| `cd-deploy` | 构建 Docker 镜像并推送到 Docker Hub |
| `monitoring` | 部署后健康检查 |
| `notify` | 发送 Discord 通知报告 |

## 🎯 触发方式

- **自动触发**: push 到 main 分支
- **手动触发**: Actions 标签页 → 选择 workflow → Run workflow

## 📝 查看运行状态

- Actions 标签页查看运行历史
- Discord 频道接收部署通知

---

**创建时间**: 2026-03-10
**作者**: KONA
