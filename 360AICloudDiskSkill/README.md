# 360 AI 云盘 Skill (360AICloudDiskSkill)

## 概述

`360AICloudDiskSkill` 是一个为 AI Agent 打造的“云盘感知与操作”技能包。它基于 `@aicloud360/360-ai-cloud-disk-cli` 命令行工具构建，定义了一系列清晰的 `bash` 命令模板。

引入该 Skill 后，你的智能体即可通过执行系统命令的方式，直接访问和管理 360 AI 云盘中的文件。

## ⚠️ 核心依赖

**注意：此 Skill 的正常工作强依赖于宿主机环境中安装的 `@aicloud360/360-ai-cloud-disk-cli` 命令行工具。**

在将此 Skill 赋予你的 Agent 之前，请务必在运行 Agent 的环境中执行以下操作：

### 1. 全局安装 CLI
```bash
npm install -g @aicloud360/360-ai-cloud-disk-cli
```

### 2. 配置鉴权凭证
```bash
360disk auth login --api-key <YOUR_360_AI_CLOUD_DISK_API_KEY>
```
*API_KEY 可在 [360 AI 云盘 Web 端开发者中心](https://open.yunpan.360.cn) 获取。*

### 💡 替代方案：使用 npx 零安装接入

如果你不想全局安装，或者在 CI/CD、临时容器等环境中，可以直接使用 `npx` 方式调用（需确保网络畅通）。

在 Agent 的环境变量或启动脚本中，配置统一的执行前缀：
```bash
export DISK_360_CLI='npx -y -p @aicloud360/360-ai-cloud-disk-cli@latest 360disk'

# 登录鉴权
$DISK_360_CLI auth login --api-key <YOUR_360_AI_CLOUD_DISK_API_KEY>

# 执行命令
$DISK_360_CLI dir ls /
```

## 集成方式

该 Skill 可直接挂载至任何支持以 `bash` 命令形式执行外部程序的智能体框架（如 Claude Code, OpenClaw, OpenCode, Cursor 等）。

Agent 在调用云盘功能时，并不是发起复杂的 HTTP 或 MCP 协议请求，而是直接拼接并执行形如 `360disk dir ls /` 的终端命令，并解析命令返回的结构化 JSON 结果。这种方式极大地**节省了 Token** 并降低了 Agent 编排的理解难度。

详细的 Agent 提示词配置和工具使用示例，请参阅本目录下的 [`SKILL.md`](SKILL.md) 与 `references/` 目录。

## 能力概览

通过本 Skill，Agent 将获得以下 5 大类的核心云盘能力（对应底层 CLI 命令）：

- **身份鉴权与配额（`auth`, `user`）**
  - **登录授权**：`360disk auth login --api-key <key>`（首次使用或 Token 过期时调用）
  - **状态查询**：`360disk auth whoami`
  - **配额查看**：`360disk user info`（获取云盘总容量和已用容量）
- **目录生命周期（`dir`）**
  - **目录列表**：`360disk dir ls <path>`（支持 `-r` 递归）
  - **创建目录**：`360disk dir mkdir <path>`（支持 `-p` 递归创建）
- **文件流转与状态（`file`）**
  - **检索与查询**：`360disk file search <keyword>`（全局搜索）、`360disk file node-info`、`360disk file origin-size`
  - **移动与重命名**：`360disk file mv <src> <dest>`、`360disk file rename <path> <newName>`
  - **复制与转存**：`360disk file trans-copy <src> <dest>`
  - **删除与清空**：`360disk file rm <path>`、`360disk file clear-dir <dir>`
  - **同名冲突检测**：`360disk file exists <dir> <name>`
- **云盘专属功能（`file`）**
  - **分享链接生成**：`360disk file share <path>`（生成带提取码的分享链接）
  - **保存他人分享**：`360disk file save <shareUrl>`（支持密码提取并存入自己云盘）
  - **直链获取**：`360disk file url <path_or_nid>`（获取带时效的防盗链下载直链）
  - **文本追加**：`360disk file append <path>`（向云盘文本文件末尾追加内容）
- **数据传输与配置（`file`）**
  - **文件上传**：`360disk file upload <local> <remote>`（将本地文件/目录传至云盘）
  - **文件下载**：`360disk file download <remote> <local>`（将云盘文件/目录拉取到本地执行环境）
  - **配置文件读写**：`360disk file config`（直接读取和修改云端 JSON/YAML/INI 配置）

## 反馈与支持

- **在线开发文档**: [360 AI 云盘开放平台文档](https://open.yunpan.360.cn)
- **提交问题**: 如遇 CLI 执行或 Skill 配置问题，请访问 [GitHub 仓库提交 Issue](https://github.com/yifangyun/ecs-yunpan-skills/issues)。