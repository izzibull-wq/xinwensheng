# 新闻声 XinWenSheng

> 让中文新闻被听见 — 粘贴新闻，立即用普通话朗读。
> Paste Chinese news, listen instantly in Mandarin. No voice installation needed.

![HTML5](https://img.shields.io/badge/HTML5-E34F26?style=flat-square&logo=html5&logoColor=white)
![CSS3](https://img.shields.io/badge/CSS3-1572B6?style=flat-square&logo=css3&logoColor=white)
![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?style=flat-square&logo=javascript&logoColor=black)
![No Dependencies](https://img.shields.io/badge/Dependencies-0-brightgreen?style=flat-square)
![License](https://img.shields.io/badge/License-MIT-blue?style=flat-square)
![Language](https://img.shields.io/badge/Language-中文%20(zh--CN)-red?style=flat-square)

**Demo:** 下载本仓库 → 用 VS Code + Live Server 打开 `index.html` → 点击 **朗读** 即可。

---

## ✨ 为什么叫 新闻声？

| 候选名 | 评价 |
| :--- | :--- |
| 中国新闻朗读 | 太长、太通用，像功能描述，不像品牌 |
| 中文朗读器 | 太技术化，没有新闻感 |
| **新闻声 XinWenSheng ✅** | **短、好记、有画面感 — “新闻的声音”。中文 + 拼音，GitHub / 域名 / 搜索都好用** |

- **新闻** = 专门做新闻，不是通用朗读器
- **声** = 声音、播报感，一听就知道是听新闻
- **XinWenSheng** = 拼音，方便在 GitHub、README、英文环境下引用，仓库名建议 `xinwensheng`

---

## ✨ 功能 Features

- **仅中文 (zh-CN)** — 专为中文新闻优化
- **语音已注入** — 主语音是在线普通话 (Google TTS zh-CN)，直接写在代码里，不依赖设备有没有中文语音
- **3 重朗读兜底** — ① 本地中文语音 → ② 在线注入语音 → ③ 默认语音
- **新闻示例** — 今日头条 / 国际新闻 / 经济新闻 / 体育新闻 / 社会新闻
- **选中朗读** — 选中部分文本，只读选中的部分
- **高亮跟读** — 正在读的句子高亮显示
- **语速 / 音量** — 语速 0.7x–1.3x
- **诊断日志** — 一键诊断为什么没声音
- **下载 MP3** — 中文发音，可离线播放与分享
- **深色 / 浅色模式** — 文本按语言自动保存
- **零依赖** — 纯 HTML + CSS + JS

## 🎬 快速开始 Quick Start

```bash
git clone https://github.com/<username>/xinwensheng.git
cd xinwensheng
```

1. 在 VS Code 中打开文件夹 `xinwensheng`
2. 安装扩展 **Live Server**
3. 右键 `index.html` → **Open with Live Server** / 点击右下角 **Go Live**
4. 在 **Google Chrome / Microsoft Edge** 最新版打开 `http://127.0.0.1:5500`
5. 点击 **测试注入语音** → 听到 “你好” 说明正常 → 点击 **朗读**

> ⚠️ 不要直接双击 `file://` 打开。`file://` 下下载 MP3 和在线语音可能被浏览器拦截。一定要用 Live Server。

## 📖 使用 Usage

1. 粘贴中文新闻，或点击示例 **今日头条 / 国际新闻 / 经济新闻 / 体育新闻 / 社会新闻**
2. （可选）选中一段文本，只读那一段
3. 点击 **朗读**
4. **暂停 / 继续 / 停止** 控制播放
5. 点击 **下载音频 (MP3)** 保存中文音频

## 📁 项目结构 Project Structure

```
xinwensheng/
├── index.html          # 1 个 HTML — 界面
├── css/
│   └── style.css       # 1 个 CSS — 样式
├── js/
│   └── app.js          # 1 个 JS — 逻辑 + 注入语音
└── README.md           # 本文件
```

## 🔊 语音是怎么“注入”的？

- `speechSynthesis` 的语音来自 **Windows / 浏览器**，代码只能“选择”设备上已有的语音，不能“带”一个新语音进去。
- 所以本项目把 **在线中文 TTS (Google 普通话 zh-CN)** 当作主语音，直接写在代码里：

```js
// js/app.js
const INJECTED_VOICE = { name: '在线普通话 (已注入)', lang: 'zh-CN' };
async function fetchTTSChunk(text) {
  const url = 'https://translate.googleapis.com/translate_tts?ie=UTF-8&client=tw-ob&tl=zh-CN&q=' + encodeURIComponent(text);
  const res = await fetch(url);
  return await res.blob();
}
```

- 朗读时按句切分（每段 ≤170 字）→ 逐段取音频 → 用 `Audio` 连续播放。
- 本地中文语音只当作离线备用。

## 🛠️ 技术栈

| 技术 | 用途 |
| :--- | :--- |
| HTML5 | 界面结构 |
| CSS3 | 样式 + 深色模式 |
| JavaScript (Vanilla) | 逻辑、语音、下载 |
| Web Speech API | 本地中文语音（备用） |
| Google TTS (zh-CN) | 在线注入主语音 + MP3 下载 |
| Web Audio API | 喇叭测试音 |

## 🔍 没声音？Troubleshooting

1. **不要在聊天预览 / `file://` 里测试。** 必须下载仓库，用 Chrome + Live Server 打开。
2. 点 **“🔊 先测试喇叭有没有声音”** — 如果连 “滴” 声都没有，问题在喇叭 / 音量 / 耳机。
3. 点 **“🔍 一键诊断为什么没声音”** — 看 **诊断日志**。
4. 检查音量滑块不是 0，耳机 / 蓝牙是否连错设备。
5. 在线注入语音需要联网。如果没网，会自动用本地语音。

## ✏️ 怎么改？

| 想改什么 | 改哪里 |
| :--- | :--- |
| 示例新闻 | `js/app.js` → `SAMPLES` |
| 默认语速 | `js/app.js` → `rateInput` |
| 颜色 / 排版 | `css/style.css` |
| 标题 / 品牌名 | `index.html` → `<title>` 和 `<h1>` |
| 下载文件名 | `js/app.js` → `downloadAudio()` |

## 🤝 贡献 Contributing

1. Fork 本仓库
2. 新建分支：`git checkout -b feature/xxx`
3. 提交：`git commit -m "feat: xxx"`
4. 推送并开 PR

## 📄 License

MIT License — 可自由使用、修改、商用，请保留原作者信息。

---

**新闻声 XinWenSheng** — 让每一条中文新闻，都能被听见。
