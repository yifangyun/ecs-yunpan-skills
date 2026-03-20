---
name: 360-ai-cloud-disk
description: "360 AI 云盘文件管理和助手工具。提供对 360 AI 云盘的全面操作能力，包括文件/文件夹的列表查看、内容搜索、分享文件、上传下载、文件重命名、移动文件、创建文件夹等功能。支持与云盘进行快速的文件交互与管理。"
---

# 360 AI Cloud Disk

**重要指令：** 根据用户意图，**直接选择合适的工具执行，绝对不要先列出所有可用功能让用户选择。**

## 执行约束

- 映射表中的**所有工具均已实现**，可直接通过 `executor.py` 调用。
- `executor.py` 采用通用调度架构，不需要为每个工具单独编写分支代码。

## 工具调用方式

```bash
python3 executor.py <tool-name> [param1=value1] [param2=value2]
```

## 意图与工具映射表

请严格按照下表，将用户的意图映射到对应的工具名称上，并直接执行：

| 用户意图 | 对应工具 |
|---|---|
| 查看/浏览云盘目录、列出文件 | `file-list` |
| 按关键词搜索文件 | `file-search` |
| 上传本地文件到云盘 | `file-upload-stdio` |
| 创建新文件夹 | `make-dir` |
| 移动文件或文件夹 | `file-move` |
| 重命名文件或文件夹 | `file-rename` |
| 生成文件分享链接 | `file-share` |
| 查看当前用户信息 | `user-info` |
| 保存 URL 或文本内容到云盘 | `file-save` |
| 获取文件下载链接 | `get-download-url` |

**详细的工具参数说明，请按需查阅 [references/tools.md](references/tools.md)。**

## 全局规则：路径规范

- 任何文件路径**必须**以 `/` 开头（如 `/文档/test.txt`）
- 任何文件夹路径**必须**以 `/` 结尾（如 `/文档/`）
- 若需批量操作多个文件，请用 `|` 将它们分隔（如 `/file1.txt|/file2.txt`）
