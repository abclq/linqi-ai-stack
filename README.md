# 林柒 AI 技术栈

[![Private](https://img.shields.io/badge/repo-private-orange.svg)](https://github.com/abclq)
[![Components](https://img.shields.io/badge/components-2-blue.svg)](https://github.com/abclq)

一套围绕「语音内容 → 知识库」的轻量 AI 工具链，由两个互相联动的项目组成。

## 🧩 组件

| 项目 | 作用 | 仓库 |
|------|------|------|
| **抖音收藏 → 知识库（教程）** | 如何搭建这套流程的方法论 + 脚本模板（不含真实收藏） | [abclq/douyin-kb-tutorial](https://github.com/abclq/douyin-kb-tutorial) |
| **抖音收藏 → 知识库（数据）** | 实际整理好的知识库笔记（私密，勿外传） | [abclq/douyin-fav-kb](https://github.com/abclq/douyin-fav-kb) *(private)* |
| **统一语音转写网关** | Cloudflare Worker，Groq→腾讯云→本地硅基流动三层 STT 兜底 | [abclq/groq-asr-proxy](https://github.com/abclq/groq-asr-proxy) |

## 🔗 关系

```
抖音收藏夹
   │  抓取 + 音频下载
   ▼
douyin-fav-kb (本地流水线)
   │  语音转写请求
   ▼
groq-asr-proxy (STT 网关)
   ├─ 1. Groq whisper-large-v3-turbo (CF 美国出口, 免费)
   ├─ 2. 腾讯云 ASR (云端兜底)
   └─ 3. 本地硅基流动 3001 (调用方脚本回落)
   │
   ▼
逐字稿 ──► douyin-fav-kb AI 整理 ──► 知识库笔记
```

- 平时机器人日常语音：直接本机硅基流动 3001 国内直连
- 批量任务（如知识库构建）：走 groq-asr-proxy 云端网关

## 📦 各仓库

- **douyin-fav-kb**：`notes/` 知识库笔记 + 抓取/整理/AI 补充脚本
- **groq-asr-proxy**：Worker 源码 + wrangler 配置 + 部署教程（密钥经 secret 注入，仓库无明文）

## 📄 License

MIT
