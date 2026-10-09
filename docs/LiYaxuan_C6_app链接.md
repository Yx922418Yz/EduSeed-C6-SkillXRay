# C6 Web Application 线上地址

## 产品：Skill X-Ray · 技能分析器

- **线上 URL**：https://yx922418yz.github.io/EduSeed-C6-SkillXRay/
- **一句话说明**：粘贴或上传 SKILL.md / .skill 文件，本地 JavaScript 规则引擎立即给出结构化分析——技能身份、用途识别、目录结构可视化、四维评分 D1–D4、具体改进建议；无需 API Key、免登录、纯前端运行。

## 可用性自检（对应 CHALLENGE.md 3.2）

| 检查项 | 结果 |
|--------|------|
| 打开链接 30 秒内知道做什么 | 顶部标题 + 双栏（输入/报告）一目了然 |
| 免登录体验核心功能 | 是，规则引擎完全本地运行，不需要任何 key |
| 核心流程走通（输入→处理→输出） | 是，粘贴示例→点"X-Ray 分析"→右侧出报告 |
| 手机浏览器可用 | 是，响应式布局，移动端单列堆叠 |
| 加载 < 5 秒 | 是，纯静态单文件，无外部依赖 |
| API Key 不暴露在前端 | 是，用户可选自填 OpenAI 兼容 key，仅存 localStorage |

## 可选：AI 深度点评接入 DeepSeek（OpenAI 兼容）—— 已实测点通 ✅

核心体检功能完全离线；AI 深度点评页面已内置 **DeepSeek 快捷预设**，无需任何中转：

1. 展开"可选：接入自己的 AI Key"，点 **DeepSeek（国内推荐）**，自动填好
   Base URL `https://api.deepseek.com`、模型 `deepseek-flash`；
2. 在 API Key 处填入自己的 DeepSeek key（sk- 开头，到 https://platform.deepseek.com 创建）；
3. 点"请求 AI 深度点评"。Key 仅存在本机浏览器，绝不写入代码、不经过第三方服务器。

**实测结果（2026-10-09）**：在浏览器中用 DeepSeek key 真实点通，返回了"核心价值 / 三个改进点 / 工作流位置"的完整点评（截图 `screenshots/05_AI深度点评_DeepSeek.png`）。跨域（CORS）已验证：DeepSeek 预检 `OPTIONS` 返回 200，且带 `access-control-allow-origin`（放行 GitHub Pages 源）、`allow-methods: POST`、`allow-headers: authorization,content-type`，因此页面可直接在浏览器调用，无需自建中转。

> 模型 ID 说明：DeepSeek 当前线上模型为 `deepseek-flash`、`deepseek-v4-pro`（`GET https://api.deepseek.com/models` 可查），旧的 `deepseek-chat` 已退役。DeepSeek 与 OpenAI 的 `/chat/completions` 协议完全兼容，同一个前端可在 DeepSeek / OpenAI / 任意 OpenAI 兼容中转间切换，只需改 Base URL 与模型名。
