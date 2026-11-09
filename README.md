# 🟢 Auto Green Keep-Alive

> &zwnj;**Because nobody can read your mind (yet), but GitHub can read your commits.**&zwnj;

这是一个轻量级的 GitHub Actions 工作流，旨在自动维持 GitHub 贡献图（Contribution Graph）的活跃度。通过定时提交微小变更，确保你的贡献格子保持绿色，展示你的持续活跃状态。

## ✨ 特性

- 🚀 &zwnj;**全自动运行**&zwnj;：基于 GitHub Actions Cron 调度，无需人工干预。
- 🔒 &zwnj;**安全隐私**&zwnj;：敏感信息（邮箱、用户名）通过 GitHub Secrets 管理，代码中无明文泄露。
- 🍃 &zwnj;**轻量级**&zwnj;：仅生成极小的文本文件变更，不污染仓库历史。
- ⚙️ &zwnj;**可配置**&zwnj;：支持自定义提交频率和用户信息。

## 📖 工作原理

1. &zwnj;**定时触发**&zwnj;：工作流按照设定的 Cron 表达式（默认每4小时）自动触发。
2. &zwnj;**生成变更**&zwnj;：脚本创建一个包含当前时间戳的文件 `.keep-alive`。
3. &zwnj;**安全提交**&zwnj;：使用存储在 Secrets 中的 Git 配置信息进行 commit 和 push。
4. &zwnj;**更新贡献图**&zwnj;：GitHub 识别到有效代码提交，更新个人主页的贡献统计。

## 🛠️ 安装与设置

### 1. 克隆或创建仓库

将此模板应用到你的 GitHub 仓库中。

### 2. 配置 Secrets (关键步骤)

为了让 Action 能够以你的身份提交代码，你需要在仓库设置中添加两个 Secrets：

1. 进入仓库的 &zwnj;**Settings**&zwnj; > &zwnj;**Secrets and variables**&zwnj; > &zwnj;**Actions**&zwnj;。
2. 点击 &zwnj;**New repository secret**&zwnj;，添加以下两个变量：

| Name | Value | 说明 |
| :--- | :--- | :--- |
| `GIT_EMAIL` | 你的 GitHub 注册邮箱 | 例如: `yourname@example.com` |
| `GIT_USERNAME` | 你的 GitHub 用户名 | 例如: `yourname` |

### 3. 启用 Workflows

确保 `.github/workflows/auto-green.yml` 文件已存在于仓库中。如果需要修改提交频率，可以编辑该文件中的 `cron` 表达式。

## 📅 自定义提交频率

默认配置为每 4 小时运行一次。如果你希望调整频率，请编辑 `.github/workflows/auto-green.yml`：

```yaml
on:
  schedule:
    # 格式: 分 时 日 月 周
    # 下面表示每天 UTC 时间的 0:50, 4:50, 8:50... 运行
    - cron: "50 0/4 * * *"
