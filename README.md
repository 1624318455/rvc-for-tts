# rvc-for-tts

dsh-plugin-tts 的**公开音色包仓库**（模型 + 索引 + `manifest.json`）。
插件「音色包」模块直接读取本仓库的 `manifest.json` 实现一键下载安装。

## 使用（dsh-plugin-tts）

1. 打开 dsh-plugin-tts 设置 → 插件 → 语音 → 「音色包」；
2. 仓库地址填：`https://raw.githubusercontent.com/1624318455/rvc-for-tts/main`；
3. 「获取列表」→ 看到音色包列表 → 点「下载并启用」，自动校验 sha256 并填入模型/索引。

## 结构

```
rvc-for-tts/
├── manifest.json          # 音色包清单（插件「音色包」模块读取）
└── packs/
    ├── guanguanV1/        # 模型 model.pth + guanguanV1.index
    └── keruanV1/          # 模型 model.pth + keruanV1.index
```

- url 均为相对路径，插件按仓库地址自动解析；
- 每个包都带 sha256 校验值，下载时自动核对。

## 如何新增音色

1. 建 `packs/<id>/`，放入 `model.pth` + 索引（超过 GitHub 100MB 单文件上限时，
   先用插件的「压缩索引」生成紧凑版）；
2. 在 `manifest.json` 的 `packs` 数组加一项（url 用相对路径）；
3. `Get-FileHash 文件 -Algorithm SHA256` 填 `size` 与 `sha256`；
4. 提交推送。

## 版权

- 本仓库只收录**有权分发**的音色（作者自有或已获授权）；
- 曾经的演示音色 azusa-test 受版权限制已移除，不在此仓库。
