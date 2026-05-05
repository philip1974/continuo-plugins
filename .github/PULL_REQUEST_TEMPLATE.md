<!-- 上架新 plugin 的 PR,按下面填。如果是改已有 entry,只填变更部分。 -->

## Plugin 信息

- **Repo**:https://github.com/your-handle/your-plugin-repo
- **当前版本**:v0.1.0
- **manifest.id**:com.your.plugin
- **声明权限**(permissions):无 / fs / network / clipboard / shell

## 这个 plugin 做什么

<!-- 1-2 句话描述核心用途。avoid 营销话,用例就好。 -->

## 截图(可选但加分)

<!-- plugin 在 Continuo 里跑起来的样子 -->

## 自测确认

- [ ] 在最新 Continuo dev 上 `installFromGit(my-repo-url)` 装上能 enable
- [ ] 核心命令跑过、不抛错
- [ ] 声明的权限 try/catch PermissionError(若有)
- [ ] 未在 plugin 里访问 `window.api.*` / 直接 `globalThis.fetch`
- [ ] 同意 review feedback,长期维护

## 其它

<!-- 任何 reviewer 应该知道的事:依赖 / 已知限制 / 后续计划 -->
