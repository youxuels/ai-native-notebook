# 📒 AI 原生本地笔记本（AI Native Local Notebook）

> 一个把 LLM 真正"嵌进"日常记录流程的单文件 HTML 笔记本。
> 粘贴链接自动生成摘要卡片，右键选中文字自动提炼要点，输入问题回车即触发深度 /loop 讨论。
> 全本地存储，零云端依赖，支持 Markdown 双向同步到本地文件夹。

```
单文件 HTML · 无需后端 · 调用你自己的 DeepSeek API · 数据完全在你手里
```

---

## ✨ 核心特性

### 🤖 AI 原生，不是"加个 AI 按钮"
- **/loop 深度讨论**：底部输入框输入任何问题，回车即触发。AI 被约束为 1-3 句、直击本质、不绕弯子，并保留最近 6 轮上下文做连续追问
- **链接 → 摘要卡片**：复制一个网页 URL 粘进笔记，自动抓取标题/摘要/缩略图，生成可视化卡片（microlink.io + jina.ai + favicon 三级容错）
- **右键 → 摘要卡片**：选中任意文字右键，AI 把它提炼为 3 句要点，**原文字被卡片替换**，完整原文同时存档到 localStorage，可随时导出 TXT
- **卡片引用到 /loop**：右键任意卡片（URL/摘要/问答/图片）→ "引用到 /loop"，把卡片内容作为上下文继续追问

### 🎨 经典撞色卡片系统
6 种主题色（朱红 / 靛蓝 / 墨绿 / 赭黄 / 紫罗兰 / 青蓝），**相邻三张卡片颜色保证不重复**，算法自动分配。

### 📝 Word 风格编辑器
- 干净空白页面，无预制文本框
- 四类卡片：URL 卡片 / 摘要卡片 / /loop 问答卡片 / 图片卡片
- 图片可粘贴、可拖拽、可调整大小（拖动手柄 + 25%/50%/75%/100% 预设按钮）
- 所有卡片统一右键菜单：引用 / 复制 / 删除

### 📅 日期导航 + 天气标题
- 侧边栏按日期列出所有页面，每天一页
- 自动获取当天天气（Open-Meteo 免费接口），生成"日期 + 天气"标题
- 侧边栏宽度可拖动调整，宽度持久化

### 💾 本地 Markdown 双向同步
- 基于 File System Access API，绑定本地目录（建议 `D:\AI\traework\note-AI`）
- 点击右上角保存按钮或 `Ctrl/Cmd+S`，当日笔记转为 Markdown 写入 `YYYY-MM-DD.md`
- 目录绑定通过 IndexedDB 持久化，**不用每次重新绑定**
- 退出网页有未保存提醒

### 🔒 隐私优先
- 笔记数据存 localStorage，API Key 仅存本地
- 图片以 base64 嵌入，无任何第三方上传
- 唯一外部调用：DeepSeek API（你自己的 Key）+ 网页抓取代理 + 天气接口

---

## 🚀 快速开始

### 1. 打开
下载 `index.html`，用 **Chrome 或 Edge** 打开（File System Access API 仅 Chromium 支持）。

> 推荐通过本地 HTTP 服务打开，避免 `file://` 协议下浏览器对 fetch 的限制：
> ```bash
> # Python
> python -m http.server 8765
> # 然后访问 http://localhost:8765/index.html
> ```

### 2. 配置 DeepSeek API Key
- 点击右上角齿轮 → 填入 DeepSeek API Key
- 获取地址：https://platform.deepseek.com/api_keys
- 点击"测试连接"验证

### 3. 设置城市（可选）
- 在设置中输入城市名（如"南京"、"上海"）→ 保存并刷新天气

### 4. 绑定本地目录（可选，推荐）
- 设置 → 本地 Markdown 同步 → 点击"绑定本地目录"
- 选择或新建一个文件夹（如 `D:\AI\traework\note-AI`）
- 授权写入权限，目录会被记住

### 5. 开始记录
| 操作 | 效果 |
|---|---|
| 粘贴网页链接 | 自动生成 URL 摘要卡片 |
| 粘贴图片 | 生成可调整大小的图片卡片 |
| 选中文字 → 右键 → "整理为摘要卡片" | AI 提炼要点，原文存档 |
| 选中文字 → 右键 → "引用选中内容到 /loop" | 把选中内容作为 AI 上下文 |
| 右键任意卡片 | 引用 / 复制 / 打开 / 删除 |
| 底部输入框输入问题 → 回车 | 触发 /loop 深度讨论 |
| `Ctrl/Cmd + S` | 保存为 Markdown 到本地 |

