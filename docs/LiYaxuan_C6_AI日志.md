# C6 AI 日志

## 产品设计阶段
- 用 AI（豆包/Claude）讨论 C6 项目方向：选择"Skill X-Ray 技能分析器"，与 C4 技能分享形成闭环——把别人写的 SKILL.md 丢进来就能体检。
- 明确边界：核心功能必须**纯本地规则引擎**实现（免 API key、免登录），AI 深度点评作为**可选增强**（用户自填 key，仅存 localStorage）。

## 前端开发阶段
- AI 生成首版单文件 HTML：青蓝/teal 配色、双栏布局、响应式。
- AI 设计规则引擎：解析 YAML frontmatter → 提取标题 → 正则识别 references/scripts 目录 → 关键词判断（适用场景/不适用边界/示例/警告/交付物）→ 四维评分 D1-D4 → 生成带优先级的改进建议。
- AI 设计可选 AI 集成：OpenAI 兼容 `/chat/completions`，用户在折叠面板里填 Base URL / Key / Model，key 只写 localStorage，刷新不丢、绝不硬编码到代码。

## 调试阶段（真实踩坑）
- **Bug**：首版截图发现报告区域一直显示"等待输入"，分析结果不出。
- **定位**：用 node --check 抽取 JS 做语法检查，发现 `detectDirs` 的正则 `/[\s`)]*)/` 里字符类提前被 `]` 闭合，导致整个 `<script>` 块解析失败，`analyze` 函数根本没定义。
- **修复**：把字符类改为 `[^\s`)\]]+`（转义 `]`），重新 node --check 通过，重新上传 GitHub。
- 这一步是 AI + 工具链协作：AI 写代码，headless Edge 截图暴露问题，node --check 定位根因，再修。

## 部署阶段
- 用 gh_helper.py（GitHub REST API）创建仓库、upload-dir 上传 index.html、enable-pages 开启 Pages。
- 轮询 https://yx922418yz.github.io/EduSeed-C6-SkillXRay/ 直到 HTTP 200 且页面含 "Skill X-Ray"。

## 迭代记录
- v1：初版，规则引擎 + 可选 AI 点评。
- v1.1：修复正则语法错误（上述调试）。
