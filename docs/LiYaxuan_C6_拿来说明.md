# C6 拿来说明

## 借鉴与使用的开源/第三方资源

| 拿来什么 | 从哪拿 | 怎么改 |
|----------|--------|--------|
| 整体产品形态 | C6 CHALLENGE.md 第八节"示例 2：skill-explainer" | 把示例里"Claude API 驱动"改为"本地规则引擎驱动 + 可选 AI 点评"，让核心功能免 key 可用 |
| ECharts / 图表思路 | 不用图表库，用纯 CSS 进度条做四维评分，避免外部依赖 | 改造为 CSS `.scorebar` 宽度动画 |
| OpenAI 兼容 API 调用模式 | OpenAI Cookbook / 通用 fetch 模式 | 改为用户自填 Base URL/Key/Model，key 不硬编码；并新增 DeepSeek 快捷预设（base https://api.deepseek.com，模型 deepseek-flash），已在浏览器实测点通 |
| DeepSeek 接入 | DeepSeek 官方 OpenAI 兼容接口（api.deepseek.com，模型 deepseek-flash；CORS 放行 Pages 源） | 仅作为用户可选点评后端，key 由用户在页面自填、绝不内置 |
| teal/青蓝配色 | 用户偏好（青蓝色系） | CSS 变量集中定义 `--teal-900..--teal-50` |
| 响应式布局 | 通用 CSS Grid `@media(max-width:820px)` | 双栏在窄屏自动堆叠为单列 |

## 没有使用
- 没有用 React/Vue/Tailwind CDN（纯原生，离线可用）。
- 没有硬编码任何 API key。
- 没有引入后端。
