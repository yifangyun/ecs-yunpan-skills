# 360 AI 云盘技能库 (ECS Yunpan Skills)

本仓库提供了一组 360 AI 云盘的官方技能（Skills），旨在为 AI 智能体（如 OpenClaw、Cursor、Claude Code 等）提供开箱即用的云盘操作能力。

通过为 Agent 挂载这些技能，您可以让 AI 直接管理云盘中的文件（如检索、上传、下载、分享等），极大提升工作流自动化效率。

---

## 📦 技能列表

本仓库目前提供两种技术形态的云盘核心技能。**强烈推荐使用 CLI 技能**，它拥有更轻量的依赖和更强大的本地文件处理能力。

### 1. 🌟 360 AI 云盘 CLI 技能 (`360-ai-cloud-disk-cli-skill`) - 【推荐使用】

基于 Node.js 命令行工具（`360disk`）直接在终端执行操作。适合在本地开发环境或支持 Shell 交互的 Agent。

*   **执行方式**：Shell 命令 (`360disk <group> <cmd> ...`)
*   **适用场景**：Cursor、Claude Code、Windsurf 等面向开发者的本地编程 Agent，或 CI/CD 自动化脚本。
*   **核心优势**：原生支持管道操作、支持复杂的本地文件上传/下载编排、依赖项更轻。
*   **配置复杂度**：低（支持 `npx @aicloud360/360-ai-cloud-disk-cli` 免安装运行，或全局安装）。

> 👉 [查看 CLI 技能的安装与使用指南](./360-ai-cloud-disk-cli-skill/README.md)

### 2. ⚠️ 360 AI 云盘 MCP 技能 (`360-ai-cloud-disk-mcp-skill`) - 【停止更新】

基于 Python 执行器（`executor.py`）调用后端 MCP Server 接口。

*   **状态说明**：**该技能已停止更新，后续不再维护新功能。** 建议所有新接入的 Agent 迁移至上述的 CLI 技能。
*   **执行方式**：Python 脚本 (`python3 executor.py <tool> ...`)
*   **适用场景**：仅作为历史遗留系统的兼容保留。

> 👉 [查看 MCP 技能的历史文档](./360-ai-cloud-disk-mcp-skill/SKILL.md)

---

## 🔐 获取 API 密钥

所有的技能包调用最终均依赖于 360 AI 云盘的开放能力，请前往 [360 AI 云盘开放平台](https://www.yunpan.com/skill) 申请您的专属 API Key 以进行鉴权。

## 🛠️ 反馈与支持

- 查阅 [官方文档中心](https://www.yunpan.com/skill)
- 提交 [GitHub Issue](https://github.com/yifangyun/ecs-yunpan-skills/issues)

## 📝 许可证

Apache-2.0 License.