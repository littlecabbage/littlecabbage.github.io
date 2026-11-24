# PR & Issue 智能治理 Review 报告 · cann/npu-simulator

| 维度 | 详情 |
|---|---|
| **目标仓库** | [cann/npu-simulator](https://gitcode.com/cann/npu-simulator)（GitCode） |
| **巡检时间** | 2026-11-24 13:39 (UTC+8) |
| **分析引擎** | `gitcode-issue-triage` 确定性守卫 + Pi Agent (`cannbot/deepseek-v4.1-flash`) |
| **判定原则** | 宁漏勿错：强灌水信号 + 无安全否决 → 低价值候选；有任何实质代码/测试/关联 Issue → 保留并给出合路建议 |

---

## 一、执行摘要（供 on-call & committer 速览）

- **Issue 巡检**：共扫描 **66** 条 Issue，判定 KEEP **65** / CLOSE 候选 **0** / 待人工复核 **1**。
- **Open PR 总览（共 10 个）**：
  - ✅ **可立即合入（5 个）**：#75、#74、#73、#59、#58
  - ⚠️ **实质贡献但门禁阻塞（5 个）**：#72、#70、#67、#64、#60
  - 🧹 **低价值/表面改动候选（0 个）**：无

## 二、Open PR 逐条深度评审与行动清单

| PR | AI 结论 | 合路门禁 | 关联 Issue | 改动规模 (实质文件) | AI 改动摘要与关联对齐 | committer 建议动作 |
|---|---|---|---|---|---|---|
| [#75](https://gitcode.com/cann/npu-simulator/pulls/75) | **🤖 值得合入** | ✅ 可合入 | — | +0/-14 (2/2 实质) | 删除 dashboard 未引用的 _bar 辅助函数与测试中重复的 _parse 定义（无关联 Issue，属无行为变更的代码清理） | CLA 与 CI 均已通过且无冲突，建议直接合入 |
| [#74](https://gitcode.com/cann/npu-simulator/pulls/74) | **🤖 值得合入** | ✅ 可合入 | — | +17/-14 (6/7 实质) | 修正prof指标键名写反、日志f-string错误并加除零越界防护（无关联Issue，属作者自查缺陷修复） | CLA已签、CI全绿且无冲突，建议直接合入 |
| [#73](https://gitcode.com/cann/npu-simulator/pulls/73) | **🤖 值得合入** | ✅ 可合入 | [#61](https://gitcode.com/cann/npu-simulator/issues/61) | +3/-3 (3/3 实质) | 修正CI脚本中仓库名残留，并清理bandit失效路径配置（精准修复 #61 仓库名复制残留缺陷） | CLA与CI均通过且无冲突，建议直接合入 |
| [#72](https://gitcode.com/cann/npu-simulator/pulls/72) | **🤖 阻塞待解** | ❌ CLA 未签 (cann-cla/no)；缺 cann-cla/yes；缺 ci-pipeline-passed；阻塞标签 stat/needs-squash | — | +80/-0 (2/2 实质) | CI 新增 md_check 静态检查复用 workflow 及流水线任务（无关联 Issue，属 CI 门禁能力增强） | 需先签署 CLA、压缩提交并跑通 CI 后再评审合入 |
| [#70](https://gitcode.com/cann/npu-simulator/pulls/70) | **🤖 阻塞待解** | ❌ 缺 ci-pipeline-passed | [#66](https://gitcode.com/cann/npu-simulator/issues/66) | +5/-5 (0/2 实质) | 修正两份最佳实践文档中英文间距，提升中文可读性（已针对性修复 #66 列明的 5 处间距问题） | 文档改动无害，需等待 ci-pipeline-passed 打标后合入 |
| [#67](https://gitcode.com/cann/npu-simulator/pulls/67) | **🤖 阻塞待解** | ❌ 阻塞标签 stat/needs-squash | [#63](https://gitcode.com/cann/npu-simulator/issues/63) | +67/-145 (11/11 实质) | 移除独立 roofline JSON 导出，可选处理失败时保留基础报告（已针对性修复 #63 报告导出失败缺陷） | 已有 approve，需先 squash 提交解除 needs-squash 阻塞再合入 |
| [#64](https://gitcode.com/cann/npu-simulator/pulls/64) | **🤖 阻塞待解** | ❌ 阻塞标签 stat/needs-squash | — | +330/-2 (6/6 实质) | 新增 SOL 分析器与 --sol 选项，评估内核吞吐上限（无关联 Issue，新特性未先走方案讨论） | 需作者 squash 提交、补测试并关联 Issue 后再评审 |
| [#60](https://gitcode.com/cann/npu-simulator/pulls/60) | **🤖 阻塞待解** | ❌ 缺 ci-pipeline-passed | [#56](https://gitcode.com/cann/npu-simulator/issues/56) | +11/-5 (1/1 实质) | 把 pending 单槽改为按 twin_key 索引的字典，折叠 fixpipe 孪生行，修复 UB 写重复计数（已针对性修复 #56 孪生行重复计数缺陷） | 暂缓合入：需补齐 ci-pipeline-passed，并回应评审的 key 收紧建议 |
| [#59](https://gitcode.com/cann/npu-simulator/pulls/59) | **🤖 值得合入** | ✅ 可合入 | [#60](https://gitcode.com/cann/npu-simulator/issues/60) | +14/-16 (1/1 实质) | 用正则统一识别 python3.11 等版本化解释器并修正 Python 路径判定（针对性修复 #60 版本化解释器漏判） | CLA 与 CI 均通过且无冲突，建议直接合入 |
| [#58](https://gitcode.com/cann/npu-simulator/pulls/58) | **🤖 值得合入** | ✅ 可合入 | [#59](https://gitcode.com/cann/npu-simulator/issues/59) | +63/-28 (2/2 实质) | 实质代码改动（2 文件 +63/-28），门禁全绿（已关联 #59） | CLA 与 CI 已通过，建议 committer 完成最终代码检视后合入 |

### PR #75：refactor: remove unused _bar helper and duplicate _parse definition

- **作者**：`@qunzhongjia` · **停留自然时长**：0.4h · **AI 判定**：**🤖 值得合入**
- **代码规模**：2 个文件（实质改动文件 2 个，表面改动文件 0 个，新增测试 +0 行）
- **关联 Issue 对齐**：无关联 Issue，属无行为变更的代码清理
- **核心改动摘要**：删除 dashboard 未引用的 _bar 辅助函数与测试中重复的 _parse 定义
  - _bar 为嵌套局部函数且无任何调用点，删除不影响盒线渲染逻辑
  - test_config.py 中 _parse 重复定义且实现一致，去重后测试语义不变
- **committer 建议动作**：**CLA 与 CI 均已通过且无冲突，建议直接合入**

### PR #74：fix(prof): fix AIV1 overlap label, SIMT f-string log, and analyzer guards

- **作者**：`@qunzhongjia` · **停留自然时长**：0.4h · **AI 判定**：**🤖 值得合入**
- **代码规模**：7 个文件（实质改动文件 6 个，表面改动文件 0 个，新增测试 +0 行）
- **关联 Issue 对齐**：无关联Issue，属作者自查缺陷修复
- **核心改动摘要**：修正prof指标键名写反、日志f-string错误并加除零越界防护
  - summary_reporter与demo同步修正AIV1_SCALAR_vs_AIV1_VEC键名，修复指标重叠统计错误
  - arch_diagram与elf_object_reader增加除零、空列表防护，runner改遍历副本避免移除异常
- **committer 建议动作**：**CLA已签、CI全绿且无冲突，建议直接合入**

### PR #73：fix(ci): update REPOSITORY_NAME to npu-simulator and remove stale bandit path

- **作者**：`@qunzhongjia` · **停留自然时长**：0.5h · **AI 判定**：**🤖 值得合入**
- **代码规模**：3 个文件（实质改动文件 3 个，表面改动文件 0 个，新增测试 +0 行）
- **关联 Issue 对齐**：精准修复 #61 仓库名复制残留缺陷
- **核心改动摘要**：修正CI脚本中仓库名残留，并清理bandit失效路径配置
  - 将 compile.sh 与 ut.sh 中误写的 REPOSITORY_NAME="ops-math" 改为 npu-simulator，修正日志与断言中的仓库标识
  - 从 .pre-commit-config.yaml 的 bandit 参数中移除不存在的 prof_demo/ 根路径，避免检查报错
- **committer 建议动作**：**CLA与CI均通过且无冲突，建议直接合入**

### PR #72：CI 添加StaticCheck_md_check检查项

- **作者**：`@zhouchongshun` · **停留自然时长**：20.9h · **AI 判定**：**🤖 阻塞待解**
- **代码规模**：2 个文件（实质改动文件 2 个，表面改动文件 0 个，新增测试 +0 行）
- **关联 Issue 对齐**：无关联 Issue，属 CI 门禁能力增强
- **核心改动摘要**：CI 新增 md_check 静态检查复用 workflow 及流水线任务
  - 新增 workflow_call 复用模板并接入 CodeCheck 阶段，结构合理，但需确认 md_check 镜像版本来源
  - workflow 名称拼写为 staticheck_action，且启用 allow-unsafe-pr-checkout，需复核安全性
- **committer 建议动作**：**需先签署 CLA、压缩提交并跑通 CI 后再评审合入**

### PR #70：docs(npu-simulator): fix spacing in examples

- **作者**：`@gcw_WJCkAUuk` · **停留自然时长**：56.4h · **AI 判定**：**🤖 阻塞待解**
- **代码规模**：2 个文件（实质改动文件 0 个，表面改动文件 0 个，新增测试 +0 行）
- **关联 Issue 对齐**：已针对性修复 #66 列明的 5 处间距问题
- **核心改动摘要**：修正两份最佳实践文档中英文间距，提升中文可读性
  - 纯文档改动，仅调中英文空格，未改示例命令、参数或技术语义，无回归风险
  - Issue 标题称 26 项但正文仅列 5 项，本 MR 已覆盖全部可核验条目，剩余项需后续 Issue 补充
- **committer 建议动作**：**文档改动无害，需等待 ci-pipeline-passed 打标后合入**

### PR #67：fix(prof): preserve base reports when optional processing fails

- **作者**：`@churkinaleksandr` · **停留自然时长**：111.2h · **AI 判定**：**🤖 阻塞待解**
- **代码规模**：11 个文件（实质改动文件 11 个，表面改动文件 0 个，新增测试 +15 行）
- **关联 Issue 对齐**：已针对性修复 #63 报告导出失败缺陷
- **核心改动摘要**：移除独立 roofline JSON 导出，可选处理失败时保留基础报告
  - hotspots_processor 用临时目录生成 Critical Path，失败仅告警不中断基础报告
  - device ELF 解码失败改为告警并继续处理该 launch，避免整体流程中断
  - 删除 roofline_reporter.py 及独立 JSON 导出，改由 SQLite 表与 CSV 承载结果
  - 同步更新 command_line_features 等文档，并补充基础报告连续性单测
- **committer 建议动作**：**已有 approve，需先 squash 提交解除 needs-squash 阻塞再合入**

### PR #64：Add Speed-of-light profiling feature

- **作者**：`@fomichevoleg5` · **停留自然时长**：158.9h · **AI 判定**：**🤖 阻塞待解**
- **代码规模**：6 个文件（实质改动文件 6 个，表面改动文件 0 个，新增测试 +0 行）
- **关联 Issue 对齐**：无关联 Issue，新特性未先走方案讨论
- **核心改动摘要**：新增 SOL 分析器与 --sol 选项，评估内核吞吐上限
  - 新增 276 行 SOL 分析器和峰值常量表，需确认 V100 以外架构取值来源
  - report 契约版本放宽到 7 或 8，需评估向后兼容与迁移说明
  - 本次无新增测试文件覆盖，建议补 SpeedOfLightData 生成用例
- **committer 建议动作**：**需作者 squash 提交、补测试并关联 Issue 后再评审**

### PR #60：fix(report): collapse the fixpipe twin rows by identity, not by adjacency

- **作者**：`@gcw_EkTYFH3T` · **停留自然时长**：206.3h · **AI 判定**：**🤖 阻塞待解**
- **代码规模**：1 个文件（实质改动文件 1 个，表面改动文件 0 个，新增测试 +0 行）
- **关联 Issue 对齐**：已针对性修复 #56 孪生行重复计数缺陷
- **核心改动摘要**：把 pending 单槽改为按 twin_key 索引的字典，折叠 fixpipe 孪生行，修复 UB 写重复计数
  - SQL 按 CoreId 排序使孪生行不相邻，改用 twin_key 字典匹配，逻辑正确且注释到位
  - 评审建议将指令 ID 纳入 twin_key，避免地址/时刻/大小相同的两次写被误合并
  - 缺少 ci-pipeline-passed 门禁标签，也未新增覆盖该折叠路径的单元测试
- **committer 建议动作**：**暂缓合入：需补齐 ci-pipeline-passed，并回应评审的 key 收紧建议**

### PR #59：fix(record): recognize versioned Python executables

- **作者**：`@liangjinxuan-2026` · **停留自然时长**：232.7h · **AI 判定**：**🤖 值得合入**
- **代码规模**：1 个文件（实质改动文件 1 个，表面改动文件 0 个，新增测试 +0 行）
- **关联 Issue 对齐**：针对性修复 #60 版本化解释器漏判
- **核心改动摘要**：用正则统一识别 python3.11 等版本化解释器并修正 Python 路径判定
  - 将 _PYTHON_COMMAND 改为正则，覆盖 python、python2/3、python3.11、pytest 等命名
  - 同步收敛解释器与 Python 前缀集合，避免两处判定逻辑漂移
  - 作者已同步 master、解决冲突并完成 CPU 验证（11 项测试通过）；建议后续补单测固化
- **committer 建议动作**：**CLA 与 CI 均通过且无冲突，建议直接合入**

### PR #58：fix(report): handle detector output write failures

- **作者**：`@liangjinxuan-2026` · **停留自然时长**：232.7h · **AI 判定**：**🤖 值得合入**
- **代码规模**：2 个文件（实质改动文件 2 个，表面改动文件 0 个，新增测试 +39 行）
- **关联 Issue 对齐**：已关联 #59
- **核心改动摘要**：实质代码改动（2 文件 +63/-28），门禁全绿
  - 守卫判定：substantive_diff: 2 file(s); adds_tests; linked_issue_legit: #59; external_participant: ZhouBX
- **committer 建议动作**：**CLA 与 CI 已通过，建议 committer 完成最终代码检视后合入**

