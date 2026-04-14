# 360 AI 云盘 CLI Skill 安装指南

本 README 供智能体（AI Agent）或自动化脚本快速读取，用于自动下载并安装 `360-ai-cloud-disk-cli-skill`。

## 什么是 360-ai-cloud-disk-cli-skill？

`360-ai-cloud-disk-cli-skill` 是一个云盘操作技能包。Agent 安装并加载它后，可以通过执行本地命令行工具来直接管理 360 AI 云盘中的文件。详细的工具依赖、鉴权配置和使用说明均已定义在同目录的 [`SKILL.md`](SKILL.md) 中。

## 如何自动化安装

由于该 Skill 托管在 `ecs-yunpan-skills` 仓库中（该仓库可能包含多个不同的 Skill），你需要将此仓库克隆或下载到本地，并提取出 `360-ai-cloud-disk-cli-skill` 子目录。

### 自动化安装命令示例（供 Agent 执行）：

```bash
# 1. 创建你的 skills 存放目录（以 .skills 为例）
mkdir -p .skills

# 2. 将包含该 skill 的仓库拉取到本地
git clone https://github.com/yifangyun/ecs-yunpan-skills.git .skills/ecs-yunpan-skills

# 3. 将 360-ai-cloud-disk-cli-skill 移动到你的主 skills 目录，并清理无用文件
mv .skills/ecs-yunpan-skills/360-ai-cloud-disk-cli-skill .skills/
rm -rf .skills/ecs-yunpan-skills
```

执行完毕后，你的本地结构应当如下：
```text
.skills/
└── 360-ai-cloud-disk-cli-skill/
    ├── SKILL.md
    ├── README.md
    └── references/
        └── commands.md
```

## 智能体加载与配置

安装到本地后，Agent 必须读取并加载 `.skills/360-ai-cloud-disk-cli-skill/SKILL.md` 的内容到自己的上下文中。

- 相关的依赖（如全局安装 `@aicloud360/360-ai-cloud-disk-cli`）和 API 鉴权配置步骤，**都记录在 `SKILL.md` 内的“前提条件与要求”章节中**，Agent 需自行读取 `SKILL.md` 并执行相应的依赖准备命令。
- `SKILL.md` 是 Agent 理解和使用云盘功能的核心提示词来源。

> **安装校验测试**：向 Agent 发送 `"请加载 360-ai-cloud-disk-cli-skill，然后帮我列出云盘根目录下的文件"`，若 Agent 能成功解析 `SKILL.md` 并执行 `360disk dir ls /`，即表示安装和配置成功。