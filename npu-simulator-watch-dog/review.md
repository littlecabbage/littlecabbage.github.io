# PR & Issue 智能治理 Review 报告 · cann/npu-simulator

| 维度 | 详情 |
|---|---|
| **目标仓库** | [cann/npu-simulator](https://gitcode.com/cann/npu-simulator)（GitCode） |
| **巡检时间** | 2026-11-25 12:38 (UTC+8) |
| **分析引擎** | `gitcode-issue-triage` 确定性守卫 + Pi Agent (`cannbot/deepseek-v4.1-flash`) |
| **判定原则** | 宁漏勿错：强灌水信号 + 无安全否决 → 低价值候选；有任何实质代码/测试/关联 Issue → 保留并给出合路建议 |

---

## 一、执行摘要（供 on-call & committer 速览）

- **Issue 巡检**：共扫描 **73** 条 Issue，判定 KEEP **72** / CLOSE 候选 **0** / 待人工复核 **1**。
- **Open PR 总览（共 11 个）**：
  - ✅ **可立即合入（7 个）**：#80、#76、#75、#74、#73、#70、#59
  - ⚠️ **实质贡献但门禁阻塞（4 个）**：#78、#77、#72、#60
  - 🧹 **低价值/表面改动候选（0 个）**：无

## 二、Open PR 逐条深度评审与行动清单

| PR | AI 结论 | 合路门禁 | 关联 Issue | 改动规模 (实质文件) | AI 改动摘要与关联对齐 | committer 建议动作 |
|---|---|---|---|---|---|---|
| [#80](https://gitcode.com/cann/npu-simulator/pulls/80) | **🤖 值得合入** | ✅ 可合入 | — | +2/-2 (1/1 实质) | 修改启动 banner 常量，引导地址由发布讨论帖改为开源仓库首页（针对性修复 #73 引导地址失效） | CLA 与 CI 均通过、无冲突，建议直接合入 |
| [#78](https://gitcode.com/cann/npu-simulator/pulls/78) | **🤖 阻塞待解** | ❌ 缺 ci-pipeline-passed；阻塞标签 stat/needs-squash | — | +571/-10 (13/13 实质) | 新增 SOL 分析器、--sol 选项、表结构与文档及测试（无关联 Issue，需补方案讨论） | 需修复 CI 失败、压缩提交并重跑门禁后再合入 |
| [#77](https://gitcode.com/cann/npu-simulator/pulls/77) | **🤖 阻塞待解** | ❌ 缺 ci-pipeline-passed | [#68](https://gitcode.com/cann/npu-simulator/issues/68) | +2/-0 (1/1 实质) | README 补两行说明 cannsim 为分发名、与 npusim 共用 CLI（针对性澄清 #68 中 cannsim 命名疑问） | 需先补齐 ci-pipeline-passed 门禁后即可合入 |
| [#76](https://gitcode.com/cann/npu-simulator/pulls/76) | **🤖 值得合入** | ✅ 可合入 (已 approved) | [#67](https://gitcode.com/cann/npu-simulator/issues/67) | +2/-22 (2/2 实质) | 清理 compile.sh/ut.sh 中 GE/ops-math 拷贝残留死代码并修正仓库名（已针对性修复 #67 脚本冗余清理） | 已获 approved/lgtm 且门禁全绿，建议直接合入 |
| [#75](https://gitcode.com/cann/npu-simulator/pulls/75) | **🤖 值得合入** | ✅ 可合入 | — | +0/-14 (2/2 实质) | 删除 dashboard 未引用的 _bar 辅助函数及测试中重复的 _parse 定义（无关联 Issue，纯代码清理重构） | CLA 与 CI 均已通过且无冲突，建议直接合入 |
| [#74](https://gitcode.com/cann/npu-simulator/pulls/74) | **🤖 值得合入** | ✅ 可合入 | — | +17/-14 (6/7 实质) | 修正AIV1指标键名复制错误，并补除零、越界与日志异常防护（无关联Issue，为自主发现的缺陷修复） | CLA与CI均通过，采纳检视建议后可合入 |
| [#73](https://gitcode.com/cann/npu-simulator/pulls/73) | **🤖 值得合入** | ✅ 可合入 | [#61](https://gitcode.com/cann/npu-simulator/issues/61) | +3/-3 (3/3 实质) | 修正 CI 脚本中仓库名的复制残留，并清理 bandit 的无效路径（已针对性修复 #61 配置残留问题） | CLA（贡献者许可协议）与 CI 检查全绿且无冲突，建议直接合入 |
| [#72](https://gitcode.com/cann/npu-simulator/pulls/72) | **🤖 阻塞待解** | ❌ CLA 未签 (cann-cla/no)；缺 cann-cla/yes；缺 ci-pipeline-passed；阻塞标签 stat/needs-squash | — | +80/-0 (2/2 实质) | 实质改动（2 文件 +80/-0），当前存在合路阻塞（无关联 Issue） | 解决门禁阻塞（cla_not_signed(cann-cla/no)、missing_label:cann-cla/yes、missing_label:ci-pipeline-passed、blocking_label:stat/needs-squash）后再推进合入 |
| [#70](https://gitcode.com/cann/npu-simulator/pulls/70) | **🤖 值得合入** | ✅ 可合入 | [#66](https://gitcode.com/cann/npu-simulator/issues/66) | +5/-5 (0/2 实质) | 修复两份中文最佳实践文档中英文间距问题（已针对性修复 #66 列明的间距问题） | CLA 与 CI 均通过、无冲突，建议直接合入 |
| [#60](https://gitcode.com/cann/npu-simulator/pulls/60) | **🤖 阻塞待解** | ❌ 缺 ci-pipeline-passed | [#56](https://gitcode.com/cann/npu-simulator/issues/56) | +11/-5 (1/1 实质) | 按 twin_key 字典折叠 fixpipe 孪生行，修复 UB 写重复计数（已针对性修复 #56 孪生行重复计入缺陷） | 需补跑 CI 取得 ci-pipeline-passed 标签后再合入 |
| [#59](https://gitcode.com/cann/npu-simulator/pulls/59) | **🤖 值得合入** | ✅ 可合入 | [#60](https://gitcode.com/cann/npu-simulator/issues/60) | +14/-16 (1/1 实质) | 用正则识别版本化 Python 解释器，修复记录启动路径分类错误（已针对性修复 #60 版本化解释器识别缺陷） | CLA 与 CI 均通过且冲突已解，建议合入并跟进 ABI 后缀建议 |

### PR #80：chore(comm): 欢迎页引导地址改为开源仓库

- **作者**：`@zengzihui` · **停留自然时长**：1.2h · **AI 判定**：**🤖 值得合入**
- **代码规模**：1 个文件（实质改动文件 1 个，表面改动文件 0 个，新增测试 +0 行）
- **关联 Issue 对齐**：针对性修复 #73 引导地址失效
- **核心改动摘要**：修改启动 banner 常量，引导地址由发布讨论帖改为开源仓库首页
  - 仅替换 welcome 字符串两行，无逻辑变更，风险极低
  - 全仓仅此一处引用，无测试依赖，新地址长期有效
- **committer 建议动作**：**CLA 与 CI 均通过、无冲突，建议直接合入**

### PR #78：Add Speed-of-light profiling feature

- **作者**：`@fomichevoleg5` · **停留自然时长**：13.7h · **AI 判定**：**🤖 阻塞待解**
- **代码规模**：13 个文件（实质改动文件 13 个，表面改动文件 0 个，新增测试 +20 行）
- **关联 Issue 对齐**：无关联 Issue，需补方案讨论
- **核心改动摘要**：新增 SOL 分析器、--sol 选项、表结构与文档及测试
  - contract version 放宽接受 7/8，需说明 version 7 缺 SOL 表时的降级处理
  - CUBE/VECTOR 计算缺异常保护，且 MMAD 查询未按 CoreTypeId 过滤，SOL 口径可能失真
- **committer 建议动作**：**需修复 CI 失败、压缩提交并重跑门禁后再合入**

### PR #77：docs: clarify cannsim package and CLI aliases

- **作者**：`@lilong555` · **停留自然时长**：15.6h · **AI 判定**：**🤖 阻塞待解**
- **代码规模**：1 个文件（实质改动文件 1 个，表面改动文件 0 个，新增测试 +0 行）
- **关联 Issue 对齐**：针对性澄清 #68 中 cannsim 命名疑问
- **核心改动摘要**：README 补两行说明 cannsim 为分发名、与 npusim 共用 CLI
  - 仅文档新增两行，说明 wheel 分发名与 CLI 入口别名，不改代码与构建
  - 已具 cann-cla/yes，但缺 ci-pipeline-passed，需重跑 CI 再评审
- **committer 建议动作**：**需先补齐 ci-pipeline-passed 门禁后即可合入**

### PR #76：删除冗余代码

- **作者**：`@cui_jiahao` · **停留自然时长**：16.9h · **AI 判定**：**🤖 值得合入**
- **代码规模**：2 个文件（实质改动文件 2 个，表面改动文件 0 个，新增测试 +0 行）
- **关联 Issue 对齐**：已针对性修复 #67 脚本冗余清理
- **核心改动摘要**：清理 compile.sh/ut.sh 中 GE/ops-math 拷贝残留死代码并修正仓库名
  - 删除未使用的 LOG_HEAD 函数与 ge_st_rt2 死打印，不影响功能逻辑
  - REPOSITORY_NAME 由 ops-math 修正为 npu-simulator，建议补充产物路径影响说明
- **committer 建议动作**：**已获 approved/lgtm 且门禁全绿，建议直接合入**

### PR #75：refactor: remove unused _bar helper and duplicate _parse definition

- **作者**：`@qunzhongjia` · **停留自然时长**：23.4h · **AI 判定**：**🤖 值得合入**
- **代码规模**：2 个文件（实质改动文件 2 个，表面改动文件 0 个，新增测试 +0 行）
- **关联 Issue 对齐**：无关联 Issue，纯代码清理重构
- **核心改动摘要**：删除 dashboard 未引用的 _bar 辅助函数及测试中重复的 _parse 定义
  - _bar 定义后无任何调用点，删除后不影响分隔行渲染逻辑，属安全清理
  - test_config.py 中 _parse 重复定义且实现完全一致，去重可避免维护歧义
- **committer 建议动作**：**CLA 与 CI 均已通过且无冲突，建议直接合入**

### PR #74：fix(prof): fix AIV1 overlap label, SIMT f-string log, and analyzer guards

- **作者**：`@qunzhongjia` · **停留自然时长**：23.4h · **AI 判定**：**🤖 值得合入**
- **代码规模**：7 个文件（实质改动文件 6 个，表面改动文件 0 个，新增测试 +0 行）
- **关联 Issue 对齐**：无关联Issue，为自主发现的缺陷修复
- **核心改动摘要**：修正AIV1指标键名复制错误，并补除零、越界与日志异常防护
  - summary_reporter与demo中AIV1_SCALAR重叠指标键名误写为AIV0_VEC，已改正
  - 补total_exec_time除零、functions空列表越界，is not改!=比较更稳妥
  - runner改用list(root.handlers)避免遍历中删元素，log_level空值需显式判空
- **committer 建议动作**：**CLA与CI均通过，采纳检视建议后可合入**

### PR #73：fix(ci): update REPOSITORY_NAME to npu-simulator and remove stale bandit path

- **作者**：`@qunzhongjia` · **停留自然时长**：23.5h · **AI 判定**：**🤖 值得合入**
- **代码规模**：3 个文件（实质改动文件 3 个，表面改动文件 0 个，新增测试 +0 行）
- **关联 Issue 对齐**：已针对性修复 #61 配置残留问题
- **核心改动摘要**：修正 CI 脚本中仓库名的复制残留，并清理 bandit 的无效路径
  - compile.sh 与 ut.sh 两处 REPOSITORY_NAME 由 ops-math 改为 npu-simulator，修复日志与断言的误标
  - .pre-commit-config.yaml 移除不存在的根目录 prof_demo/，使 bandit 扫描的路径与实际目录结构一致
- **committer 建议动作**：**CLA（贡献者许可协议）与 CI 检查全绿且无冲突，建议直接合入**

### PR #72：CI 添加StaticCheck_md_check检查项

- **作者**：`@zhouchongshun` · **停留自然时长**：43.9h · **AI 判定**：**🤖 阻塞待解**
- **代码规模**：2 个文件（实质改动文件 2 个，表面改动文件 0 个，新增测试 +0 行）
- **关联 Issue 对齐**：无关联 Issue
- **核心改动摘要**：实质改动（2 文件 +80/-0），当前存在合路阻塞
  - 守卫判定：substantive_diff: 2 file(s); external_participant: Arerere
  - 门禁阻塞：cla_not_signed(cann-cla/no)、missing_label:cann-cla/yes、missing_label:ci-pipeline-passed、blocking_label:stat/needs-squash
- **committer 建议动作**：**解决门禁阻塞（cla_not_signed(cann-cla/no)、missing_label:cann-cla/yes、missing_label:ci-pipeline-passed、blocking_label:stat/needs-squash）后再推进合入**

### PR #70：docs(npu-simulator): fix spacing in examples

- **作者**：`@gcw_WJCkAUuk` · **停留自然时长**：79.4h · **AI 判定**：**🤖 值得合入**
- **代码规模**：2 个文件（实质改动文件 0 个，表面改动文件 0 个，新增测试 +0 行）
- **关联 Issue 对齐**：已针对性修复 #66 列明的间距问题
- **核心改动摘要**：修复两份中文最佳实践文档中英文间距问题
  - 仅调整两文件 5 处中英文空格，未改示例命令与技术语义，风险极低
  - 纯文档改动无需编译与 UT，git diff --check 通过；标题 26 项与正文 5 项差异已在 Issue 留言说明
- **committer 建议动作**：**CLA 与 CI 均通过、无冲突，建议直接合入**

### PR #60：fix(report): collapse the fixpipe twin rows by identity, not by adjacency

- **作者**：`@gcw_EkTYFH3T` · **停留自然时长**：229.3h · **AI 判定**：**🤖 阻塞待解**
- **代码规模**：1 个文件（实质改动文件 1 个，表面改动文件 0 个，新增测试 +0 行）
- **关联 Issue 对齐**：已针对性修复 #56 孪生行重复计入缺陷
- **核心改动摘要**：按 twin_key 字典折叠 fixpipe 孪生行，修复 UB 写重复计数
  - 改用字典按 twin_key 配对，解决 CoreId 排序导致孪生行不相邻的漏折叠
  - 评审建议把指令 ID 并入 key，避免同址同 tick 的不同写入被误合并
- **committer 建议动作**：**需补跑 CI 取得 ci-pipeline-passed 标签后再合入**

### PR #59：fix(record): recognize versioned Python executables

- **作者**：`@liangjinxuan-2026` · **停留自然时长**：255.7h · **AI 判定**：**🤖 值得合入**
- **代码规模**：1 个文件（实质改动文件 1 个，表面改动文件 0 个，新增测试 +0 行）
- **关联 Issue 对齐**：已针对性修复 #60 版本化解释器识别缺陷
- **核心改动摘要**：用正则识别版本化 Python 解释器，修复记录启动路径分类错误
  - 以正则替换静态 token 集合，覆盖 python3.11、绝对路径及 env 前缀三种形态
  - 自动检视指出 python3.11m 等 ABI 后缀未匹配，可作为后续增量改进
- **committer 建议动作**：**CLA 与 CI 均通过且冲突已解，建议合入并跟进 ABI 后缀建议**

