# PR & Issue 智能治理 Review 报告 · cann/npu-simulator

| 维度 | 详情 |
|---|---|
| **目标仓库** | [cann/npu-simulator](https://gitcode.com/cann/npu-simulator)（GitCode） |
| **巡检时间** | 2026-11-12 22:37 (UTC+8) |
| **分析引擎** | `gitcode-issue-triage` 确定性守卫 + Pi Agent (`cannbot/deepseek-v4.1-flash`) |
| **判定原则** | 宁漏勿错：强灌水信号 + 无安全否决 → 低价值候选；有任何实质代码/测试/关联 Issue → 保留并给出合路建议 |

---

## 一、执行摘要（供 on-call & committer 速览）

- **Issue 巡检**：共扫描 **49** 条 Issue，判定 KEEP **49** / CLOSE 候选 **0** / 待人工复核 **0**。
- **Open PR 总览（共 1 个）**：
  - ✅ **可立即合入（0 个）**：无
  - ⚠️ **实质贡献但门禁阻塞（1 个）**：#50
  - 🧹 **低价值/表面改动候选（0 个）**：无

## 二、Open PR 逐条深度评审与行动清单

| PR | AI 结论 | 合路门禁 | 关联 Issue | 改动规模 (实质文件) | AI 改动摘要与关联对齐 | committer 建议动作 |
|---|---|---|---|---|---|---|
| [#50](https://gitcode.com/cann/npu-simulator/pulls/50) | **🤖 阻塞待解** | ❌ 缺 ci-pipeline-passed；阻塞标签 stat/needs-squash | — | +930/-34 (14/14 实质) | 新增 Roofline 分析器、JSON 导出与 SQL 表，统一函数地址字段（无关联 Issue，新特性缺方案讨论） | 要求作者 squash 提交、补测试并等 CI 转绿后再评审合入 |

### PR #50：[WIP] Enable Source/Assembly and Roofline features for npusim-prof

- **作者**：`@churkinaleksandr` · **停留自然时长**：0.3h · **AI 判定**：**🤖 阻塞待解**
- **代码规模**：14 个文件（实质改动文件 14 个，表面改动文件 0 个，新增测试 +0 行）
- **关联 Issue 对齐**：无关联 Issue，新特性缺方案讨论
- **核心改动摘要**：新增 Roofline 分析器、JSON 导出与 SQL 表，统一函数地址字段
  - Functions 表 SourceInstrAddr 改为 FunctionAddr，需同步迁移旧库与调用方
  - 新增 930 行无任何测试覆盖，Roofline 计算与 SQL schema 缺乏验证证据
  - 标题仍为 [WIP] 且需 squash，作者自述未补测试与文档
- **committer 建议动作**：**要求作者 squash 提交、补测试并等 CI 转绿后再评审合入**

