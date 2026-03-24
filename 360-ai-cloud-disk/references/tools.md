# 工具参数参考

用于理解各个 CLI 工具的调用参数。

## 目录

- [file-list](#file-list)
- [file-search](#file-search)
- [make-dir](#make-dir)
- [file-move](#file-move)
- [file-rename](#file-rename)
- [file-share](#file-share)
- [file-save](#file-save)
- [file-upload-stdio](#file-upload-stdio)
- [user-info](#user-info)
- [get-download-url](#get-download-url)

## CLI 参数传递规则

- **基本格式**：`param=value`
- **含空格的值**：`param="带 空格 的 值"`
- **数组类型**：必须用单引号包裹整个参数，并使用有效的 JSON 数组字符串，例如：`'filePaths=["/path/a.txt", "/path/b.txt"]'`

---

## file-list

获取云盘指定路径下的文件和文件夹列表，支持分页查询。返回文件名、大小、创建时间、修改时间等详细信息。

| 参数 | 类型 | 必填 | 说明 |
|------|------|------|------|
| `page` | `number` | ❌ 否 | 页码，默认从0开始。 |
| `page_size` | `number` | ❌ 否 | 每页显示的条目数，默认50条。 |
| `path` | `string` | ❌ 否 | 云盘路径，必须以/开头和结尾，如 /folder/subfolder/，根目录为 / |

```bash
python3 executor.py file-list page=1 page_size=50 path=/我的文档/
```

## file-search

在云盘中根据关键词搜索文件和文件夹，支持按文件类型筛选和分页查询。返回符合条件的文件详细信息。

| 参数 | 类型 | 必填 | 说明 |
|------|------|------|------|
| `file_category` | `number` | ❌ 否 | 文件类型筛选：-1(全部)、0(其他)、1(图片)、2(文档)、3(音乐)、4(视频) |
| `key` | `string` | ❌ 否 | 搜索关键词，当file_category 不为 -1 时，可以为空，否则必填 |
| `page` | `number` | ❌ 否 | 页码，从1开始 |
| `page_size` | `number` | ❌ 否 | 每页显示的条目数，默认20条，最大100条 |

```bash
python3 executor.py file-search file_category=-1 key=example_value page=1 page_size=20
```

## make-dir

在云盘中创建新文件夹，支持指定路径。

| 参数 | 类型 | 必填 | 说明 |
|------|------|------|------|
| `fname` | `string` | ✅ 是 | 要创建的文件夹完整路径，例如：/新文件夹/ 或 /文档/子文件夹/ |

```bash
python3 executor.py make-dir fname=文件.txt
```

## file-move

移动云盘中的文件或文件夹到指定位置。支持批量移动多个文件。

| 参数 | 类型 | 必填 | 说明 |
|------|------|------|------|
| `src_name` | `string` | ✅ 是 | 源文件或文件夹路径，多个文件用竖线(|)分隔，例如：/文件1.txt|/文件2.txt |
| `new_name` | `string` | ✅ 是 | 目标文件夹路径，例如：/目标文件夹/ |

```bash
python3 executor.py file-move src_name=文件.txt new_name=文件.txt
```

## file-rename

重命名云盘中的文件或文件夹。

| 参数 | 类型 | 必填 | 说明 |
|------|------|------|------|
| `src_name` | `string` | ✅ 是 | 原文件或文件夹的完整路径，例如：/我的知识库/111.doc 或 /我的知识库/ |
| `new_name` | `string` | ✅ 是 | 新的名称（仅文件名或文件夹名，不含父路径）。文件夹名需以/结尾，例如：222.doc 或 我的知识库/ |

```bash
python3 executor.py file-rename src_name=文件.txt new_name=文件.txt
```

## file-share

生成云盘文件的分享链接。支持批量生成多个文件的分享链接。

| 参数 | 类型 | 必填 | 说明 |
|------|------|------|------|
| `paths` | `string` | ✅ 是 | 要分享的文件全路径，多个文件用竖线(|)隔开，例如：/文件1.txt|/文件夹2/文件2.txt |

```bash
python3 executor.py file-share paths=/我的文档/
```

## file-save

通过URL或文本内容保存文件到云盘

| 参数 | 类型 | 必填 | 说明 |
|------|------|------|------|
| `url` | `string` | ❌ 否 | 文件下载地址；与 content 互斥且二选一，必须且只能传其中一个 |
| `content` | `string` | ❌ 否 | 文件内容（建议为 MD 文本）；与 url 互斥且二选一，必须且只能传其中一个；需传用户指定的完整内容，不能省略任何部分 |
| `upload_path` | `string` | ❌ 否 | 云盘存储路径，必须以 / 开头和结尾。如不指定，默认为 '/AI为我下载/YYYYMMDD/'（YYYYMMDD 为当天日期）。 |
| `file_name` | `string` | ❌ 否 | 保存到云盘的文件名，不含路径。如不填写此参数代表自动解析。 |

```bash
python3 executor.py file-save upload_path=/我的文档/
```

## file-upload-stdio

将本地文件上传到云盘指定路径。支持批量上传多个文件。

| 参数 | 类型 | 必填 | 说明 |
|------|------|------|------|
| `filePaths` | `array` | ✅ 是 | 本地文件路径数组，例如：['/本地/文件1.txt', '/本地/文件2.jpg'] |
| `uploadPath` | `string` | ❌ 否 | 云盘上传目标路径，默认为根目录'/' |

### 执行约束

- 此工具**已实现**，可直接执行，不要误判为“仅文档声明、未实现”。
- `filePaths` 必须传入**本机可访问的绝对路径**。
- 若当前使用 HTTP 模式，执行器会自动切换到 `npx` 模式处理本地文件上传。

```bash
python3 executor.py file-upload-stdio 'filePaths=["/path/to/file.txt"]' uploadPath=/我的文档/
```

## user-info

获取360AI云盘用户详细信息。

> 此工具无需任何参数

```bash
python3 executor.py user-info
```

## get-download-url

获取云盘中文件的下载链接。可以通过文件NID或路径获取。

| 参数 | 类型 | 必填 | 说明 |
|------|------|------|------|
| `nid` | `string` | ❌ 否 | 文件nid，与fpath二选一必填 |
| `fpath` | `string` | ❌ 否 | 文件路径，与nid二选一必填 |

```bash
python3 executor.py get-download-url
```
