# 360AI云盘技能库 (ECS Yunpan Skills)

这是一个 360AI云盘 的技能（Skills）集合仓库，旨在为 AI 客户端（如 OpenClaw、Cursor、Claude Desktop 等）提供开箱即用的云盘操作能力。

通过这些技能，AI 助手可以直接帮助您管理 360AI云盘 中的文件，包括查询、上传、下载、分享等操作，无需手动登录网页或客户端。

## 📦 技能列表

### [360AI云盘文件管理 (360-cloud-disk)](./360-cloud-disk)

功能全面的云盘文件管理工具，提供以下能力：

*   **文件查询** — 获取文件列表、按关键词搜索文件
*   **文件管理** — 创建文件夹、移动文件、重命名文件
*   **文件传输** — 通过 URL 或文本内容保存文件到云盘、将本地文件上传到云盘
*   **资源共享** — 生成分享链接、获取下载链接
*   **账号信息** — 查询当前用户详情、空间用量等

> 👉 [查看详细文档与使用指南](./360-cloud-disk/SKILL.md)

*(后续将持续新增更多场景化技能)*

## 🚀 快速开始

### 1. 前置准备

请确保您的系统已安装 Python 3.10 或更高版本：

```bash
python3 --version
```

### 2. 获取 API 密钥

前往 [360AI云盘控制台](https://www.yunpan.com/v2/mcp) 申请您的专属 API Key。

### 3. 安装与配置

```bash
# 克隆仓库
git clone https://github.com/yifangyun/ecs-yunpan-skills.git
cd ecs-yunpan-skills

# 进入目标技能目录
cd 360-cloud-disk

# 安装依赖
pip3 install -r requirements.txt

# 配置环境变量（复制模板并填入您的 API Key）
cp .env.example .env
```

### 4. 验证安装

```bash
python3 executor.py user-info
```

如果返回了您的账户信息，说明配置成功。

### 5. 接入 AI 客户端

将以下仓库地址发送给您使用的 AI 客户端（如 OpenClaw、Cursor、Claude Desktop 等），即可由 AI 自动完成安装：

```
https://github.com/yifangyun/ecs-yunpan-skills/tree/main
```

AI 客户端会自动识别仓库中的技能文件，按照引导完成配置后即可开始使用。

---

## 🛠️ 常见问题

遇到问题时请参考对应技能目录下的故障排查文档：
- [360-cloud-disk 故障排查](./360-cloud-disk/references/troubleshooting.md)

## 📝 许可证

Apache-2.0 License.