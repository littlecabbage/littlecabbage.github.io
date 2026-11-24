# PR & Issue 智能治理 Review 报告 · cann/npu-simulator

| 维度 | 详情 |
|---|---|
| **目标仓库** | [cann/npu-simulator](https://gitcode.com/cann/npu-simulator)（GitCode） |
| **巡检时间** | 2026-11-24 21:38 (UTC+8) |
| **分析引擎** | `gitcode-issue-triage` 确定性守卫 + Pi Agent (`cannbot/deepseek-v4.1-flash`) |
| **判定原则** | 宁漏勿错：强灌水信号 + 无安全否决 → 低价值候选；有任何实质代码/测试/关联 Issue → 保留并给出合路建议 |

---

## 一、执行摘要（供 on-call & committer 速览）

- **Issue 巡检**：共扫描 **70** 条 Issue，判定 KEEP **69** / CLOSE 候选 **0** / 待人工复核 **1**。
- **Open PR 总览（共 10 个）**：
  - ✅ **可立即合入（5 个）**：#75、#74、#73、#70、#59
  - ⚠️ **实质贡献但门禁阻塞（5 个）**：#77、#76、#72、#64、#60
  - 🧹 **低价值/表面改动候选（0 个）**：无

## 二、Open PR 逐条深度评审与行动清单

| PR | AI 结论 | 合路门禁 | 关联 Issue | 改动规模 (实质文件) | AI 改动摘要与关联对齐 | committer 建议动作 |
|---|---|---|---|---|---|---|
| [#77](https://gitcode.com/cann/npu-simulator/pulls/77) | **🤖 阻塞待解** | ❌ 缺 ci-pipeline-passed | [#68](https://gitcode.com/cann/npu-simulator/issues/68) | +2/-0 (1/1 实质) | README 补两行说明 cannsim 为分发名、与 npusim 共用 CLI（针对性澄清 #68 中 cannsim 命名疑问） | 需先补齐 ci-pipeline-passed 门禁后即可合入 |
| [#76](https://gitcode.com/cann/npu-simulator/pulls/76) | **🤖 阻塞待解** | ❌ 缺 ci-pipeline-passed | [#67](https://gitcode.com/cann/npu-simulator/issues/67) | +2/-22 (2/2 实质) | 清理 CI 脚本中 ops-math/ge 拷贝残留的冗余代码与死函数（针对性修复 #67 脚本冗余项清理） | 需作者补齐 ci-pipeline-passed 门禁并确认脚本语法通过后再合入 |
| [#75](https://gitcode.com/cann/npu-simulator/pulls/75) | **🤖 值得合入** | ✅ 可合入 | — | +0/-14 (2/2 实质) | 删除 dashboard 未引用的 _bar 辅助函数及测试中重复的 _parse 定义（无关联 Issue，纯代码清理重构） | CLA 与 CI 均已通过且无冲突，建议直接合入 |
| [#74](https://gitcode.com/cann/npu-simulator/pulls/74) | **🤖 值得合入** | ✅ 可合入 | — | +17/-14 (6/7 实质) | 修复AIV1指标键名写错、日志f-string及除零越界防护（无关联Issue，属自发现缺陷修复） | CLA与CI均通过、无冲突，建议直接合入 |
| [#73](https://gitcode.com/cann/npu-simulator/pulls/73) | **🤖 值得合入** | ✅ 可合入 | [#61](https://gitcode.com/cann/npu-simulator/issues/61) | +3/-3 (3/3 实质) | 修正CI脚本仓库名残留并移除bandit失效路径（已针对性修复#61仓库名误标缺陷） | cann-cla与CI门禁全绿，建议直接合入 |
| [#72](https://gitcode.com/cann/npu-simulator/pulls/72) | **🤖 阻塞待解** | ❌ CLA 未签 (cann-cla/no)；缺 cann-cla/yes；缺 ci-pipeline-passed；阻塞标签 stat/needs-squash | — | +80/-0 (2/2 实质) | CI 新增 StaticCheck md_check 复用 workflow 并接入 CodeCheck 阶段（无关联 Issue，按 PR 描述新增 CI 检查） | 请作者修正拼写、签 CLA 并 squash 后重跑 CI |
| [#70](https://gitcode.com/cann/npu-simulator/pulls/70) | **🤖 值得合入** | ✅ 可合入 | [#66](https://gitcode.com/cann/npu-simulator/issues/66) | +5/-5 (0/2 实质) | 修复两份中文最佳实践文档中英文间距问题（已针对性修复 #66 列明的间距问题） | CLA 与 CI 均通过、无冲突，建议直接合入 |
| [#64](https://gitcode.com/cann/npu-simulator/pulls/64) | **🤖 阻塞待解** | ❌ 缺 ci-pipeline-passed；阻塞标签 stat/needs-squash | — | +571/-10 (13/13 实质) | 新增 SOL 性能分析特性，含 --sol 选项、分析器、建表与文档测试（无关联 Issue，新特性缺方案讨论） | 需先补关联 Issue 与 CI 通过，并 squash 为单提交 |
| [#60](https://gitcode.com/cann/npu-simulator/pulls/60) | **🤖 阻塞待解** | ❌ 缺 ci-pipeline-passed | [#56](https://gitcode.com/cann/npu-simulator/issues/56) | +11/-5 (1/1 实质) | 把 pending 单槽改为按 twin_key 索引的字典，折叠 fixpipe 孪生行，修复 UB 写重复计数（已针对性修复 #56 孪生行重复计数缺陷） | 暂缓合入：需补齐 ci-pipeline-passed，并回应评审的 key 收紧建议 |
| [#59](https://gitcode.com/cann/npu-simulator/pulls/59) | **🤖 值得合入** | ✅ 可合入 | [#60](https://gitcode.com/cann/npu-simulator/issues/60) | +14/-16 (1/1 实质) | 用正则统一识别 python3.11 等版本化解释器并修正 Python 路径判定（针对性修复 #60 版本化解释器漏判） | CLA 与 CI 均通过且无冲突，建议直接合入 |

### PR #77：docs: clarify cannsim package and CLI aliases

- **作者**：`@lilong555` · **停留自然时长**：0.6h · **AI 判定**：**🤖 阻塞待解**
- **代码规模**：1 个文件（实质改动文件 1 个，表面改动文件 0 个，新增测试 +0 行）
- **关联 Issue 对齐**：针对性澄清 #68 中 cannsim 命名疑问
- **核心改动摘要**：README 补两行说明 cannsim 为分发名、与 npusim 共用 CLI
  - 仅文档新增两行，说明 wheel 分发名与 CLI 入口别名，不改代码与构建
  - 已具 cann-cla/yes，但缺 ci-pipeline-passed，需重跑 CI 再评审
- **committer 建议动作**：**需先补齐 ci-pipeline-passed 门禁后即可合入**

### PR #76：删除冗余代码

- **作者**：`@cui_jiahao` · **停留自然时长**：1.9h · **AI 判定**：**🤖 阻塞待解**
- **代码规模**：2 个文件（实质改动文件 2 个，表面改动文件 0 个，新增测试 +0 行）
- **关联 Issue 对齐**：针对性修复 #67 脚本冗余项清理
- **核心改动摘要**：清理 CI 脚本中 ops-math/ge 拷贝残留的冗余代码与死函数
  - 已修正 REPOSITORY_NAME 仓名错误，删除未使用的 LOG_HEAD 死函数与 ge_st_rt2 死打印，属实质清理
  - 仅缺 ci-pipeline-passed 标签；建议补跑流水线确认 compile.sh/ut.sh 语法与 UT 不受影响
- **committer 建议动作**：**需作者补齐 ci-pipeline-passed 门禁并确认脚本语法通过后再合入**

### PR #75：refactor: remove unused _bar helper and duplicate _parse definition

- **作者**：`@qunzhongjia` · **停留自然时长**：8.4h · **AI 判定**：**🤖 值得合入**
- **代码规模**：2 个文件（实质改动文件 2 个，表面改动文件 0 个，新增测试 +0 行）
- **关联 Issue 对齐**：无关联 Issue，纯代码清理重构
- **核心改动摘要**：删除 dashboard 未引用的 _bar 辅助函数及测试中重复的 _parse 定义
  - _bar 定义后无任何调用点，删除后不影响分隔行渲染逻辑，属安全清理
  - test_config.py 中 _parse 重复定义且实现完全一致，去重可避免维护歧义
- **committer 建议动作**：**CLA 与 CI 均已通过且无冲突，建议直接合入**

### PR #74：fix(prof): fix AIV1 overlap label, SIMT f-string log, and analyzer guards

- **作者**：`@qunzhongjia` · **停留自然时长**：8.4h · **AI 判定**：**🤖 值得合入**
- **代码规模**：7 个文件（实质改动文件 6 个，表面改动文件 0 个，新增测试 +0 行）
- **关联 Issue 对齐**：无关联Issue，属自发现缺陷修复
- **核心改动摘要**：修复AIV1指标键名写错、日志f-string及除零越界防护
  - 修正AIV1_SCALAR与AIV1_VEC重叠键被误写为AIV0_VEC的复制粘贴错误，同步两处reporter
  - 补充除零/空列表越界防护、f-string花括号、枚举整型比较与handler遍历安全
- **committer 建议动作**：**CLA与CI均通过、无冲突，建议直接合入**

### PR #73：fix(ci): update REPOSITORY_NAME to npu-simulator and remove stale bandit path

- **作者**：`@qunzhongjia` · **停留自然时长**：8.5h · **AI 判定**：**🤖 值得合入**
- **代码规模**：3 个文件（实质改动文件 3 个，表面改动文件 0 个，新增测试 +0 行）
- **关联 Issue 对齐**：已针对性修复#61仓库名误标缺陷
- **核心改动摘要**：修正CI脚本仓库名残留并移除bandit失效路径
  - compile.sh 与 ut.sh 中 REPOSITORY_NAME 由 ops-math 改为 npu-simulator，修复日志与断言误标
  - 移除 .pre-commit-config.yaml 中不存在的 prof_demo/ 路径，避免 bandit 因路径失效报错
- **committer 建议动作**：**cann-cla与CI门禁全绿，建议直接合入**

### PR #72：CI 添加StaticCheck_md_check检查项

- **作者**：`@zhouchongshun` · **停留自然时长**：28.9h · **AI 判定**：**🤖 阻塞待解**
- **代码规模**：2 个文件（实质改动文件 2 个，表面改动文件 0 个，新增测试 +0 行）
- **关联 Issue 对齐**：无关联 Issue，按 PR 描述新增 CI 检查
- **核心改动摘要**：CI 新增 StaticCheck md_check 复用 workflow 并接入 CodeCheck 阶段
  - 新增 staticcheck_action.yml 复用工作流并在主流水线注册 md_check 作业，方向合理
  - workflow 名称拼写 staticheck_action 需按评审意见改为 staticcheck
  - JOB_staticcheck_md_check 依赖 jobs.JOB_image.outputs.staticcheck，需确认该镜像变量已定义
  - 存在 cann-cla/no 与 stat/needs-squash，需签 CLA、压缩提交并通过 CI
- **committer 建议动作**：**请作者修正拼写、签 CLA 并 squash 后重跑 CI**

### PR #70：docs(npu-simulator): fix spacing in examples

- **作者**：`@gcw_WJCkAUuk` · **停留自然时长**：64.4h · **AI 判定**：**🤖 值得合入**
- **代码规模**：2 个文件（实质改动文件 0 个，表面改动文件 0 个，新增测试 +0 行）
- **关联 Issue 对齐**：已针对性修复 #66 列明的间距问题
- **核心改动摘要**：修复两份中文最佳实践文档中英文间距问题
  - 仅调整两文件 5 处中英文空格，未改示例命令与技术语义，风险极低
  - 纯文档改动无需编译与 UT，git diff --check 通过；标题 26 项与正文 5 项差异已在 Issue 留言说明
- **committer 建议动作**：**CLA 与 CI 均通过、无冲突，建议直接合入**

### PR #64：Add Speed-of-light profiling feature

- **作者**：`@fomichevoleg5` · **停留自然时长**：166.9h · **AI 判定**：**🤖 阻塞待解**
- **代码规模**：13 个文件（实质改动文件 13 个，表面改动文件 0 个，新增测试 +20 行）
- **关联 Issue 对齐**：无关联 Issue，新特性缺方案讨论
- **核心改动摘要**：新增 SOL 性能分析特性，含 --sol 选项、分析器、建表与文档测试
  - 新增 281 行 SpeedOfLightAnalyzer 与 SpeedOfLightData 表，需确认峰值参数来源与校准依据
  - report.py 放开 contract_version 至 7/8，须保证旧库兼容与版本升级路径清晰
  - PR 模板 CLA/测试/评审勾选项均未勾选，且缺少 ci-pipeline-passed 标签
  - 已有 2 个测试文件覆盖 --sol 与 ddr 采集依赖，但需补分析器输出数值校验用例
- **committer 建议动作**：**需先补关联 Issue 与 CI 通过，并 squash 为单提交**

### PR #60：fix(report): collapse the fixpipe twin rows by identity, not by adjacency

- **作者**：`@gcw_EkTYFH3T` · **停留自然时长**：214.3h · **AI 判定**：**🤖 阻塞待解**
- **代码规模**：1 个文件（实质改动文件 1 个，表面改动文件 0 个，新增测试 +0 行）
- **关联 Issue 对齐**：已针对性修复 #56 孪生行重复计数缺陷
- **核心改动摘要**：把 pending 单槽改为按 twin_key 索引的字典，折叠 fixpipe 孪生行，修复 UB 写重复计数
  - SQL 按 CoreId 排序使孪生行不相邻，改用 twin_key 字典匹配，逻辑正确且注释到位
  - 评审建议将指令 ID 纳入 twin_key，避免地址/时刻/大小相同的两次写被误合并
  - 缺少 ci-pipeline-passed 门禁标签，也未新增覆盖该折叠路径的单元测试
- **committer 建议动作**：**暂缓合入：需补齐 ci-pipeline-passed，并回应评审的 key 收紧建议**

### PR #59：fix(record): recognize versioned Python executables

- **作者**：`@liangjinxuan-2026` · **停留自然时长**：240.7h · **AI 判定**：**🤖 值得合入**
- **代码规模**：1 个文件（实质改动文件 1 个，表面改动文件 0 个，新增测试 +0 行）
- **关联 Issue 对齐**：针对性修复 #60 版本化解释器漏判
- **核心改动摘要**：用正则统一识别 python3.11 等版本化解释器并修正 Python 路径判定
  - 将 _PYTHON_COMMAND 改为正则，覆盖 python、python2/3、python3.11、pytest 等命名
  - 同步收敛解释器与 Python 前缀集合，避免两处判定逻辑漂移
  - 作者已同步 master、解决冲突并完成 CPU 验证（11 项测试通过）；建议后续补单测固化
- **committer 建议动作**：**CLA 与 CI 均通过且无冲突，建议直接合入**

