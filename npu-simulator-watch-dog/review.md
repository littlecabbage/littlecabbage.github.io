# PR & Issue 智能治理 Review 报告 · cann/npu-simulator

| 维度 | 详情 |
|---|---|
| **目标仓库** | [cann/npu-simulator](https://gitcode.com/cann/npu-simulator)（GitCode） |
| **巡检时间** | 2026-11-14 04:37 (UTC+8) |
| **分析引擎** | `gitcode-issue-triage` 确定性守卫 + Pi Agent (`cannbot/deepseek-v4.1-flash`) |
| **判定原则** | 宁漏勿错：强灌水信号 + 无安全否决 → 低价值候选；有任何实质代码/测试/关联 Issue → 保留并给出合路建议 |

---

## 一、执行摘要（供 on-call & committer 速览）

- **Issue 巡检**：共扫描 **53** 条 Issue，判定 KEEP **53** / CLOSE 候选 **0** / 待人工复核 **0**。
- **Open PR 总览（共 5 个）**：
  - ✅ **可立即合入（0 个）**：无
  - ⚠️ **实质贡献但门禁阻塞（5 个）**：#53、#52、#51、#50、#27
  - 🧹 **低价值/表面改动候选（0 个）**：无

## 二、Open PR 逐条深度评审与行动清单

| PR | AI 结论 | 合路门禁 | 关联 Issue | 改动规模 (实质文件) | AI 改动摘要与关联对齐 | committer 建议动作 |
|---|---|---|---|---|---|---|
| [#53](https://gitcode.com/cann/npu-simulator/pulls/53) | **🤖 阻塞待解** | ❌ 缺 ci-pipeline-passed | [#53](https://gitcode.com/cann/npu-simulator/issues/53) | +9/-0 (1/1 实质) | 两处区间并集扫描前按 TickStart 预排序，修正带宽统计被低估（已针对性修复 #53 带宽低估缺陷） | 需作者补齐 ci-pipeline-passed 门禁并重跑流水线，全绿后可合入 |
| [#52](https://gitcode.com/cann/npu-simulator/pulls/52) | **🤖 阻塞待解** | ❌ 缺 ci-pipeline-passed；阻塞标签 stat/needs-squash | — | +1236/-16 (17/17 实质) | 为 record 新增 --timeout，超时终止进程组并归档部分产物（无关联 Issue，属独立功能增强） | 需作者 squash 提交并补齐 CI 通过后再评审合入 |
| [#51](https://gitcode.com/cann/npu-simulator/pulls/51) | **🤖 阻塞待解** | ❌ 缺 ci-pipeline-passed | [#50](https://gitcode.com/cann/npu-simulator/issues/50) | +797/-36 (12/12 实质) | record 阶段自动提取设备 ELF，并接入 report/prof 逐 kernel 分析（已针对性实现 #50 的自动归档与逐 kernel 发现需求） | 需作者补充 ci-pipeline-passed 标签并重跑 CI，门禁全绿后再合入 |
| [#50](https://gitcode.com/cann/npu-simulator/pulls/50) | **🤖 阻塞待解** | ❌ 阻塞标签 stat/needs-squash | — | +1224/-35 (16/16 实质) | 新增 roofline 分析及 JSON 导出，并修正函数地址区间匹配（无关联 Issue，属新增 roofline 特性） | 需压缩提交解除 needs-squash 后重跑 CI 再评审合入 |
| [#27](https://gitcode.com/cann/npu-simulator/pulls/27) | **🤖 阻塞待解** | ❌ 缺 ci-pipeline-passed | — | +1/-0 (1/1 实质) | 在 .gitattributes 中重复添加同一 png binary 规则，未产生实际配置变化（无关联 Issue，评审要求先规范建 Issue） | 需先补建关联 Issue、删除重复行并重跑 CI 至通过 |

### PR #53：fix(report): order the busy-time sweep by interval start

- **作者**：`@gcw_EkTYFH3T` · **停留自然时长**：8h · **AI 判定**：**🤖 阻塞待解**
- **代码规模**：1 个文件（实质改动文件 1 个，表面改动文件 0 个，新增测试 +0 行）
- **关联 Issue 对齐**：已针对性修复 #53 带宽低估缺陷
- **核心改动摘要**：两处区间并集扫描前按 TickStart 预排序，修正带宽统计被低估
  - 在 calc_throughput_stats 与被调内联副本两处扫描前各加一次按起点排序，代价 O(n log n)、可接受
  - 选择在调用方固化有序前提、保留原 ORDER BY TickEnd，避免改动 8 处 SQL，兼容性更好
  - 逻辑正确但未新增单测；建议补充交错区间用例（长传输与短传输重叠）以防回归
  - 仅缺 ci-pipeline-passed 标签，CLA 已通过、无冲突与 squash 问题，补跑 CI 即可
- **committer 建议动作**：**需作者补齐 ci-pipeline-passed 门禁并重跑流水线，全绿后可合入**

### PR #52：feat(record): 支持 --timeout 限制仿真时长并在超时后自动终止

- **作者**：`@Li_cube` · **停留自然时长**：12.4h · **AI 判定**：**🤖 阻塞待解**
- **代码规模**：17 个文件（实质改动文件 17 个，表面改动文件 0 个，新增测试 +455 行）
- **关联 Issue 对齐**：无关联 Issue，属独立功能增强
- **核心改动摘要**：为 record 新增 --timeout，超时终止进程组并归档部分产物
  - 实现 SIGTERM→5s 宽限→SIGKILL 终止整个进程组，覆盖孙进程
  - 新增 5 个测试文件覆盖解析、超时终止与状态回填，需 CI 验证
- **committer 建议动作**：**需作者 squash 提交并补齐 CI 通过后再评审合入**

### PR #51：feat: 自动归档 AI Core 设备 ELF 并接入逐 kernel report/prof 分析

- **作者**：`@zengzihui` · **停留自然时长**：19.4h · **AI 判定**：**🤖 阻塞待解**
- **代码规模**：12 个文件（实质改动文件 12 个，表面改动文件 0 个，新增测试 +414 行）
- **关联 Issue 对齐**：已针对性实现 #50 的自动归档与逐 kernel 发现需求
- **核心改动摘要**：record 阶段自动提取设备 ELF，并接入 report/prof 逐 kernel 分析
  - 新增 DeviceObjectResolver 按 kernel 符号精确匹配，缺失或歧义时关闭 object 依赖分析，避免误选
  - 归档失败仅告警不阻断录制，并校验 Ascend ELF 边界、拒绝 host ELF/截断/symlink；含 5 个测试文件 414 行
  - report/prof 上下文 object_file、kernel_name 保存与恢复逻辑需确认线程安全与异常路径
  - hidumper 缓存 key 改为 (obj_path, kernel_name, force_disassembly)，可能影响既有缓存命中与磁盘占用
- **committer 建议动作**：**需作者补充 ci-pipeline-passed 标签并重跑 CI，门禁全绿后再合入**

### PR #50：[WIP] Enable Source/Assembly and Roofline features for npusim-prof

- **作者**：`@churkinaleksandr` · **停留自然时长**：30.3h · **AI 判定**：**🤖 阻塞待解**
- **代码规模**：16 个文件（实质改动文件 16 个，表面改动文件 0 个，新增测试 +0 行）
- **关联 Issue 对齐**：无关联 Issue，属新增 roofline 特性
- **核心改动摘要**：新增 roofline 分析及 JSON 导出，并修正函数地址区间匹配
  - 新增 roofline 分析器、报表器与 SQL 表，共 16 文件 1224 行，属实质特性改动，须按 WIP 转正流程补齐测试
  - Functions 表 SourceInstrAddr 改 FunctionAddr 涉及 schema 与查询兼容性，需确认旧库升级路径并补充 UT
- **committer 建议动作**：**需压缩提交解除 needs-squash 后重跑 CI 再评审合入**

### PR #27：update: 更新文件 .gitattributes

- **作者**：`@ZhouBX` · **停留自然时长**：258.8h · **AI 判定**：**🤖 阻塞待解**
- **代码规模**：1 个文件（实质改动文件 1 个，表面改动文件 0 个，新增测试 +0 行）
- **关联 Issue 对齐**：无关联 Issue，评审要求先规范建 Issue
- **核心改动摘要**：在 .gitattributes 中重复添加同一 png binary 规则，未产生实际配置变化
  - 新增行与首行完全一致，属重复配置，建议删除或改真实规则
  - ci-pipeline-failed，缺 ci-pipeline-passed，且缺关联 Issue 与测试说明
- **committer 建议动作**：**需先补建关联 Issue、删除重复行并重跑 CI 至通过**

