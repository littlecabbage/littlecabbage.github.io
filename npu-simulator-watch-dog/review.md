# PR & Issue 智能治理 Review 报告 · cann/npu-simulator

| 维度 | 详情 |
|---|---|
| **目标仓库** | [cann/npu-simulator](https://gitcode.com/cann/npu-simulator)（GitCode） |
| **巡检时间** | 2026-11-11 18:38 (UTC+8) |
| **分析引擎** | `gitcode-issue-triage` 确定性守卫 + Pi Agent (`cannbot/deepseek-v4.1-flash`) |
| **判定原则** | 宁漏勿错：强灌水信号 + 无安全否决 → 低价值候选；有任何实质代码/测试/关联 Issue → 保留并给出合路建议 |

---

## 一、执行摘要（供 on-call & committer 速览）

- **Issue 巡检**：共扫描 **39** 条 Issue，判定 KEEP **39** / CLOSE 候选 **0** / 待人工复核 **0**。
- **Open PR 总览（共 12 个）**：
  - ✅ **可立即合入（9 个）**：#47、#46、#45、#44、#41、#40、#39、#36、#23
  - ⚠️ **实质贡献但门禁阻塞（3 个）**：#37、#22、#21
  - 🧹 **低价值/表面改动候选（0 个）**：无

## 二、Open PR 逐条深度评审与行动清单

| PR | AI 结论 | 合路门禁 | 关联 Issue | 改动规模 (实质文件) | AI 改动摘要与关联对齐 | committer 建议动作 |
|---|---|---|---|---|---|---|
| [#47](https://gitcode.com/cann/npu-simulator/pulls/47) | **🤖 值得合入** | ✅ 可合入 | [#28](https://gitcode.com/cann/npu-simulator/issues/28) | +337/-58 (5/5 实质) | 按 kernel/core 隔离同步与竞争检测，修复跨核与 buffer 误报（针对性修复 #28 多核多 kernel 误报漏报） | CLA 通过且 CI 全绿、无冲突，建议直接合入 |
| [#46](https://gitcode.com/cann/npu-simulator/pulls/46) | **🤖 值得合入** | ✅ 可合入 | [#25](https://gitcode.com/cann/npu-simulator/issues/25) | +905/-368 (13/13 实质) | 重构 Action CI 流水线，新增 ARM smoke 支持（已针对性支持 #25 的 aarch64 smoke） | CLA 与 CI 全绿且无冲突，建议直接合入 |
| [#45](https://gitcode.com/cann/npu-simulator/pulls/45) | **🤖 值得合入** | ✅ 可合入 | [#24](https://gitcode.com/cann/npu-simulator/issues/24) | +64/-1 (3/3 实质) | 分析前检查空 kernel DB 并跳过，避免除零导致报告生成失败（针对性修复 #24 空 DB 报告失败） | CLA 与 CI 均通过且无冲突，建议直接合入 |
| [#44](https://gitcode.com/cann/npu-simulator/pulls/44) | **🤖 值得合入** | ✅ 可合入 | [#36](https://gitcode.com/cann/npu-simulator/issues/36) | +5/-1 (1/1 实质) | 修正数据竞争检测文档，明确 report 缺 record DB 时直接失败退出（针对性修复 #36 文档错误描述） | CLA 与 CI 均通过、无冲突，建议直接合入 |
| [#41](https://gitcode.com/cann/npu-simulator/pulls/41) | **🤖 值得合入** | ✅ 可合入 | [#32](https://gitcode.com/cann/npu-simulator/issues/32) | +112/-6 (8/8 实质) | -c 模式下 -n 生效，--chip/-u 改为显式告警（针对性修复 #32 参数静默忽略缺陷） | CLA 与 CI 均通过，无阻塞，建议直接合入 |
| [#40](https://gitcode.com/cann/npu-simulator/pulls/40) | **🤖 值得合入** | ✅ 可合入 | [#33](https://gitcode.com/cann/npu-simulator/issues/33) | +101/-11 (2/2 实质) | 修复 prof_demo 报告目录名解析，kernel 索引取 launch 号不再塌缩为 0（已针对性修复 #33 合并覆盖丢 kernel 缺陷） | CLA 与 CI 全绿且无冲突，建议直接合入 |
| [#39](https://gitcode.com/cann/npu-simulator/pulls/39) | **🤖 值得合入** | ✅ 可合入 | [#37](https://gitcode.com/cann/npu-simulator/issues/37) | +5/-4 (2/3 实质) | 统一 -n 默认行为为模型默认 core 0，修正帮助文本与用户指南措辞（针对修复 #37 文档默认核描述不一致） | CLA 与 CI 门禁全绿，文档与帮助文本已对齐，建议直接合入 |
| [#37](https://gitcode.com/cann/npu-simulator/pulls/37) | **🤖 阻塞待解** | ❌ 缺 ci-pipeline-passed | [#29](https://gitcode.com/cann/npu-simulator/issues/29) | +48/-26 (3/3 实质) | 移除 record 在用户 cwd 建/搬 log、run_log，避免误删用户数据（针对修复 #29 静默删除用户目录的缺陷） | 需先定位并修复 CI 流水线失败，重跑通过后再合入 |
| [#36](https://gitcode.com/cann/npu-simulator/pulls/36) | **🤖 值得合入** | ✅ 可合入 | [#18](https://gitcode.com/cann/npu-simulator/issues/18) | +70/-0 (2/2 实质) | 修复归档同名产物被低优先级来源覆盖的问题（已针对性修复 #18 归档覆盖缺陷） | CLA 与 CI 均通过且无冲突，建议直接合入 |
| [#23](https://gitcode.com/cann/npu-simulator/pulls/23) | **🤖 值得合入** | ✅ 可合入 | [#18](https://gitcode.com/cann/npu-simulator/issues/18) | +34/-3 (2/2 实质) | 修复多来源同名产物归档时被后来源覆盖的问题（针对性修复 #18 同名产物覆盖缺陷） | CLA 已签、CI 通过且无阻塞，建议直接合入 |
| [#22](https://gitcode.com/cann/npu-simulator/pulls/22) | **🤖 阻塞待解** | ❌ 存在代码冲突；阻塞标签 stat/needs-squash | [#17](https://gitcode.com/cann/npu-simulator/issues/17) | +5/-5 (1/3 实质) | 修正三份文档中四处页内锚点链接，匹配 GitCode 渲染标题 ID（精准修复 #17 的四处锚点失配） | 需作者解决合并冲突、squash 后重跑 CI，再合入 |
| [#21](https://gitcode.com/cann/npu-simulator/pulls/21) | **🤖 阻塞待解** | ❌ 缺 ci-pipeline-passed；阻塞标签 stat/needs-squash | [#16](https://gitcode.com/cann/npu-simulator/issues/16) | +75/-6 (5/5 实质) | 用独占 mkdir 分配运行目录，避免同秒运行复用归档（针对性修复 #16 目录复用缺陷） | 请作者 squash 提交并补 CI 通过标签后再评审合入 |

### PR #47：fix(detection): 按 kernel/core 隔离同步检测并修复跨核与 buffer 误报

- **作者**：`@ZhouBX` · **停留自然时长**：1h · **AI 判定**：**🤖 值得合入**
- **代码规模**：5 个文件（实质改动文件 5 个，表面改动文件 0 个，新增测试 +179 行）
- **关联 Issue 对齐**：针对性修复 #28 多核多 kernel 误报漏报
- **核心改动摘要**：按 kernel/core 隔离同步与竞争检测，修复跨核与 buffer 误报
  - 事件池 key 增加 core 维度并按 record DB 重建 KernelScope，隔离向量时钟与 GM 读写历史，消除跨核误报
  - 跨核同步改为读取 ExtendParams.ffts_mode，buffer 用 buf_id/buf_mode/buf_cnt 精确匹配，并限制冗余规则仅作用于 flag 家族
  - 新增 179 行测试覆盖多核多 kernel 场景，本地 212 passed，真实用例回归误报从 58/178 降到 0
- **committer 建议动作**：**CLA 通过且 CI 全绿、无冲突，建议直接合入**

### PR #46：ci: 重构 Action CI 流水线并支持 ARM smoke

- **作者**：`@ZhouBX` · **停留自然时长**：1h · **AI 判定**：**🤖 值得合入**
- **代码规模**：13 个文件（实质改动文件 13 个，表面改动文件 0 个，新增测试 +0 行）
- **关联 Issue 对齐**：已针对性支持 #25 的 aarch64 smoke
- **核心改动摘要**：重构 Action CI 流水线，新增 ARM smoke 支持
  - pre_smoke_for_action.sh 归一化架构名、精确匹配 linux-<arch> 包名，并预检 en_dtypes 工具链，覆盖 #25 三点痛点
  - py37_compat_action.yml 与 scan_action.yml 的 name 字段误写为 compile_action，建议改为对应工作流名称
- **committer 建议动作**：**CLA 与 CI 全绿且无冲突，建议直接合入**

### PR #45：fix(report): 跳过无执行指令的空 kernel DB

- **作者**：`@ZhouBX` · **停留自然时长**：1h · **AI 判定**：**🤖 值得合入**
- **代码规模**：3 个文件（实质改动文件 3 个，表面改动文件 0 个，新增测试 +53 行）
- **关联 Issue 对齐**：针对性修复 #24 空 DB 报告失败
- **核心改动摘要**：分析前检查空 kernel DB 并跳过，避免除零导致报告生成失败
  - reporters.py 在分析前判断 ExecutedInstructions 表缺失或 0 行则跳过，避免 exec_time_ticks=0 除零
  - 新增 test_reporters.py 并补强 prof_demo 用例，覆盖空 DB 场景，回归风险低
- **committer 建议动作**：**CLA 与 CI 均通过且无冲突，建议直接合入**

### PR #44：docs: 修正无 record DB 时 report 的行为说明

- **作者**：`@ZhouBX` · **停留自然时长**：1h · **AI 判定**：**🤖 值得合入**
- **代码规模**：1 个文件（实质改动文件 1 个，表面改动文件 0 个，新增测试 +0 行）
- **关联 Issue 对齐**：针对性修复 #36 文档错误描述
- **核心改动摘要**：修正数据竞争检测文档，明确 report 缺 record DB 时直接失败退出
  - 仅改 1 个文档文件（+5/-1），与 report.py 缺 DB 即 return None 的实际行为一致
  - 补充重新采集命令并声明 instr.bin / log_ca 不再支持，消除用户误解
- **committer 建议动作**：**CLA 与 CI 均通过、无冲突，建议直接合入**

### PR #41：feat(record): -c 模式支持 -n 并明确 --chip/-u 不生效

- **作者**：`@zhengronggui` · **停留自然时长**：3.7h · **AI 判定**：**🤖 值得合入**
- **代码规模**：8 个文件（实质改动文件 8 个，表面改动文件 0 个，新增测试 +72 行）
- **关联 Issue 对齐**：针对性修复 #32 参数静默忽略缺陷
- **核心改动摘要**：-c 模式下 -n 生效，--chip/-u 改为显式告警
  - KtestConfig 新增 core_id，经 parse_core_id 与 SoC 校验后注入 CORE_ENABLE_MASK，未指定时退回模型默认
  - 3 个测试文件新增 72 行覆盖 Stage1 解析、环境注入与告警路径，用户指南同步说明
- **committer 建议动作**：**CLA 与 CI 均通过，无阻塞，建议直接合入**

### PR #40：fix(report): 识别 prof_demo kernel_<launch>_<name>_reports 命名

- **作者**：`@zhengronggui` · **停留自然时长**：3.7h · **AI 判定**：**🤖 值得合入**
- **代码规模**：2 个文件（实质改动文件 2 个，表面改动文件 0 个，新增测试 +70 行）
- **关联 Issue 对齐**：已针对性修复 #33 合并覆盖丢 kernel 缺陷
- **核心改动摘要**：修复 prof_demo 报告目录名解析，kernel 索引取 launch 号不再塌缩为 0
  - 新增 ^kernel_(\d+)_.*_reports$ 分支，用 launch 号作 kernel 索引，修正 pid 塌缩与产物覆盖
  - 输出名冲突时追加 _2/_3 序号并打印 warn，配合 70 行新增用例覆盖索引、合并与 pid 唯一性
- **committer 建议动作**：**CLA 与 CI 全绿且无冲突，建议直接合入**

### PR #39：docs: 统一 -n 默认行为描述为模型默认（core 0）

- **作者**：`@zhengronggui` · **停留自然时长**：3.7h · **AI 判定**：**🤖 值得合入**
- **代码规模**：3 个文件（实质改动文件 2 个，表面改动文件 0 个，新增测试 +0 行）
- **关联 Issue 对齐**：针对修复 #37 文档默认核描述不一致
- **核心改动摘要**：统一 -n 默认行为为模型默认 core 0，修正帮助文本与用户指南措辞
  - 同步修改 main.py 帮助文本、用户指南与 record.py 注释，三处措辞一致，无行为变更
  - 作者以 ktest 实测佐证 camodel 默认仅 core 0；record 模式默认行为尚未验证，建议后续补充
- **committer 建议动作**：**CLA 与 CI 门禁全绿，文档与帮助文本已对齐，建议直接合入**

### PR #37：fix(record): 不再在用户工作目录创建/搬运 log、run_log，避免静默删除用户数据

- **作者**：`@zengzihui` · **停留自然时长**：22.6h · **AI 判定**：**🤖 阻塞待解**
- **代码规模**：3 个文件（实质改动文件 3 个，表面改动文件 0 个，新增测试 +32 行）
- **关联 Issue 对齐**：针对修复 #29 静默删除用户目录的缺陷
- **核心改动摘要**：移除 record 在用户 cwd 建/搬 log、run_log，避免误删用户数据
  - runtime.py 从 CAMODEL_ASSETS 摘除 log/run_log 并删除 RUNTIME_DIRS，消除归档后删除用户同名目录的路径
  - 新增 test_prepare_runtime_dirs_leaves_user_cwd_untouched 回归用例覆盖 #29，建议补充失败路径清理断言
- **committer 建议动作**：**需先定位并修复 CI 流水线失败，重跑通过后再合入**

### PR #36：fix(record): 同名产物按来源优先级归档，低优先级不再覆盖（#18）

- **作者**：`@yampolskiy` · **停留自然时长**：23.4h · **AI 判定**：**🤖 值得合入**
- **代码规模**：2 个文件（实质改动文件 2 个，表面改动文件 0 个，新增测试 +54 行）
- **关联 Issue 对齐**：已针对性修复 #18 归档覆盖缺陷
- **核心改动摘要**：修复归档同名产物被低优先级来源覆盖的问题
  - 三个归档入口改为按目标文件名去重，同名保留高优先级来源，低优先级文件留在原处
  - 新增三个同名冲突用例，复现失败→修复后 FIRST 保留、来源文件正确移动，测试覆盖充分
- **committer 建议动作**：**CLA 与 CI 均通过且无冲突，建议直接合入**

### PR #23：fix: preserve first-root artifact when names collide

- **作者**：`@gxhgxh2475698` · **停留自然时长**：368.3h · **AI 判定**：**🤖 值得合入**
- **代码规模**：2 个文件（实质改动文件 2 个，表面改动文件 0 个，新增测试 +25 行）
- **关联 Issue 对齐**：针对性修复 #18 同名产物覆盖缺陷
- **核心改动摘要**：修复多来源同名产物归档时被后来源覆盖的问题
  - 通配符归档加入 seen_names 去重，三个归档入口统一按首个来源优先，逻辑一致
  - 新增覆盖三条归档路径的回归用例，验证首来源保留且目标缺失时清理行为不变
- **committer 建议动作**：**CLA 已签、CI 通过且无阻塞，建议直接合入**

### PR #22：docs: match in-page links to rendered heading IDs

- **作者**：`@gxhgxh2475698` · **停留自然时长**：368.5h · **AI 判定**：**🤖 阻塞待解**
- **代码规模**：3 个文件（实质改动文件 1 个，表面改动文件 0 个，新增测试 +0 行）
- **关联 Issue 对齐**：精准修复 #17 的四处锚点失配
- **核心改动摘要**：修正三份文档中四处页内锚点链接，匹配 GitCode 渲染标题 ID
  - READM E、用户指南、安全声明四处 fragment 均对照渲染 HTML 核实，改动正确且无副作用
  - 已获 liangbinglong /approve 且 CI 通过，但仍有冲突与 needs-squash 阻塞，暂不可合
- **committer 建议动作**：**需作者解决合并冲突、squash 后重跑 CI，再合入**

### PR #21：fix: reserve separate output directories for same-second runs

- **作者**：`@gxhgxh2475698` · **停留自然时长**：368.7h · **AI 判定**：**🤖 阻塞待解**
- **代码规模**：5 个文件（实质改动文件 5 个，表面改动文件 0 个，新增测试 +46 行）
- **关联 Issue 对齐**：针对性修复 #16 目录复用缺陷
- **核心改动摘要**：用独占 mkdir 分配运行目录，避免同秒运行复用归档
  - 新增 create_unique_target_dir 以独占 mkdir 加 _N 后缀，record 与 ktest 两模式共用，逻辑正确
  - 附带修复 runtime.py 备份清理的 Py3.7 兼容问题，但 os.rename 改 copy2 需确认语义无回退
  - 两模式各新增同秒回归测试，覆盖仍开放 #16 的复现场景，建议补并发竞争用例
- **committer 建议动作**：**请作者 squash 提交并补 CI 通过标签后再评审合入**

