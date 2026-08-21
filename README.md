# DeepSeek Harness 研究报告

十三篇关于 [deepseek-ai/deepseek-harness](https://github.com/deepseek-ai/deepseek-harness) 仓库的中文长报告——架构、开发工作流、文档治理、Skill 体系、CI 与仓库治理、前端验证留档、团队组织与分工，以及一份外部信源勘察。

01–07 基于仓库快照 `47f943859b`（2026-08-13）；08–10 与 `xiaoxuan/` 下的三篇补充调研基于 `141eb6fef8`（tag `dsh-v0.1.0-rc.8`，2026-08-19）。文中的 commit hash / 文件路径都可自行复核。

每个 `.html` 都是自包含单文件网页：内嵌样式与 SVG，无外部依赖，离线可读，跟随系统浅色/深色。


## 目录

| # | 报告 | 主题 | 在线预览 | 发布 |
|---|------|------|----------|------|
| 01 | [`01-解剖·架构（第一卷）.html`](01-%E8%A7%A3%E5%89%96%C2%B7%E6%9E%B6%E6%9E%84%EF%BC%88%E7%AC%AC%E4%B8%80%E5%8D%B7%EF%BC%89.html) | 架构解剖：turn 怎么跑、四层补丁如何压平、26 个能力接缝、E2B 替换的删除量、62 道闸门、账单与风险 | [预览](https://htmlpreview.github.io/?https://github.com/TonQiaN/dsh-research-reports/blob/main/01-%E8%A7%A3%E5%89%96%C2%B7%E6%9E%B6%E6%9E%84%EF%BC%88%E7%AC%AC%E4%B8%80%E5%8D%B7%EF%BC%89.html) | 2026-08-17 |
| 02 | [`02-闸门代替信任·开发方法.html`](02-%E9%97%B8%E9%97%A8%E4%BB%A3%E6%9B%BF%E4%BF%A1%E4%BB%BB%C2%B7%E5%BC%80%E5%8F%91%E6%96%B9%E6%B3%95.html) | 开发方法：分支名取证、流程被失败逼出来的时间线、协作的记忆机制、把关体系三态（机器把关／评审负责／已命名的洞） | [预览](https://htmlpreview.github.io/?https://github.com/TonQiaN/dsh-research-reports/blob/main/02-%E9%97%B8%E9%97%A8%E4%BB%A3%E6%9B%BF%E4%BF%A1%E4%BB%BB%C2%B7%E5%BC%80%E5%8F%91%E6%96%B9%E6%B3%95.html) | 2026-08-17 |
| 03 | [`03-文档治理·结构与时间线（初版）.html`](03-%E6%96%87%E6%A1%A3%E6%B2%BB%E7%90%86%C2%B7%E7%BB%93%E6%9E%84%E4%B8%8E%E6%97%B6%E9%97%B4%E7%BA%BF%EF%BC%88%E5%88%9D%E7%89%88%EF%BC%89.html) | 文档治理第一版：五层结构 + 两条横切机制、分层表、Agent Notes 生命周期、28 个门禁、从 692 字节到 16.8 MB 的时间线 | [预览](https://htmlpreview.github.io/?https://github.com/TonQiaN/dsh-research-reports/blob/main/03-%E6%96%87%E6%A1%A3%E6%B2%BB%E7%90%86%C2%B7%E7%BB%93%E6%9E%84%E4%B8%8E%E6%97%B6%E9%97%B4%E7%BA%BF%EF%BC%88%E5%88%9D%E7%89%88%EF%BC%89.html) | 2026-08-17 |
| 04 | [`04-工作流·团队协作（第二卷）.html`](04-%E5%B7%A5%E4%BD%9C%E6%B5%81%C2%B7%E5%9B%A2%E9%98%9F%E5%8D%8F%E4%BD%9C%EF%BC%88%E7%AC%AC%E4%BA%8C%E5%8D%B7%EF%BC%89.html) | 开发工作流：谁在写代码、一次变更的九站生命周期、AGENTS.md／Skill／Agent Note、闸门分层、Web GUI 五天冲刺现场、专治 agent 病的规则 | [预览](https://htmlpreview.github.io/?https://github.com/TonQiaN/dsh-research-reports/blob/main/04-%E5%B7%A5%E4%BD%9C%E6%B5%81%C2%B7%E5%9B%A2%E9%98%9F%E5%8D%8F%E4%BD%9C%EF%BC%88%E7%AC%AC%E4%BA%8C%E5%8D%B7%EF%BC%89.html) | 2026-08-17 |
| 05 | [`05-文档治理考古（第三卷）.html`](05-%E6%96%87%E6%A1%A3%E6%B2%BB%E7%90%86%E8%80%83%E5%8F%A4%EF%BC%88%E7%AC%AC%E4%B8%89%E5%8D%B7%EF%BC%89.html) | 文档治理考古（重写版）：ADR 0007 元规则、十个地层、AGENTS.md 字数新陈代谢、决策记录六次形态变化、治理的税、给个人 vibecoder 的学习路线 | [预览](https://htmlpreview.github.io/?https://github.com/TonQiaN/dsh-research-reports/blob/main/05-%E6%96%87%E6%A1%A3%E6%B2%BB%E7%90%86%E8%80%83%E5%8F%A4%EF%BC%88%E7%AC%AC%E4%B8%89%E5%8D%B7%EF%BC%89.html) | 2026-08-17 |
| 06 | [`06-谁在讲开发流程·外部信源盘点.html`](06-%E8%B0%81%E5%9C%A8%E8%AE%B2%E5%BC%80%E5%8F%91%E6%B5%81%E7%A8%8B%C2%B7%E5%A4%96%E9%83%A8%E4%BF%A1%E6%BA%90%E7%9B%98%E7%82%B9.html) | 外部信源勘察：讲 dsh 开发流程的公开材料分级、那条推文数字的本地复算、已证伪的八条说法、五条自产材料的线 | [预览](https://htmlpreview.github.io/?https://github.com/TonQiaN/dsh-research-reports/blob/main/06-%E8%B0%81%E5%9C%A8%E8%AE%B2%E5%BC%80%E5%8F%91%E6%B5%81%E7%A8%8B%C2%B7%E5%A4%96%E9%83%A8%E4%BF%A1%E6%BA%90%E7%9B%98%E7%82%B9.html) | 2026-08-18 |
| 07 | [`07-十一个 Skill（第四卷）.html`](07-%E5%8D%81%E4%B8%80%E4%B8%AA%20Skill%EF%BC%88%E7%AC%AC%E5%9B%9B%E5%8D%B7%EF%BC%89.html) | 十一个 Skill：每份 SKILL.md 的出生疼痛、体量与附件、写法解剖、四个簇、skill 里的「agent 病历」、与 AGENTS.md／文档／闸门／笔记的分工、陈旧与上下文税 | [预览](https://htmlpreview.github.io/?https://github.com/TonQiaN/dsh-research-reports/blob/main/07-%E5%8D%81%E4%B8%80%E4%B8%AA%20Skill%EF%BC%88%E7%AC%AC%E5%9B%9B%E5%8D%B7%EF%BC%89.html) | 2026-08-19 |
| 08 | [`08-.github 控制面（第五卷）.html`](08-.github%20%E6%8E%A7%E5%88%B6%E9%9D%A2%EF%BC%88%E7%AC%AC%E4%BA%94%E5%8D%B7%EF%BC%89.html) | `.github/` 考古：27 个文件的四层结构、ci.yml 的 15 个 job 与 `all-checks-passed`、四条发布序列、706 行 Issue 策略引擎、251 次提交的四段时间线、ci.yml 的七个阶段、41 篇 Agent Note 提炼的原则，以及公开仓上跑不起来的那一面 | [预览](https://htmlpreview.github.io/?https://github.com/TonQiaN/dsh-research-reports/blob/main/08-.github%20%E6%8E%A7%E5%88%B6%E9%9D%A2%EF%BC%88%E7%AC%AC%E4%BA%94%E5%8D%B7%EF%BC%89.html) | 2026-08-21 |
| 09 | [`09-前端验证留档（第六卷）.html`](09-%E5%89%8D%E7%AB%AF%E9%AA%8C%E8%AF%81%E7%95%99%E6%A1%A3%EF%BC%88%E7%AC%AC%E5%85%AD%E5%8D%B7%EF%BC%89.html) | 前端验证留档：Web GUI 的文档管理五装置、GUI 测试三层与 PR 上唯一的浏览器闸门、`apps/web/tests/snapshots/` 证据解剖（64 场景 / 138 文件）、教 AI 留档的六个机制、以及哪些规矩是闸门、哪些只是写给 AI 看的一句话 | [预览](https://htmlpreview.github.io/?https://github.com/TonQiaN/dsh-research-reports/blob/main/09-%E5%89%8D%E7%AB%AF%E9%AA%8C%E8%AF%81%E7%95%99%E6%A1%A3%EF%BC%88%E7%AC%AC%E5%85%AD%E5%8D%B7%EF%BC%89.html) | 2026-08-21 |
| 10 | [`10-谁写了 DeepSeek Harness（第七卷）.html`](10-%E8%B0%81%E5%86%99%E4%BA%86%20DeepSeek%20Harness%EF%BC%88%E7%AC%AC%E4%B8%83%E5%8D%B7%EF%BC%89.html) | 团队组织与分工：28 人名册与在场区间、Tianyi Cui 到底负责什么、合并权在三周内从 100% 交到 18% 的曲线、十四张人物卡、包边界当并发调度基元（78.2% 的「包×日」只有一个作者）、分支前缀里的工具签名、被删掉的 missions/ 九人 AI 队友账本，以及「人 + AI 舰队」的四层组织结构 | [预览](https://htmlpreview.github.io/?https://github.com/TonQiaN/dsh-research-reports/blob/main/10-%E8%B0%81%E5%86%99%E4%BA%86%20DeepSeek%20Harness%EF%BC%88%E7%AC%AC%E4%B8%83%E5%8D%B7%EF%BC%89.html) | 2026-08-21 |
| X01 | [`xiaoxuan/01-从-Issue-到-PR·代码开发全流程.html`](xiaoxuan/01-%E4%BB%8E-Issue-%E5%88%B0-PR%C2%B7%E4%BB%A3%E7%A0%81%E5%BC%80%E5%8F%91%E5%85%A8%E6%B5%81%E7%A8%8B.html) | Idea 到 PR 主线：Issue 分诊、Ready、worktree、Plan / Spec、实现、测试、pre-push、PR、CI 与人工验收，以及每一站的自动化边界 | [预览](https://htmlpreview.github.io/?https://github.com/TonQiaN/dsh-research-reports/blob/main/xiaoxuan/01-%E4%BB%8E-Issue-%E5%88%B0-PR%C2%B7%E4%BB%A3%E7%A0%81%E5%BC%80%E5%8F%91%E5%85%A8%E6%B5%81%E7%A8%8B.html) | 2026-08-20 |
| X02 | [`xiaoxuan/02-DeepSeek-Harness·文档管理全流程.html`](xiaoxuan/02-DeepSeek-Harness%C2%B7%E6%96%87%E6%A1%A3%E7%AE%A1%E7%90%86%E5%85%A8%E6%B5%81%E7%A8%8B.html) | 文档生命周期：Issue、Agent Note、README / JSDoc、双语同步、Snapshot、CI、Postmortem 与归档如何随代码一起演进 | [预览](https://htmlpreview.github.io/?https://github.com/TonQiaN/dsh-research-reports/blob/main/xiaoxuan/02-DeepSeek-Harness%C2%B7%E6%96%87%E6%A1%A3%E7%AE%A1%E7%90%86%E5%85%A8%E6%B5%81%E7%A8%8B.html) | 2026-08-20 |
| X03 | [`xiaoxuan/03-DeepSeek-Harness·开发流程Skills地图.html`](xiaoxuan/03-DeepSeek-Harness%C2%B7%E5%BC%80%E5%8F%91%E6%B5%81%E7%A8%8BSkills%E5%9C%B0%E5%9B%BE.html) | 开发流程 Skills 地图：11 份 Skill 覆盖哪些环节、如何触发、与 AGENTS.md / CI 如何分工，以及 Idea、Issue、Worktree、Plan、测试设计和 PR 创建等缺口 | [预览](https://htmlpreview.github.io/?https://github.com/TonQiaN/dsh-research-reports/blob/main/xiaoxuan/03-DeepSeek-Harness%C2%B7%E5%BC%80%E5%8F%91%E6%B5%81%E7%A8%8BSkills%E5%9C%B0%E5%9B%BE.html) | 2026-08-20 |

> GitHub 不会渲染仓库里的 `.html`，点开只看到源码。上表的「预览」走第三方的 htmlpreview 渲染；更稳的方式是 `git clone` 或下载 ZIP 后用浏览器打开。

## 关于编号

01、04、05、07、08、09、10 是同一个系列的第一到第七卷（架构 → 工作流 → 文档治理 → Skill 体系 → CI 与仓库治理 → 前端验证留档 → 团队组织），版式同源、强调色各异。

02 与 03 是系列之外的两篇独立报告。其中 03 是文档治理主题的早期版本，05 是后来重做、篇幅更大的一版——两者标题相同但内容不同，故分别保留。

X01–X03 位于 `xiaoxuan/`，从实际使用问题出发，分别沿 Idea → PR 主线、文档生命周期和 Skills 覆盖地图展开。

## 建议阅读顺序

先 01（它是什么），再 04（他们怎么做），再 05（文档治理怎么长出来的），再 07（写给 agent 的剧本长什么样），再 08（这一切最后由哪些闸门兜住），再 09（怎么逼 agent 交出可复核的验证证据），最后 10（这些制度背后是哪些人、怎么分工）；02 是 04 的另一种切法，更短、更聚焦「什么在兜底」；06 用来判断外面哪些文章值得读、哪些数字不能转引。

如果更关心一项工作如何落地，可以从 X01 开始，再读 X02（文档如何伴随代码），最后读 X03（Skills 能做什么、不能做什么）。

## 来源与免责

01–09 由原作者用 Claude Code 做仓库考古 + 多轮事实核查后写成；X01–X03 是 `xiaoxuan/` 下的补充调研。所有报告均与 DeepSeek 官方无关，也没有任何内部信息来源；数字来自公开仓库的脚本统计。如发现错漏，欢迎开 Issue。
