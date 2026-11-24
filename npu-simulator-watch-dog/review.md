# PR & Issue 智能治理 Review 报告 · cann/npu-simulator

| 维度 | 详情 |
|---|---|
| **目标仓库** | [cann/npu-simulator](https://gitcode.com/cann/npu-simulator)（GitCode） |
| **巡检时间** | 2026-11-24 12:38 (UTC+8) |
| **分析引擎** | `gitcode-issue-triage` 确定性守卫 + Pi Agent (`cannbot/deepseek-v4.1-flash`) |
| **判定原则** | 宁漏勿错：强灌水信号 + 无安全否决 → 低价值候选；有任何实质代码/测试/关联 Issue → 保留并给出合路建议 |

---

## 一、执行摘要（供 on-call & committer 速览）

- **Issue 巡检**：共扫描 **66** 条 Issue，判定 KEEP **65** / CLOSE 候选 **0** / 待人工复核 **1**。
- **Open PR 总览（共 7 个）**：
  - ✅ **可立即合入（2 个）**：#59、#58
  - ⚠️ **实质贡献但门禁阻塞（5 个）**：#72、#70、#67、#64、#60
  - 🧹 **低价值/表面改动候选（0 个）**：无

## 二、Open PR 逐条深度评审与行动清单

| PR | AI 结论 | 合路门禁 | 关联 Issue | 改动规模 (实质文件) | AI 改动摘要与关联对齐 | committer 建议动作 |
|---|---|---|---|---|---|---|
| [#72](https://gitcode.com/cann/npu-simulator/pulls/72) | **🤖 阻塞待解** | ❌ CLA 未签 (cann-cla/no)；缺 cann-cla/yes；缺 ci-pipeline-passed；阻塞标签 stat/needs-squash | — | +80/-0 (2/2 实质) | CI 新增 md_check 静态检查复用 workflow 及流水线任务（无关联 Issue，属 CI 门禁能力增强） | 需先签署 CLA、压缩提交并跑通 CI 后再评审合入 |
| [#70](https://gitcode.com/cann/npu-simulator/pulls/70) | **🤖 阻塞待解** | ❌ 缺 ci-pipeline-passed | [#66](https://gitcode.com/cann/npu-simulator/issues/66) | +5/-5 (0/2 实质) | 修正两份最佳实践文档中英文间距，提升中文可读性（已针对性修复 #66 列明的 5 处间距问题） | 文档改动无害，需等待 ci-pipeline-passed 打标后合入 |
| [#67](https://gitcode.com/cann/npu-simulator/pulls/67) | **🤖 阻塞待解** | ❌ 存在代码冲突；阻塞标签 stat/needs-squash | [#63](https://gitcode.com/cann/npu-simulator/issues/63) | +67/-145 (11/11 实质) | 修复可选处理失败导致 .npu-rep 无法导出的问题（已针对性修复 #63 的导出缺陷） | 需先解决合并冲突、完成 squash 并重跑 CI，然后再合入 |
| [#64](https://gitcode.com/cann/npu-simulator/pulls/64) | **🤖 阻塞待解** | ❌ 阻塞标签 stat/needs-squash | — | +330/-2 (6/6 实质) | 新增 SOL 分析器与 --sol 选项，评估内核吞吐上限（无关联 Issue，新特性未先走方案讨论） | 需作者 squash 提交、补测试并关联 Issue 后再评审 |
| [#60](https://gitcode.com/cann/npu-simulator/pulls/60) | **🤖 阻塞待解** | ❌ 缺 ci-pipeline-passed | [#56](https://gitcode.com/cann/npu-simulator/issues/56) | +11/-5 (1/1 实质) | 把 pending 单槽改为按 twin_key 索引的字典，折叠 fixpipe 孪生行，修复 UB 写重复计数（已针对性修复 #56 孪生行重复计数缺陷） | 暂缓合入：需补齐 ci-pipeline-passed，并回应评审的 key 收紧建议 |
| [#59](https://gitcode.com/cann/npu-simulator/pulls/59) | **🤖 值得合入** | ✅ 可合入 | [#60](https://gitcode.com/cann/npu-simulator/issues/60) | +14/-16 (1/1 实质) | 用正则统一识别 python3.11 等版本化解释器并修正 Python 路径判定（针对性修复 #60 版本化解释器漏判） | CLA 与 CI 均通过且无冲突，建议直接合入 |
| [#58](https://gitcode.com/cann/npu-simulator/pulls/58) | **🤖 值得合入** | ✅ 可合入 | [#59](https://gitcode.com/cann/npu-simulator/issues/59) | +63/-28 (2/2 实质) | 实质代码改动（2 文件 +63/-28），门禁全绿（已关联 #59） | CLA 与 CI 已通过，建议 committer 完成最终代码检视后合入 |

### PR #72：CI 添加StaticCheck_md_check检查项

- **作者**：`@zhouchongshun` · **停留自然时长**：19.9h · **AI 判定**：**🤖 阻塞待解**
- **代码规模**：2 个文件（实质改动文件 2 个，表面改动文件 0 个，新增测试 +0 行）
- **关联 Issue 对齐**：无关联 Issue，属 CI 门禁能力增强
- **核心改动摘要**：CI 新增 md_check 静态检查复用 workflow 及流水线任务
  - 新增 workflow_call 复用模板并接入 CodeCheck 阶段，结构合理，但需确认 md_check 镜像版本来源
  - workflow 名称拼写为 staticheck_action，且启用 allow-unsafe-pr-checkout，需复核安全性
- **committer 建议动作**：**需先签署 CLA、压缩提交并跑通 CI 后再评审合入**

### PR #70：docs(npu-simulator): fix spacing in examples

- **作者**：`@gcw_WJCkAUuk` · **停留自然时长**：55.4h · **AI 判定**：**🤖 阻塞待解**
- **代码规模**：2 个文件（实质改动文件 0 个，表面改动文件 0 个，新增测试 +0 行）
- **关联 Issue 对齐**：已针对性修复 #66 列明的 5 处间距问题
- **核心改动摘要**：修正两份最佳实践文档中英文间距，提升中文可读性
  - 纯文档改动，仅调中英文空格，未改示例命令、参数或技术语义，无回归风险
  - Issue 标题称 26 项但正文仅列 5 项，本 MR 已覆盖全部可核验条目，剩余项需后续 Issue 补充
- **committer 建议动作**：**文档改动无害，需等待 ci-pipeline-passed 打标后合入**

### PR #67：fix(prof): preserve base reports when optional processing fails

- **作者**：`@churkinaleksandr` · **停留自然时长**：110.2h · **AI 判定**：**🤖 阻塞待解**
- **代码规模**：11 个文件（实质改动文件 11 个，表面改动文件 0 个，新增测试 +15 行）
- **关联 Issue 对齐**：已针对性修复 #63 的导出缺陷
- **核心改动摘要**：修复可选处理失败导致 .npu-rep 无法导出的问题
  - 移除独立的 roofline.json 导出，Roofline 结果保留在 SQLite 表和 CSV 中，降低耦合
  - 设备 ELF 解码与 Critical Path 生成失败时降级为告警，保证基础报告产出，并补充单测
- **committer 建议动作**：**需先解决合并冲突、完成 squash 并重跑 CI，然后再合入**

### PR #64：Add Speed-of-light profiling feature

- **作者**：`@fomichevoleg5` · **停留自然时长**：157.9h · **AI 判定**：**🤖 阻塞待解**
- **代码规模**：6 个文件（实质改动文件 6 个，表面改动文件 0 个，新增测试 +0 行）
- **关联 Issue 对齐**：无关联 Issue，新特性未先走方案讨论
- **核心改动摘要**：新增 SOL 分析器与 --sol 选项，评估内核吞吐上限
  - 新增 276 行 SOL 分析器和峰值常量表，需确认 V100 以外架构取值来源
  - report 契约版本放宽到 7 或 8，需评估向后兼容与迁移说明
  - 本次无新增测试文件覆盖，建议补 SpeedOfLightData 生成用例
- **committer 建议动作**：**需作者 squash 提交、补测试并关联 Issue 后再评审**

### PR #60：fix(report): collapse the fixpipe twin rows by identity, not by adjacency

- **作者**：`@gcw_EkTYFH3T` · **停留自然时长**：205.3h · **AI 判定**：**🤖 阻塞待解**
- **代码规模**：1 个文件（实质改动文件 1 个，表面改动文件 0 个，新增测试 +0 行）
- **关联 Issue 对齐**：已针对性修复 #56 孪生行重复计数缺陷
- **核心改动摘要**：把 pending 单槽改为按 twin_key 索引的字典，折叠 fixpipe 孪生行，修复 UB 写重复计数
  - SQL 按 CoreId 排序使孪生行不相邻，改用 twin_key 字典匹配，逻辑正确且注释到位
  - 评审建议将指令 ID 纳入 twin_key，避免地址/时刻/大小相同的两次写被误合并
  - 缺少 ci-pipeline-passed 门禁标签，也未新增覆盖该折叠路径的单元测试
- **committer 建议动作**：**暂缓合入：需补齐 ci-pipeline-passed，并回应评审的 key 收紧建议**

### PR #59：fix(record): recognize versioned Python executables

- **作者**：`@liangjinxuan-2026` · **停留自然时长**：231.7h · **AI 判定**：**🤖 值得合入**
- **代码规模**：1 个文件（实质改动文件 1 个，表面改动文件 0 个，新增测试 +0 行）
- **关联 Issue 对齐**：针对性修复 #60 版本化解释器漏判
- **核心改动摘要**：用正则统一识别 python3.11 等版本化解释器并修正 Python 路径判定
  - 将 _PYTHON_COMMAND 改为正则，覆盖 python、python2/3、python3.11、pytest 等命名
  - 同步收敛解释器与 Python 前缀集合，避免两处判定逻辑漂移
  - 作者已同步 master、解决冲突并完成 CPU 验证（11 项测试通过）；建议后续补单测固化
- **committer 建议动作**：**CLA 与 CI 均通过且无冲突，建议直接合入**

### PR #58：fix(report): handle detector output write failures

- **作者**：`@liangjinxuan-2026` · **停留自然时长**：231.7h · **AI 判定**：**🤖 值得合入**
- **代码规模**：2 个文件（实质改动文件 2 个，表面改动文件 0 个，新增测试 +39 行）
- **关联 Issue 对齐**：已关联 #59
- **核心改动摘要**：实质代码改动（2 文件 +63/-28），门禁全绿
  - 守卫判定：substantive_diff: 2 file(s); adds_tests; linked_issue_legit: #59; external_participant: ZhouBX
- **committer 建议动作**：**CLA 与 CI 已通过，建议 committer 完成最终代码检视后合入**

