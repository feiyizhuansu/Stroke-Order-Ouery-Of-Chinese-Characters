基于 React Native (Expo) 构建的汉字笔顺查询应用，依据《通用规范汉字笔顺规范》(GF 0023－2020)，收录 9574 个汉字的完整笔顺数据，支持逐笔动画演示和语音播报。

## 功能特性

- **汉字笔顺查询** — 输入任意汉字，查询其标准笔顺写法，数据依据国家语委规范 GF 0023－2020
- **田字格笔顺动画** — 标准田字格展示，不同颜色区分笔画，逐笔动画演示书写过程，标注书写序号
- **五种基本笔形** — 清晰区分横（一）、竖（丨）、撇（丿）、点（丶）、折（乛）五种基本笔形
- **汉字属性信息** — 提供偏旁部首、音序、注音（多音字列出全部读音）、释义等多种属性
- **组词参考** — 展示汉字常用组词，帮助理解汉字在词语中的用法
- **笔顺同步朗读** — 播放动画时同步朗读笔画名称（"第一笔，横；第二笔，竖..."），支持语音播报
- **手势操作** — 支持左右滑动返回，替代传统返回按钮
- **离线使用** — 所有数据内置在应用中，无需网络即可使用

## 技术栈

| 类别 | 技术 |
|------|------|
| 框架 | React Native 0.81 + Expo SDK 54 |
| 图形渲染 | react-native-svg（田字格 + 笔顺动画） |
| 语音播报 | expo-speech |
| 笔顺识别 | cnchar + cnchar-order |
| 数据格式 | 笔画路径 SVG path 数据，分块懒加载 |

## 项目结构

```
StrokeOrderApp/
├── App.js                          # 应用入口，三屏切换
├── app.json                        # Expo 配置
├── package.json                    # 依赖管理
├── assets/
│   ├── stroke_data/
│   │   ├── index.json              # 汉字索引（9574字，含笔画数）
│   │   ├── char_attrs.json         # 汉字属性（部首、注音、释义）
│   │   ├── stroke_names.json       # 笔画名称映射
│   │   └── words.json              # 组词数据
│   └── ...                         # 图标和启动画面
├── src/
│   ├── data/
│   │   ├── lookup.js               # 笔顺数据分块懒加载查询
│   │   └── strokes_0.js ~ strokes_19.js  # 20个数据分块（每块~500字）
│   └── screens/
│       ├── StrokeHomeScreen.js     # 首页：搜索 + 汉字笔画表
│       ├── StrokeDetailScreen.js   # 详情页：田字格动画 + 属性 + 组词
│       └── AboutScreen.js          # 关于页：功能介绍 + 数据来源
├── gen_data.py                     # 笔顺数据分块生成脚本
├── gen_stroke_names.py             # 笔画名称生成脚本
├── gen_stroke_names_from_cnchar.js # 笔画名称生成脚本（cnchar版）
├── gen_words.py                    # 组词数据生成脚本
└── curated_overrides.json          # 人工校验的笔画名称覆盖
```

## 快速开始

### 环境要求

- Node.js >= 18
- npm 或 yarn
- Expo CLI

### 安装运行

```bash
# 安装依赖
npm install

# 启动开发服务器
npx expo start

# 在 Android 设备/模拟器上运行
npx expo run:android
```

### 数据生成

笔顺数据通过脚本从 hanzi-writer-data 生成：

```bash
# 生成笔顺分块数据（需要先安装 hanzi-writer-data）
python gen_data.py

# 生成笔画名称映射
python gen_stroke_names.py
```

## 使用指南

1. **首页** — 显示汉字笔画表，按笔画数排列；点击「显示全部」可展示所有汉字
2. **搜索** — 顶部搜索框输入汉字即可查询，输入后自动筛选匹配结果
3. **详情页** — 展示田字格笔顺动画、汉字属性（笔画数、Unicode、音序、偏旁部首、注音、释义）和组词
4. **重播** — 点击「重播」按钮重新播放笔顺动画
5. **朗读** — 点击喇叭图标朗读完整笔顺（"某字，共N画。第一笔，横。第二笔..."）
6. **返回** — 向右滑动屏幕或按系统返回键回到首页

## 数据来源

- **笔顺规范**：《通用规范汉字笔顺规范》(GF 0023－2020)，教育部/国家语委 2020 年发布
- **笔画路径**：Hanzi Writer 开源项目 ([chanind/hanzi-writer-data](https://github.com/chanind/hanzi-writer-data))
- **汉字属性**：Make Me A Hanzi 开源项目 ([skishore/makemeahanzi](https://github.com/skishore/makemeahanzi))

## 许可证

MIT License
