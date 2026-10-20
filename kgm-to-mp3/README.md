# 加密音频 → MP3 转换网页

基于开源 **Unlock Music** 的浏览器本地解密方案（WASM），支持批量转换酷狗等平台的加密音频。

## 功能

- 批量上传 / 拖拽 `.kgm` `.kgma` `.kgg` `.vpr` 等加密文件
- 同时兼容：QMC 系（`.qmcflac` `.qmcogg` `.mflac` `.mgg` `.bkcmp3` `.tkm`…）、网易云 `.ncm`、酷我 `.kwm`
- 在**浏览器本地**解密（不上传服务器）
- 结果展示在上传区下方：可试听、可下载
- 解密结果若不是 MP3（如 FLAC/OGG），可自动用 ffmpeg.wasm 转成 MP3
- 支持一键打包下载全部 MP3（ZIP）

## 目录结构

```
kgm-to-mp3/
├── index.html          # 主页面（UI + 转换逻辑）
├── js/
│   ├── KgmWasmBundle.js   # Unlock Music KGM 解密 WASM（已本地化）
│   └── QmcWasmBundle.js   # Unlock Music QMC 解密 WASM（已本地化）
└── README.md
```

## 如何运行（推荐 VS Code + Live Server）

1. 用 **Visual Studio Code** 打开文件夹 `kgm-to-mp3`
2. 安装扩展 **Live Server**（作者：Ritwick Dey）
3. 打开 `index.html` → 右键 → **Open with Live Server**
   - 或点击 VS Code 右下角 **Go Live**
4. 浏览器打开类似地址：`http://127.0.0.1:5500/index.html`

> **请勿**直接双击用 `file://` 打开：部分 CDN / ES Module / WASM 加载在本地文件协议下会被浏览器拦截。

## 使用说明

1. 点击上传区或拖入多个加密音频
2. 等待每个文件状态变为「✓ 完成」
3. 在列表中试听，或点「下载」保存单曲
4. 需要全部导出时点「打包下载全部 MP3」

### 转 MP3 选项

- 勾选「非 MP3 自动转 MP3」：解密后若为 FLAC/OGG 等，会再用 ffmpeg 转成 MP3
- 首次转码需从 CDN 加载 ffmpeg 核心（约 30MB），请保持网络畅通
- 多数酷狗 `.kgm/.kgma` 解密后本身就是 MP3，无需转码

## 开源依赖

| 组件 | 用途 | 来源 |
|------|------|------|
| @xhacker/kgmwasm | 酷狗 KGM/KGMA 解密 | npm / Unlock Music 生态 |
| @xhacker/qmcwasm | QQ 音乐 QMC v2 解密 | npm / Unlock Music 生态 |
| @clamber_l/crypto | NCM / QMC1 等通用解密 | npm（Unlock Music crypto 继承） |
| @ffmpeg/ffmpeg | 转 MP3 | jsDelivr CDN |
| JSZip | 批量打包 | jsDelivr CDN |

源码参考：[um/web（Unlock Music Web）](https://git.um-react.app/um/web)

## 免责声明

本工具仅用于**个人已购买内容**在自有设备上的播放兼容。请保持音乐平台会员有效；请勿将解锁文件二次分发。使用前请确认符合当地法律法规。
