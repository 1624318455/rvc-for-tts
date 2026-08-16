# rvc-for-tts

dsh-plugin-tts 的**公开音色包仓库**（模型 + 索引 + `manifest.json`）。
插件「音色包」模块直接读取本仓库的 `manifest.json` 实现一键下载安装。

- **音色包网页列表**：https://1624318455.github.io/rvc-for-tts/（GitHub Pages，读 `manifest.json` 渲染）

## 使用（dsh-plugin-tts）

1. 打开 dsh-plugin-tts 设置 → 插件 → 语音 → 「音色包」；
2. 仓库地址填：`https://raw.githubusercontent.com/1624318455/rvc-for-tts/main`；
3. 「获取列表」→ 看到音色包列表 → 点「下载并启用」，自动校验 sha256 并填入模型/索引。

## 结构

```
rvc-for-tts/
├── index.html             # GitHub Pages 音色展示页
├── manifest.json          # 音色包清单（插件「音色包」模块读取）
├── tools/make-pack.mjs    # 一键新增音色脚本（无依赖）
└── packs/
    ├── guanguanV1/        # 模型 guanguanV1.pth + guanguanV1.index
    └── keruanV1/          # 模型 keruanV1.pth + keruanV1.index
```

- url 均为相对路径，插件按仓库地址自动解析；
- 每个包都带 sha256 校验值，下载时自动核对。

## 如何新增音色（一键）

把要上传的音色文件（一个 `.pth` 模型 + 若干 `.index` 索引）放进一个文件夹，然后：

```powershell
node tools/make-pack.mjs --id guanguanV2 --name "关关 V2" `
  --dir D:\incoming\guanguanV2 --repo . `
  --desc "一句话介绍" --author 你 --license author-owned
```

脚本会：扫描文件夹 → 复制到 `packs/<id>/` → 计算 size/sha256 → 合并进 `manifest.json`
（多个 `.index` 自动成为可选索引变体）。然后按提示 `git add/commit/push` 即可。

校验仓库完整性：

```powershell
node tools/make-pack.mjs --check --repo .
```

> 脚本同样位于插件仓库 `tools/make-pack.mjs`（含测试）。索引超过 GitHub 100MB 单文件上限时，
> 先用插件的「压缩索引」生成紧凑版再上传。

## 版权

- 本仓库只收录**有权分发**的音色（作者自有或已获授权）；
- 曾经的演示音色 azusa-test 受版权限制已移除，不在此仓库。
