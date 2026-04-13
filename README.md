# 360 AI 云盘技能库 (ECS Yunpan Skills)

本仓库提供了一组 360 AI 云盘的官方技能（Skills），旨在为 AI 智能体（如 OpenClaw、Cursor、Claude Code 等）提供开箱即用的云盘操作能力。

通过为 Agent 挂载这些技能，您可以让 AI 直接管理云盘中的文件（如检索、上传、下载、分享等），极大提升工作流自动化效率。

---

## 📦 技能列表

本仓库目前提供两种技术形态的云盘核心技能，请根据您所使用的 Agent 框架或应用场景选择合适的版本：

### 1. 360 AI 云盘 MCP 技能 (`360AICloudDisk-skill`)

基于 Python 执行器（`executor.py`）调用后端 MCP Server 接口。适合需要在远程环境或统一代理服务中执行网络请求的 Agent。

*   **执行方式**：Python 脚本 (`python3 executor.py <tool> ...`)
*   **适用场景**：OpenClaw 平台、Claude Desktop、Dify 等标准化 Agent 平台。
*   **核心优势**：接口稳定，自带协议隔离，支持 HTTP/Stdio 模式。
*   **配置复杂度**：中等（需要 Python 运行环境及依赖安装）。

> 👉 [查看 MCP 技能的安装与使用指南](./360AICloudDisk-skill/SKILL.md)

### 2. 360 AI 云盘 CLI 技能 (`360AICloudDiskSkill`)

基于 Node.js 命令行工具（`360disk`）直接在终端执行操作。适合在本地开发环境或支持 Shell 交互的 Agent。

*   **执行方式**：Shell 命令 (`360disk <group> <cmd> ...`)
*   **适用场景**：Cursor、Claude Code、Windsurf 等面向开发者的本地编程 Agent，或 CI/CD 自动化脚本。
*   **核心优势**：原生支持管道操作、支持复杂的本地文件上传/下载编排、依赖项更轻。
*   **配置复杂度**：低（仅需全局安装 `@aicloud360/360-ai-cloud-disk-cli`）。

> 👉 [查看 CLI 技能的安装与使用指南](./360AICloudDiskSkill/README.md)

*(后续将持续新增更多针对具体业务流的场景化技能)*

---

## 🚀 智能体自动化安装说明

如果您的 Agent 能够自动从 GitHub 拉取代码并挂载技能，请引导它执行以下操作以获取所需的技能包。

### 克隆整个技能库

首先将本仓库克隆到 Agent 本地的配置目录中：

```bash
git clone https://github.com/yifangyun/ecs-yunpan-skills.git
```

### 加载目标技能上下文

根据 Agent 的类型，进入对应的技能子目录（如 `360AICloudDisk-skill/` 或 `360AICloudDiskSkill/`），并让 Agent 完整读取目录内的 `SKILL.md`。

`SKILL.md` 包含了该技能的详细依赖准备说明、鉴权配置指南以及所有的工具能力提示词，这是 Agent 能正确运作的基础。

---

## 🔐 获取 API 密钥

所有的技能包调用最终均依赖于 360 AI 云盘的开放能力，请前往 [360 AI 云盘开放平台](https://open.yunpan.360.cn) 申请您的专属 API Key 以进行鉴权。

## 🛠️ 反馈与支持

遇到问题时请优先参考所选技能子目录中的参考文档（位于 `references/` 目录）。
如有更多问题，欢迎：
- 查阅 [官方文档中心](https://open.yunpan.360.cn)
- 提交 [GitHub Issue](https://github.com/yifangyun/ecs-yunpan-skills/issues)

## 📝 许可证

Apache-2.0 License.