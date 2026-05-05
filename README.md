# Continuo Plugins Index

Continuo 插件商店的索引仓库。

## 上架流程

1. fork 本仓库
2. 编辑 `index.json`,在数组末尾加一条:
   ```json
   {
     "id": "com.your.plugin",
     "name": "Your Plugin",
     "description": "...",
     "author": "your-handle",
     "authorUrl": "https://github.com/your-handle",
     "repo": "your-handle/your-plugin-repo",
     "branch": "main",
     "tags": ["productivity"]
   }
   ```
3. 提 PR

review 后合并;通过的会标 `"verified": true`。

## 字段说明

| 字段 | 必填 | 说明 |
|---|---|---|
| `id` | ✓ | 反 DNS 唯一 id,与 plugin manifest.id 一致 |
| `name` | ✓ | 显示名 |
| `description` | | 一句话简介 |
| `author` | ✓ | 作者 handle |
| `authorUrl` | | 作者主页 |
| `repo` | ✓ | `owner/name` 格式,plugin 源码 GitHub repo |
| `branch` | | 默认 `main` |
| `tags` | | 自由字符串数组 |
| `verified` | | 官方 review 过 → true,缺省 = 社区贡献 |

`version` 不在此处 — 由 plugin 自家 manifest.json 当源,Continuo 拉取时取真实版本。