---

## 🖼️ 截图与功能演示

![演示图 1](https://raw.githubusercontent.com/youxuels/ai-native-notebook/main/docs/images/1.png)

![演示图 2](https://raw.githubusercontent.com/youxuels/ai-native-notebook/main/docs/images/2.png)

![演示图 3](https://raw.githubusercontent.com/youxuels/ai-native-notebook/main/docs/images/3.png)

![演示图 4](https://raw.githubusercontent.com/youxuels/ai-native-notebook/main/docs/images/4.png)

![演示图 5](https://raw.githubusercontent.com/youxuels/ai-native-notebook/main/docs/images/5.png)

---

## 🛠️ 技术栈

- **单文件 HTML**：无构建工具，无依赖，开箱即用
- **原生 JS + contenteditable**：不依赖 React/Vue，编辑器零抽象
- **File System Access API**：本地目录读写
- **IndexedDB**：持久化目录句柄
- **DeepSeek Chat API**：LLM 推理（兼容 OpenAI 格式）
- **microlink.io / jina.ai**：网页摘要抓取
- **Open-Meteo**：免费天气接口

---

## 🎯 /loop 系统提示词

`/loop` 的行为被严格约束，避免 AI 车轱辘话：

```
你是一个经济学视角的深度对话伙伴。回答必须：
1. 1-3 句话，直击问题本质
2. 禁止铺垫、寒暄、复述问题
3. 禁止车轱辘话和套话
4. 用经济学思维框架（激励/均衡/约束/权衡）
5. 必要时用术语，但保留英文原文（如 moral hazard, adverse selection）
6. 如果问题模糊，直接给出最可能的解读并回答
```

你可以根据自己的领域修改 `LOOP_SYSTEM_PROMPT` 常量，把"经济学视角"换成任何你想要的视角。

---

## 📂 项目结构

```
ai-notebook/
├── index.html          # 全部代码（HTML + CSS + JS 单文件）
├── README.md           # 本文件
├── LICENSE             # MIT
└── .gitignore
```

笔记数据存放在浏览器 localStorage，本地 Markdown 同步目录由用户指定（默认建议 `note-AI/`，已 gitignore）。

---

## 🔧 高级用法

### 修改 /loop 提示词
在 `index.html` 中搜索 `LOOP_SYSTEM_PROMPT`，修改字符串即可。

### 修改撞色方案
搜索 `.theme-1` 到 `.theme-6`，修改对应的 hex 颜色。

### 导出全部数据
设置 → 数据管理 → 导出 JSON（包含所有页面、QA 历史、设置）。

### 导出原文存档
设置 → 数据管理 → 导出原文存档 TXT（所有右键摘要卡片的原文汇总）。

---

## ⚠️ 已知限制

- **浏览器兼容**：File System Access API 仅 Chrome/Edge 支持，Firefox/Safari 无法使用本地 Markdown 同步（其他功能正常）
- **localStorage 容量**：一般 5-10MB，大量图片会快速消耗配额，建议重要笔记及时导出 Markdown
- **目录句柄会话失效**：部分浏览器版本会话结束后读写权限失效，但目录绑定本身保留，第一次保存时会弹一次性授权
- **网页抓取依赖第三方**：microlink.io 免费 50 次/天，超额后自动降级到 favicon

---

## 🗺️ 路线图

- [ ] Markdown 双向同步（目前是单向：HTML → MD）
- [ ] 全文搜索
- [ ] 标签系统
- [ ] 卡片拖拽排序
- [ ] 导出为 PDF / EPUB
- [ ] PWA 离线支持
- [ ] 多模型切换（Claude / GPT / 本地模型）

---

## 🤝 贡献

欢迎 Issue 和 PR。这是一个追求"少即是多"的项目，请不要添加：
- 复杂的构建工具
- 重型依赖
- 云端同步
- 用户账号系统

---

## 📄 许可证

MIT License — 自由使用、修改、分发。数据和 API Key 永远属于你。

---

## 💡 灵感来源

- iA Writer 的克制
- Bear 的优雅
- Notion 的卡片化
- Obsidian 的本地优先
- tldraw 的"AI 嵌入工作流而非独立按钮"

但这个项目只想做一件事：**让 AI 真正融进你每天记笔记的动作里，而不是让你专门去"找 AI 聊天"**。

---

如果这个项目对你有帮助，欢迎 ⭐ Star。
