# 360 AI 云盘技能库 (ECS Yunpan Skills)

本仓库提供了一组 360 AI 云盘的官方技能（Skills），旨在为 AI 智能体（如 OpenClaw、Cursor、Claude Code 等）提供开箱即用的云盘操作能力。

通过为 Agent 挂载这些技能，您可以让 AI 直接管理云盘中的文件（如检索、上传、下载、分享等），极大提升工作流自动化效率。

---

## 📦 技能列表

本仓库目前提供**两套 CLI 技能**（同一套云盘能力、不同品牌与命令名）以及一套已停止维护的 MCP 技能。**新接入请优先使用 CLI 技能**，依赖更轻、支持本地文件与管道编排。

### 1. 🌟 360 AI 云盘 CLI 技能 (`360-ai-cloud-disk-cli-skill`)

基于 Node.js 命令行工具 **`360disk`** 在终端直接操作云盘，适合通用开发与自动化场景。

| 项目 | 说明 |
|---|---|
| **命令名** | `360disk` |
| **npm 包** | `@aicloud360/360-ai-cloud-disk-cli` |
| **配置目录** | `~/.360disk/` |
| **执行方式** | Shell 命令（`360disk <group> <cmd> ...`） |
| **适用场景** | Cursor、Claude Code、Windsurf、CI/CD 等 |
| **核心优势** | 支持管道、`jq`、批量与 stdin、本地文件上传下载 |

> 👉 [查看安装与使用指南](./360-ai-cloud-disk-cli-skill/README.md)

### 2. 🌟 AgentDrive CLI 技能 (`agentdrive-cli-skill`)

基于同一套云盘 CLI 能力，面向 **AgentDrive** 品牌发布；命令行工具为 **`agentdrive`**，能力与 `360disk` 一致，仅包名、二进制名与本地配置目录不同。

| 项目 | 说明 |
|---|---|
| **命令名** | `agentdrive` |
| **npm 包** | `@aicloud360/agentdrive` |
| **配置目录** | `~/.agentdrive/` |
| **执行方式** | Shell 命令（`agentdrive <group> <cmd> ...`） |
| **适用场景** | 同上，适合需要 AgentDrive 品牌与独立配置目录的场景 |
| **快速下载** | [agentdrive-cli-skill.zip](http://cn-zhengzhou-3.xstore.qihu.com/yunpan-zz2-pkg/agentdrive-cli-skill.zip) |

```bash
# 命令行下载 Skill 包（可选）
curl -O http://cn-zhengzhou-3.xstore.qihu.com/yunpan-zz2-pkg/agentdrive-cli-skill.zip
```

> 👉 [查看安装与使用指南](./agentdrive-cli-skill/README.md)

**如何选择？**

- 使用 **360disk** 品牌或已有 `~/.360disk` 配置 → 选 `360-ai-cloud-disk-cli-skill`
- 使用 **AgentDrive** 品牌或需要与 360disk 配置隔离 → 选 `agentdrive-cli-skill`

两套 Skill 的 MCP 工具能力相同，**不要混用同一套本地配置目录**（除非有意共用 `AI_CLOUD_DISK_CONFIG_DIR`）。

### 3. 🔁 AgentDrive 备份技能 (`agentdrive-backup-skill`)

面向龙虾（AI Agent）的**根目录云端备份**专用技能，基于 `agentdrive` CLI 实现一键备份 + 自动监听 + 保活 crontab。

| 项目 | 说明 |
|---|---|
| **命令名** | `agentdrive` |
| **npm 包** | `@aicloud360/agentdrive` |
| **备份路径规范** | `/<龙虾名称>/` |
| **适用场景** | 龙虾（AI Agent）把自身根目录安全备份到 AgentDrive 云端 |
| **核心能力** | 微信扫码/手机号登录 · 根目录自动识别（特征打分）· 首轮备份 · 自动监听 · crontab 保活 |

### 4. ⚠️ 360 AI 云盘 MCP 技能 (`360-ai-cloud-disk-mcp-skill`) - 【停止更新】

基于 Python 执行器（`executor.py`）调用后端 MCP Server 接口。

*   **状态说明**：**已停止更新**，建议新接入迁移至上述 CLI 技能。
*   **执行方式**：Python 脚本（`python3 executor.py <tool> ...`）
*   **适用场景**：仅作历史兼容保留。

> 👉 [查看 MCP 技能历史文档](./360-ai-cloud-disk-mcp-skill/SKILL.md)

---

## 📁 仓库目录结构

```text
ecs-yunpan-skills/
├── README.md                          # 本文件
├── 360-ai-cloud-disk-cli-skill/       # 360disk CLI Skill
├── agentdrive-cli-skill/              # agentdrive CLI Skill
└── 360-ai-cloud-disk-mcp-skill/       # MCP Skill（停止更新）
```

---

## 🔐 获取 API 密钥

所有技能最终均依赖 360 AI 云盘开放能力，请前往 [360 AI 云盘开放平台](https://www.yunpan.com/skill) 申请 API Key 用于鉴权。

## 🛠️ 反馈与支持

- 查阅 [官方文档中心](https://www.yunpan.com/skill)
- 提交 [GitHub Issue](https://github.com/yifangyun/ecs-yunpan-skills/issues)

## 📝 许可证

Apache-2.0 License.
