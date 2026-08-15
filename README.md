# rvc-for-tts

**私有仓库**：存放 dsh-plugin-tts 用的 RVC 音色包（模型 + 紧凑索引 + `manifest.json`）。
供本人跨机器同步使用，**不要改为公开**（音色受版权限制，仅限个人使用）。

## 使用（dsh-plugin-tts）

1. 打开 dsh-plugin-tts 设置 → 插件 → 语音 → 「音色包」；
2. 仓库地址填：`https://raw.githubusercontent.com/1624318455/rvc-for-tts/main`；
3. 「获取列表」→ 看到 azusa-test 包 → 选索引版本（2k / 10k / 20k）→ 「下载并启用」。

> 注意：私有仓库的 raw 下载需要登录态。若插件无法直连私有 raw，
> 可 `git clone` 到本机后用 `node tests/mock-registry.mjs <目录> 8899` 起本地仓库，
> 地址填 `http://127.0.0.1:8899`。

## 结构

```
rvc-for-tts/
├── manifest.json          # 音色包清单（插件「音色包」模块读取）
└── packs/
    └── azusa-test/
        ├── model.pth                       # 模型（52.7MB）
        ├── azusa-test_..._compact_2000.index   # 紧凑索引 2k（5.9MB，最省）
        ├── azusa-test_..._compact_10000.index  # 紧凑索引 10k（29.3MB，推荐）
        └── azusa-test_..._compact_20000.index  # 紧凑索引 20k（58.6MB，最还原）
```

- 完整索引（408MB）**不放在仓库**（GitHub 单文件上限 100MB），需用时从本机
  `assets/indices/` 取，或自行用「压缩索引」生成。
- 免索引 = 音色包里不填索引（设置里「索引路径」留空即可）。

## 如何新增音色

1. 建 `packs/<id>/`，放入 `model.pth` + 索引（建议用「压缩索引」生成紧凑版）；
2. 在 `manifest.json` 的 `packs` 数组加一项（url 用相对路径）；
3. `Get-FileHash 文件 -Algorithm SHA256` 填 `size` 与 `sha256`；
4. 提交推送。

## 版权提醒

- azusa-test 音色受版权限制：**仅限个人本地使用，禁止公开分发**；
- 若要对外分享音色，只发布你拥有版权或已获授权的声音。
