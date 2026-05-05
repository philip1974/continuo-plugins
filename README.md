# Continuo Plugins Index

Continuo 桌面 app 的插件商店索引仓库。

> 在 Continuo 内打开 Settings → 插件商店 即可浏览全部插件。

## 上架流程

1. **写好你的插件**(参考 [examples/sample-plugin](https://github.com/philip1974/continuo-sample-plugin))
2. **推到自己 GitHub repo**(public,含 `manifest.json` + `main.js`)
3. **fork 本仓库**,在 `index.json` 数组末尾追加一条
4. **提 PR**,使用 PR 模板填好基本信息

我们会:
- review 代码 + 跑 install 烟测
- 通过 → 合并 + 视情况标 `verified: true`
- 有问题 → comment 反馈

## index.json schema

```json
{
  "id": "com.your.plugin",
  "name": "Your Plugin",
  "description": "一句话简介",
  "author": "your-handle",
  "authorUrl": "https://github.com/your-handle",
  "repo": "your-handle/your-plugin-repo",
  "branch": "main",
  "tags": ["productivity"]
}
```

| 字段 | 必填 | 说明 |
|---|---|---|
| `id` | ✓ | 反 DNS 唯一,**与 plugin manifest.id 一致** |
| `name` | ✓ | 显示名 |
| `description` | | 一句话 |
| `author` | ✓ | 作者 handle |
| `authorUrl` | | 作者主页(GitHub / 个人站) |
| `repo` | ✓ | `owner/name` 格式 |
| `branch` | | 默认 `main` |
| `tags` | | 自由字符串数组(`productivity` / `theme` / `dev-tools` 等) |
| `verified` | | **不要自填**,review 后由维护者加 |

`version` **不在此处** — Continuo 会拉你 plugin repo 的 manifest.json 取真实版本。每次 release,bump 你 manifest.json 的 `version`,push,Continuo 自动检测到更新。

## 写 Continuo 插件

参考文档:
- 项目仓库 `doc/12-plugin-permissions.md` — 权限系统(plugin 需要的 fs/network 等必走 `app.*` API)
- `examples/sample-plugin/main.js` — 完整 9 贡献点 + 权限 demo
- `globalThis.co` 暴露 `Plugin` 基类 + `React` + `PermissionError`

最小骨架:

```js
const { Plugin } = globalThis.co;

export default class MyPlugin extends Plugin {
  async onload() {
    this.addCommand({
      id: 'my.hello',
      title: 'Hello from My Plugin',
      fn: () => alert('Hi!'),
    });
  }
}
```

## 行为准则

- 不在 plugin 里调 `window.api.*` / `globalThis.fetch` 等 raw API,只走 `this.app.fs/network/clipboard`(权限门 + sandbox 一致性)
- manifest 声明的 `permissions` 真实反映用途;不为占便宜全勾
- 不在 plugin 里暴露用户私密数据到外部 API(用户授了 network 不等于授了 telemetry)
- review 通过后保持 plugin repo 维护;长期失修可能被取消 verified 标记

## 评价插件

商店里的 plugin 卡片都显示星级 + 评价数。任何人都能写评价:

1. 进 [Discussions tab](https://github.com/philip1974/continuo-plugins/discussions)
2. 点 **New discussion** → 选 General(模板会自动应用)
3. 按表单填:
   - **Plugin ID** — 你评价的 plugin manifest.id(如 `com.example.sample`)
   - **评分** — 1-5 星
   - **评论正文** — 用了多久 / 解决了什么 / 不足
   - 可选 Continuo / plugin 版本
4. 提交,Continuo app 1 小时内拉到并展示

**评价显示规则**:
- 标题需含 `[plugin-id]`,Continuo 据此聚合
- 评分按 1-5 算术平均(不加权 / 不去极端)
- "👍" 反应数 → 排序"最有用"参考
- 维护者(philip1974)显蓝色 🛡 角标
- GitHub 注册 < 7 天的账号显黄色 ⚠ 角标(慎信)

**别这样**:
- 跟 plugin 作者吵 → 直接到他 plugin repo 提 issue 沟通
- 灌水 / 无内容 → 维护者会删
- 同一作者多账号刷好评 → 维护者会撤 verified 标记

## 反馈

bug / 建议 → 提 issue。

不熟悉 GitHub PR 流程 → 也可以提 issue 把你的 plugin repo URL + 上面 schema 字段贴出来,我们帮你加。
