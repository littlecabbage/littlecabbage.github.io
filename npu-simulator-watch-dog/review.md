# PR & Issue 智能治理 Review 报告 · cann/npu-simulator

| 维度 | 详情 |
|---|---|
| **目标仓库** | [cann/npu-simulator](https://gitcode.com/cann/npu-simulator)（GitCode） |
| **巡检时间** | 2026-11-25 03:38 (UTC+8) |
| **分析引擎** | `gitcode-issue-triage` 确定性守卫 + Pi Agent (`cannbot/deepseek-v4.1-flash`) |
| **判定原则** | 宁漏勿错：强灌水信号 + 无安全否决 → 低价值候选；有任何实质代码/测试/关联 Issue → 保留并给出合路建议 |

---

## 一、执行摘要（供 on-call & committer 速览）

- **Issue 巡检**：共扫描 **72** 条 Issue，判定 KEEP **71** / CLOSE 候选 **0** / 待人工复核 **1**。
- **Open PR 总览（共 10 个）**：
  - ✅ **可立即合入（5 个）**：#75、#74、#73、#70、#59
  - ⚠️ **实质贡献但门禁阻塞（5 个）**：#78、#77、#76、#72、#60
  - 🧹 **低价值/表面改动候选（0 个）**：无

## 二、Open PR 逐条深度评审与行动清单

| PR | AI 结论 | 合路门禁 | 关联 Issue | 改动规模 (实质文件) | AI 改动摘要与关联对齐 | committer 建议动作 |
|---|---|---|---|---|---|---|
| [#78](https://gitcode.com/cann/npu-simulator/pulls/78) | **🤖 阻塞待解** | ❌ 缺 ci-pipeline-passed；阻塞标签 stat/needs-squash | — | +571/-10 (13/13 实质) | 新增 SOL 分析功能，含采集、参数、SQL 表、文档与测试（无关联 Issue，新特性缺少方案讨论） | 需压缩提交并补齐 ci-pipeline-passed，再重跑门禁 |
| [#77](https://gitcode.com/cann/npu-simulator/pulls/77) | **🤖 阻塞待解** | ❌ 缺 ci-pipeline-passed | [#68](https://gitcode.com/cann/npu-simulator/issues/68) | +2/-0 (1/1 实质) | README 补两行说明 cannsim 为分发名、与 npusim 共用 CLI（针对性澄清 #68 中 cannsim 命名疑问） | 需先补齐 ci-pipeline-passed 门禁后即可合入 |
| [#76](https://gitcode.com/cann/npu-simulator/pulls/76) | **🤖 阻塞待解** | ❌ 缺 ci-pipeline-passed | [#67](https://gitcode.com/cann/npu-simulator/issues/67) | +2/-22 (2/2 实质) | 清理 compile.sh/ut.sh 死代码并修正仓名为 npu-simulator（已针对性清理 #67 所列冗余项） | 需作者补跑流水线取得 ci-pipeline-passed，并补充说明卸载逻辑移除 |
| [#75](https://gitcode.com/cann/npu-simulator/pulls/75) | **🤖 值得合入** | ✅ 可合入 | — | +0/-14 (2/2 实质) | 删除 dashboard 未引用的 _bar 辅助函数及测试中重复的 _parse 定义（无关联 Issue，纯代码清理重构） | CLA 与 CI 均已通过且无冲突，建议直接合入 |
| [#74](https://gitcode.com/cann/npu-simulator/pulls/74) | **🤖 值得合入** | ✅ 可合入 | — | +17/-14 (6/7 实质) | 修复 AIV1 指标键名笔误、SIMT 日志花括号及多处除零越界防护（无关联 Issue，属自主缺陷修复） | CLA 与 CI 均通过，建议同步采纳检视建议后直接合入 |
| [#73](https://gitcode.com/cann/npu-simulator/pulls/73) | **🤖 值得合入** | ✅ 可合入 | [#61](https://gitcode.com/cann/npu-simulator/issues/61) | +3/-3 (3/3 实质) | 修正 CI 脚本中仓库名的复制残留，并清理 bandit 的无效路径（已针对性修复 #61 配置残留问题） | CLA（贡献者许可协议）与 CI 检查全绿且无冲突，建议直接合入 |
| [#72](https://gitcode.com/cann/npu-simulator/pulls/72) | **🤖 阻塞待解** | ❌ CLA 未签 (cann-cla/no)；缺 cann-cla/yes；缺 ci-pipeline-passed；阻塞标签 stat/needs-squash | — | +80/-0 (2/2 实质) | CI 新增 md_check 静态检查复用 workflow 并接入 CodeCheck 阶段（无关联 Issue，属 CI 检查能力补强） | 需签署 CLA、补 JOB_image staticcheck 输出并 squash 后重跑 CI |
| [#70](https://gitcode.com/cann/npu-simulator/pulls/70) | **🤖 值得合入** | ✅ 可合入 | [#66](https://gitcode.com/cann/npu-simulator/issues/66) | +5/-5 (0/2 实质) | 修复两份中文最佳实践文档中英文间距问题（已针对性修复 #66 列明的间距问题） | CLA 与 CI 均通过、无冲突，建议直接合入 |
| [#60](https://gitcode.com/cann/npu-simulator/pulls/60) | **🤖 阻塞待解** | ❌ 缺 ci-pipeline-passed | [#56](https://gitcode.com/cann/npu-simulator/issues/56) | +11/-5 (1/1 实质) | 按 twin_key 字典折叠 fixpipe 孪生行，修复 UB 写重复计数（已针对性修复 #56 孪生行重复计入缺陷） | 需补跑 CI 取得 ci-pipeline-passed 标签后再合入 |
| [#59](https://gitcode.com/cann/npu-simulator/pulls/59) | **🤖 值得合入** | ✅ 可合入 | [#60](https://gitcode.com/cann/npu-simulator/issues/60) | +14/-16 (1/1 实质) | 用正则识别版本化 Python 解释器，修复记录启动路径分类错误（已针对性修复 #60 版本化解释器识别缺陷） | CLA 与 CI 均通过且冲突已解，建议合入并跟进 ABI 后缀建议 |

### PR #78：Add Speed-of-light profiling feature

- **作者**：`@fomichevoleg5` · **停留自然时长**：4.7h · **AI 判定**：**🤖 阻塞待解**
- **代码规模**：13 个文件（实质改动文件 13 个，表面改动文件 0 个，新增测试 +20 行）
- **关联 Issue 对齐**：无关联 Issue，新特性缺少方案讨论
- **核心改动摘要**：新增 SOL 分析功能，含采集、参数、SQL 表、文档与测试
  - 新增 13 文件 571 行，含 SpeedOfLightAnalyzer 及两项测试，属实质特性
  - 仅放宽 version 7/8 校验未说明旧库缺 SOL 表，且 CUBE/VECTOR 缺异常保护
  - 已获 approved/lgtm，但缺 ci-pipeline-passed 且有 needs-squash 阻塞
  - 无关联 Issue，新特性应先补方案讨论与兼容性说明
- **committer 建议动作**：**需压缩提交并补齐 ci-pipeline-passed，再重跑门禁**

### PR #77：docs: clarify cannsim package and CLI aliases

- **作者**：`@lilong555` · **停留自然时长**：6.6h · **AI 判定**：**🤖 阻塞待解**
- **代码规模**：1 个文件（实质改动文件 1 个，表面改动文件 0 个，新增测试 +0 行）
- **关联 Issue 对齐**：针对性澄清 #68 中 cannsim 命名疑问
- **核心改动摘要**：README 补两行说明 cannsim 为分发名、与 npusim 共用 CLI
  - 仅文档新增两行，说明 wheel 分发名与 CLI 入口别名，不改代码与构建
  - 已具 cann-cla/yes，但缺 ci-pipeline-passed，需重跑 CI 再评审
- **committer 建议动作**：**需先补齐 ci-pipeline-passed 门禁后即可合入**

### PR #76：删除冗余代码

- **作者**：`@cui_jiahao` · **停留自然时长**：7.9h · **AI 判定**：**🤖 阻塞待解**
- **代码规模**：2 个文件（实质改动文件 2 个，表面改动文件 0 个，新增测试 +0 行）
- **关联 Issue 对齐**：已针对性清理 #67 所列冗余项
- **核心改动摘要**：清理 compile.sh/ut.sh 死代码并修正仓名为 npu-simulator
  - 删除 LOG_HEAD、ge_st_rt2 打印等死代码，逻辑无功能变更，属安全清理
  - REPOSITORY_NAME 由 ops-math 改为 npu-simulator 是实质修正，需说明产物路径影响；另需确认 ops_math 卸载逻辑移除不影响 CI 环境洁净
- **committer 建议动作**：**需作者补跑流水线取得 ci-pipeline-passed，并补充说明卸载逻辑移除**

### PR #75：refactor: remove unused _bar helper and duplicate _parse definition

- **作者**：`@qunzhongjia` · **停留自然时长**：14.4h · **AI 判定**：**🤖 值得合入**
- **代码规模**：2 个文件（实质改动文件 2 个，表面改动文件 0 个，新增测试 +0 行）
- **关联 Issue 对齐**：无关联 Issue，纯代码清理重构
- **核心改动摘要**：删除 dashboard 未引用的 _bar 辅助函数及测试中重复的 _parse 定义
  - _bar 定义后无任何调用点，删除后不影响分隔行渲染逻辑，属安全清理
  - test_config.py 中 _parse 重复定义且实现完全一致，去重可避免维护歧义
- **committer 建议动作**：**CLA 与 CI 均已通过且无冲突，建议直接合入**

### PR #74：fix(prof): fix AIV1 overlap label, SIMT f-string log, and analyzer guards

- **作者**：`@qunzhongjia` · **停留自然时长**：14.4h · **AI 判定**：**🤖 值得合入**
- **代码规模**：7 个文件（实质改动文件 6 个，表面改动文件 0 个，新增测试 +0 行）
- **关联 Issue 对齐**：无关联 Issue，属自主缺陷修复
- **核心改动摘要**：修复 AIV1 指标键名笔误、SIMT 日志花括号及多处除零越界防护
  - AIV1_SCALAR_vs_AIV1_VEC 键名修正，消除与 AIV0_VEC 的指标覆盖冲突
  - log_level 空值回退为空串会丢 DEBUG traceback，建议按检视意见改为显式非空判断
- **committer 建议动作**：**CLA 与 CI 均通过，建议同步采纳检视建议后直接合入**

### PR #73：fix(ci): update REPOSITORY_NAME to npu-simulator and remove stale bandit path

- **作者**：`@qunzhongjia` · **停留自然时长**：14.5h · **AI 判定**：**🤖 值得合入**
- **代码规模**：3 个文件（实质改动文件 3 个，表面改动文件 0 个，新增测试 +0 行）
- **关联 Issue 对齐**：已针对性修复 #61 配置残留问题
- **核心改动摘要**：修正 CI 脚本中仓库名的复制残留，并清理 bandit 的无效路径
  - compile.sh 与 ut.sh 两处 REPOSITORY_NAME 由 ops-math 改为 npu-simulator，修复日志与断言的误标
  - .pre-commit-config.yaml 移除不存在的根目录 prof_demo/，使 bandit 扫描的路径与实际目录结构一致
- **committer 建议动作**：**CLA（贡献者许可协议）与 CI 检查全绿且无冲突，建议直接合入**

### PR #72：CI 添加StaticCheck_md_check检查项

- **作者**：`@zhouchongshun` · **停留自然时长**：34.9h · **AI 判定**：**🤖 阻塞待解**
- **代码规模**：2 个文件（实质改动文件 2 个，表面改动文件 0 个，新增测试 +0 行）
- **关联 Issue 对齐**：无关联 Issue，属 CI 检查能力补强
- **核心改动摘要**：CI 新增 md_check 静态检查复用 workflow 并接入 CodeCheck 阶段
  - 新增 JOB_staticcheck_md_check 引用 jobs.JOB_image.outputs.staticcheck，但 JOB_image 未定义该输出，镜像地址为空将致任务失败
  - 子 workflow 引用 env.obs_path/TARGET_BRANCH/MERGE_ID 等变量却无 env 段或 inputs 传入，下载上传路径可能为空
  - workflow 名 'staticheck_action' 拼写缺 c，建议修正；通过后仍受 cann-cla/no 与 needs-squash 门禁阻塞
- **committer 建议动作**：**需签署 CLA、补 JOB_image staticcheck 输出并 squash 后重跑 CI**

### PR #70：docs(npu-simulator): fix spacing in examples

- **作者**：`@gcw_WJCkAUuk` · **停留自然时长**：70.4h · **AI 判定**：**🤖 值得合入**
- **代码规模**：2 个文件（实质改动文件 0 个，表面改动文件 0 个，新增测试 +0 行）
- **关联 Issue 对齐**：已针对性修复 #66 列明的间距问题
- **核心改动摘要**：修复两份中文最佳实践文档中英文间距问题
  - 仅调整两文件 5 处中英文空格，未改示例命令与技术语义，风险极低
  - 纯文档改动无需编译与 UT，git diff --check 通过；标题 26 项与正文 5 项差异已在 Issue 留言说明
- **committer 建议动作**：**CLA 与 CI 均通过、无冲突，建议直接合入**

### PR #60：fix(report): collapse the fixpipe twin rows by identity, not by adjacency

- **作者**：`@gcw_EkTYFH3T` · **停留自然时长**：220.3h · **AI 判定**：**🤖 阻塞待解**
- **代码规模**：1 个文件（实质改动文件 1 个，表面改动文件 0 个，新增测试 +0 行）
- **关联 Issue 对齐**：已针对性修复 #56 孪生行重复计入缺陷
- **核心改动摘要**：按 twin_key 字典折叠 fixpipe 孪生行，修复 UB 写重复计数
  - 改用字典按 twin_key 配对，解决 CoreId 排序导致孪生行不相邻的漏折叠
  - 评审建议把指令 ID 并入 key，避免同址同 tick 的不同写入被误合并
- **committer 建议动作**：**需补跑 CI 取得 ci-pipeline-passed 标签后再合入**

### PR #59：fix(record): recognize versioned Python executables

- **作者**：`@liangjinxuan-2026` · **停留自然时长**：246.7h · **AI 判定**：**🤖 值得合入**
- **代码规模**：1 个文件（实质改动文件 1 个，表面改动文件 0 个，新增测试 +0 行）
- **关联 Issue 对齐**：已针对性修复 #60 版本化解释器识别缺陷
- **核心改动摘要**：用正则识别版本化 Python 解释器，修复记录启动路径分类错误
  - 以正则替换静态 token 集合，覆盖 python3.11、绝对路径及 env 前缀三种形态
  - 自动检视指出 python3.11m 等 ABI 后缀未匹配，可作为后续增量改进
- **committer 建议动作**：**CLA 与 CI 均通过且冲突已解，建议合入并跟进 ABI 后缀建议**

