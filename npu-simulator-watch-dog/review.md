# PR & Issue 智能治理 Review 报告 · cann/npu-simulator

| 维度 | 详情 |
|---|---|
| **目标仓库** | [cann/npu-simulator](https://gitcode.com/cann/npu-simulator)（GitCode） |
| **巡检时间** | 2026-11-13 13:37 (UTC+8) |
| **分析引擎** | `gitcode-issue-triage` 确定性守卫 + Pi Agent (`cannbot/deepseek-v4.1-flash`) |
| **判定原则** | 宁漏勿错：强灌水信号 + 无安全否决 → 低价值候选；有任何实质代码/测试/关联 Issue → 保留并给出合路建议 |

---

## 一、执行摘要（供 on-call & committer 速览）

- **Issue 巡检**：共扫描 **50** 条 Issue，判定 KEEP **50** / CLOSE 候选 **0** / 待人工复核 **0**。
- **Open PR 总览（共 3 个）**：
  - ✅ **可立即合入（0 个）**：无
  - ⚠️ **实质贡献但门禁阻塞（3 个）**：#51、#50、#27
  - 🧹 **低价值/表面改动候选（0 个）**：无

## 二、Open PR 逐条深度评审与行动清单

| PR | AI 结论 | 合路门禁 | 关联 Issue | 改动规模 (实质文件) | AI 改动摘要与关联对齐 | committer 建议动作 |
|---|---|---|---|---|---|---|
| [#51](https://gitcode.com/cann/npu-simulator/pulls/51) | **🤖 阻塞待解** | ❌ 缺 ci-pipeline-passed | [#50](https://gitcode.com/cann/npu-simulator/issues/50) | +797/-36 (12/12 实质) | record 阶段自动提取设备 ELF，并接入 report/prof 逐 kernel 分析（已针对性实现 #50 的自动归档与逐 kernel 发现需求） | 需作者补充 ci-pipeline-passed 标签并重跑 CI，门禁全绿后再合入 |
| [#50](https://gitcode.com/cann/npu-simulator/pulls/50) | **🤖 阻塞待解** | ❌ 阻塞标签 stat/needs-squash | — | +930/-34 (14/14 实质) | 新增 Roofline 分析与 JSON 导出，修正函数地址字段（无关联 Issue，属新特性增强提交） | 需作者 squash 提交并解除 needs-squash 阻塞后再合入 |
| [#27](https://gitcode.com/cann/npu-simulator/pulls/27) | **🤖 阻塞待解** | ❌ 缺 ci-pipeline-passed | — | +1/-0 (1/1 实质) | 在 .gitattributes 中重复添加同一 png binary 规则，未产生实际配置变化（无关联 Issue，评审要求先规范建 Issue） | 需先补建关联 Issue、删除重复行并重跑 CI 至通过 |

### PR #51：feat: 自动归档 AI Core 设备 ELF 并接入逐 kernel report/prof 分析

- **作者**：`@zengzihui` · **停留自然时长**：4.4h · **AI 判定**：**🤖 阻塞待解**
- **代码规模**：12 个文件（实质改动文件 12 个，表面改动文件 0 个，新增测试 +414 行）
- **关联 Issue 对齐**：已针对性实现 #50 的自动归档与逐 kernel 发现需求
- **核心改动摘要**：record 阶段自动提取设备 ELF，并接入 report/prof 逐 kernel 分析
  - 新增 DeviceObjectResolver 按 kernel 符号精确匹配，缺失或歧义时关闭 object 依赖分析，避免误选
  - 归档失败仅告警不阻断录制，并校验 Ascend ELF 边界、拒绝 host ELF/截断/symlink；含 5 个测试文件 414 行
  - report/prof 上下文 object_file、kernel_name 保存与恢复逻辑需确认线程安全与异常路径
  - hidumper 缓存 key 改为 (obj_path, kernel_name, force_disassembly)，可能影响既有缓存命中与磁盘占用
- **committer 建议动作**：**需作者补充 ci-pipeline-passed 标签并重跑 CI，门禁全绿后再合入**

### PR #50：[WIP] Enable Source/Assembly and Roofline features for npusim-prof

- **作者**：`@churkinaleksandr` · **停留自然时长**：15.3h · **AI 判定**：**🤖 阻塞待解**
- **代码规模**：14 个文件（实质改动文件 14 个，表面改动文件 0 个，新增测试 +0 行）
- **关联 Issue 对齐**：无关联 Issue，属新特性增强提交
- **核心改动摘要**：新增 Roofline 分析与 JSON 导出，修正函数地址字段
  - 新增 RooflineAnalyzer/Reporter 及 4 张表，为实质新功能，但无任何新增测试佐证
  - Functions 表 SourceInstrAddr 改为 FunctionAddr，属 schema 变更，需说明兼容性影响
  - PR 标记 WIP 且正文方案/测试章节为空，缺少合入所需的验证证据
- **committer 建议动作**：**需作者 squash 提交并解除 needs-squash 阻塞后再合入**

### PR #27：update: 更新文件 .gitattributes

- **作者**：`@ZhouBX` · **停留自然时长**：243.8h · **AI 判定**：**🤖 阻塞待解**
- **代码规模**：1 个文件（实质改动文件 1 个，表面改动文件 0 个，新增测试 +0 行）
- **关联 Issue 对齐**：无关联 Issue，评审要求先规范建 Issue
- **核心改动摘要**：在 .gitattributes 中重复添加同一 png binary 规则，未产生实际配置变化
  - 新增行与首行完全一致，属重复配置，建议删除或改真实规则
  - ci-pipeline-failed，缺 ci-pipeline-passed，且缺关联 Issue 与测试说明
- **committer 建议动作**：**需先补建关联 Issue、删除重复行并重跑 CI 至通过**

