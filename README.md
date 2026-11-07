# 🎵 Gamma Pulse: 40Hz调幅音乐

**Gamma Pulse** 是一个纯前端、单文件的 40Hz 振幅调制（Amplitude Modulation）音乐制作工具。你从本机选歌，它在浏览器里实时生成 40Hz 调幅版本，可试听、存入本机歌库、导出 WAV，全程不上传任何数据。

> 🔬 背景小知识：MIT 蔡立慧（Li-Huei Tsai）实验室 2016 年发表于 *Nature* 的小鼠实验显示，40Hz 光/声刺激可诱发大脑伽马振荡、降低 Aβ 水平、激活小胶质细胞（详见文末参考文献）。本工具把 40Hz 调幅作为一种音频制作参数呈现，仅供专注 / 放松 / 娱乐使用，**不构成医疗建议**。

## 🔗 链接

- **在线使用（手机浏览器打开体验最佳）**：https://40hz-am-studio.app.workbuddy.host/?sharecode=AZPGUTR6SW
- **GitHub**：https://github.com/jingmei/gamma-pulse-40hz
- **Gitee（国内访问快）**：https://gitee.com/respectfully-mei/gamma-pulse-40hz

## ✨ 功能

- **本地处理**：选歌 → 实时 40Hz 调制 → 试听 → 导出 WAV / 存入歌库，全程在浏览器完成，无服务器、无上传、无登录
- **场景一键设定**：🎯 专注工作（28%）／📖 深度阅读（24%）／🧘 瑜伽冥想（35%）／🚗 长途驾驶提神（45%），统一 40Hz、深度不同，点卡片即用
- **本机歌库**：保存的歌存在浏览器 IndexedDB 里（默认上限 20 首，刷新后仍在；也可选"不限数量，仅本次页面"），支持试听、连播、删除、清空
- **参数可调**：调制频率 1–100Hz、调制深度 5–60%，随时拖动即时重新生成
- **多选批量导入**：一次勾选多首歌自动依次入库；平台限制单选时也不出错
- **导出与分享**：导出 WAV 存到手机/电脑；支持 Web Share API 的浏览器可一键调起系统分享面板
- **手机适配**：微信 / 必应等应用内浏览器自动隐藏不可用的按钮并给出替代路径；夸克等浏览器只保留实测可用的功能
- **单文件部署**：核心就是一个 `index.html`（约 44KB，无外部依赖），任何静态托管都能跑

## 🚀 快速开始

无需构建、无需安装依赖：

```bash
# 方式一：直接用浏览器打开（推荐先跑起来看看）
open index.html          # macOS
start index.html         # Windows

# 方式二：起个静态服务（体验完整功能，如 PWA / 分享）
npx serve .
# 或
python -m http.server 8080
```

在手机浏览器打开体验最佳（建议耳机、中低音量）。

## 🧩 技术实现（单文件内）

- **Web Audio API**：解码音频 → `modulateBuffer()` 用 40Hz 正弦包络做逐样本振幅调制 → 离线渲染
- **波形可视化**：Canvas 逐段绘制 + 播放进度高亮
- **IndexedDB 歌库**：`libAll / libDel / trimLibrary` 等，容量模式可切换
- **平台适配层**：UA 检测（微信 / 夸克 / 必应 / 桌面），按环境隐藏不可用按钮并降级提示
- **Web Share API**：`navigator.share` 分享生成的 WAV 文件，失败自动降级为下载
- **PWA**：`manifest.json` + 图标，可添加到手机主屏幕

## 📁 目录结构

```
.
├── index.html        # 全部核心代码（HTML + CSS + JS 单文件）
├── manifest.json     # PWA 清单
├── icon-192.png      # PWA 图标
├── icon-512.png      # PWA 图标（maskable）
└── share/
    └── index.html    # 分享落地页
```

## 🔬 参考文献

1. Iaccarino HF, Singer AC, Martorell AJ, Rudenko A, Gao F, Gillingham TZ, …, Tsai LH. **Gamma frequency entrainment attenuates amyloid load and modifies microglia.** *Nature*, 540(7632): 230–235, 2016.（MIT 蔡立慧实验室：40Hz 光/声刺激诱发伽马振荡，降低 Aβ、激活小胶质细胞）
   https://pubmed.ncbi.nlm.nih.gov/27929004/
2. MIT News (2016-12-07). *Unique visual stimulation may be new treatment for Alzheimer's.*
   https://news.mit.edu/2016/visual-stimulation-treatment-alzheimer-1207

> 说明：以上多为动物实验与机制研究，40Hz 声刺激对人的长期效果仍在临床验证中。本工具仅把 40Hz 调幅作为音频制作参数呈现，不代表任何疗效承诺。

## ⚠️ 免责说明

- 本项目是一款**个人音频制作与播放工具**，仅供专注、放松、学习与日常娱乐使用；**不构成医疗建议**，不用于诊断、治疗、缓解或预防任何疾病，请勿以此替代正规诊疗。
- 40Hz 相关研究的多数证据来自**动物实验与早期临床研究**；对人的长期效果尚未确定，请理性看待。
- 如你正在接受治疗，或患有**癫痫、光敏性疾病**，或佩戴心脏起搏器等植入设备，或处于孕期，请先咨询医生再使用。
- 使用中若出现**头晕、头痛、耳鸣加重、恶心、心慌或任何不适，请立即停止使用**并休息；症状持续请及时就医。
- 「长途驾驶提神」场景**仅建议在停车休息时收听**；驾驶或操作机械时请勿佩戴耳机收听。
- 请使用**中低音量**，连续收听不宜过长，注意保护听力。

## 🔒 隐私

不上传、不采集、不统计。你的歌曲和歌库只存在于你自己的设备浏览器中。

## 📄 许可证

[MIT License](LICENSE)
