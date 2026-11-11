# PR & Issue 智能治理 Review 报告 · cann/npu-simulator

| 维度 | 详情 |
|---|---|
| **目标仓库** | [cann/npu-simulator](https://gitcode.com/cann/npu-simulator)（GitCode） |
| **巡检时间** | 2026-11-12 02:37 (UTC+8) |
| **分析引擎** | `gitcode-issue-triage` 确定性守卫 + Pi Agent (`cannbot/deepseek-v4.1-flash`) |
| **判定原则** | 宁漏勿错：强灌水信号 + 无安全否决 → 低价值候选；有任何实质代码/测试/关联 Issue → 保留并给出合路建议 |

---

## 一、执行摘要（供 on-call & committer 速览）

- **Issue 巡检**：共扫描 **39** 条 Issue，判定 KEEP **39** / CLOSE 候选 **0** / 待人工复核 **0**。
- **Open PR 总览（共 10 个）**：
  - ✅ **可立即合入（7 个）**：#47、#46、#45、#44、#36、#23、#22
  - ⚠️ **实质贡献但门禁阻塞（3 个）**：#41、#37、#21
  - 🧹 **低价值/表面改动候选（0 个）**：无

## 二、Open PR 逐条深度评审与行动清单

| PR | AI 结论 | 合路门禁 | 关联 Issue | 改动规模 (实质文件) | AI 改动摘要与关联对齐 | committer 建议动作 |
|---|---|---|---|---|---|---|
| [#47](https://gitcode.com/cann/npu-simulator/pulls/47) | **🤖 值得合入** | ✅ 可合入 | [#28](https://gitcode.com/cann/npu-simulator/issues/28) | +337/-58 (5/5 实质) | 按 kernel/core 隔离同步与竞争检测，修复跨核与 buffer 误报（针对性修复 #28 多核多 kernel 误报漏报） | CLA 通过且 CI 全绿、无冲突，建议直接合入 |
| [#46](https://gitcode.com/cann/npu-simulator/pulls/46) | **🤖 值得合入** | ✅ 可合入 | [#25](https://gitcode.com/cann/npu-simulator/issues/25) | +905/-368 (13/13 实质) | 重构 Action CI 流水线，新增 ARM smoke 支持（已针对性支持 #25 的 aarch64 smoke） | CLA 与 CI 全绿且无冲突，建议直接合入 |
| [#45](https://gitcode.com/cann/npu-simulator/pulls/45) | **🤖 值得合入** | ✅ 可合入 | [#24](https://gitcode.com/cann/npu-simulator/issues/24) | +64/-1 (3/3 实质) | 分析前检查空 kernel DB 并跳过，避免除零导致报告生成失败（针对性修复 #24 空 DB 报告失败） | CLA 与 CI 均通过且无冲突，建议直接合入 |
| [#44](https://gitcode.com/cann/npu-simulator/pulls/44) | **🤖 值得合入** | ✅ 可合入 | [#36](https://gitcode.com/cann/npu-simulator/issues/36) | +5/-1 (1/1 实质) | 修正数据竞争检测文档，明确 report 缺 record DB 时直接失败退出（针对性修复 #36 文档错误描述） | CLA 与 CI 均通过、无冲突，建议直接合入 |
| [#41](https://gitcode.com/cann/npu-simulator/pulls/41) | **🤖 阻塞待解** | ❌ 存在代码冲突 | [#32](https://gitcode.com/cann/npu-simulator/issues/32) | +112/-6 (8/8 实质) | 修复 record -c 下 -n 不生效、--chip/-u 静默忽略的问题（已针对性修复 #32 参数静默忽略缺陷） | 需作者先解决 merge 冲突并重跑 CI，全绿后再合入 |
| [#37](https://gitcode.com/cann/npu-simulator/pulls/37) | **🤖 阻塞待解** | ❌ 阻塞标签 stat/needs-squash | [#29](https://gitcode.com/cann/npu-simulator/issues/29) | +49/-29 (3/3 实质) | 移除 cwd 下 log/run_log 的创建、归档与删除逻辑，避免误删用户数据（针对性修复 #29 静默删除用户数据缺陷） | 功能与测试均认可，需作者 squash 为单提交后合入 |
| [#36](https://gitcode.com/cann/npu-simulator/pulls/36) | **🤖 值得合入** | ✅ 可合入 | [#18](https://gitcode.com/cann/npu-simulator/issues/18) | +70/-0 (2/2 实质) | 修复归档同名产物被低优先级来源覆盖的问题（已针对性修复 #18 归档覆盖缺陷） | CLA 与 CI 均通过且无冲突，建议直接合入 |
| [#23](https://gitcode.com/cann/npu-simulator/pulls/23) | **🤖 值得合入** | ✅ 可合入 | [#18](https://gitcode.com/cann/npu-simulator/issues/18) | +34/-3 (2/2 实质) | 修复多来源同名产物归档时被后来源覆盖的问题（针对性修复 #18 同名产物覆盖缺陷） | CLA 已签、CI 通过且无阻塞，建议直接合入 |
| [#22](https://gitcode.com/cann/npu-simulator/pulls/22) | **🤖 值得合入** | ✅ 可合入 | [#17](https://gitcode.com/cann/npu-simulator/issues/17) | +3/-3 (1/1 实质) | 修正安全说明两处附录锚点链接，恢复文档跳转定位（已针对性修复 #17 锚点不匹配） | 已获 approved 且门禁全绿，建议直接合入 |
| [#21](https://gitcode.com/cann/npu-simulator/pulls/21) | **🤖 阻塞待解** | ❌ 阻塞标签 stat/needs-squash | [#16](https://gitcode.com/cann/npu-simulator/issues/16) | +75/-6 (5/5 实质) | 修复同秒运行复用输出目录，改用独占 mkdir 分配（已针对性修复 #16 同秒目录复用缺陷） | 需作者 squash 压缩提交历史后重跑门禁再合入 |

### PR #47：fix(detection): 按 kernel/core 隔离同步检测并修复跨核与 buffer 误报

- **作者**：`@ZhouBX` · **停留自然时长**：9h · **AI 判定**：**🤖 值得合入**
- **代码规模**：5 个文件（实质改动文件 5 个，表面改动文件 0 个，新增测试 +179 行）
- **关联 Issue 对齐**：针对性修复 #28 多核多 kernel 误报漏报
- **核心改动摘要**：按 kernel/core 隔离同步与竞争检测，修复跨核与 buffer 误报
  - 事件池 key 增加 core 维度并按 record DB 重建 KernelScope，隔离向量时钟与 GM 读写历史，消除跨核误报
  - 跨核同步改为读取 ExtendParams.ffts_mode，buffer 用 buf_id/buf_mode/buf_cnt 精确匹配，并限制冗余规则仅作用于 flag 家族
  - 新增 179 行测试覆盖多核多 kernel 场景，本地 212 passed，真实用例回归误报从 58/178 降到 0
- **committer 建议动作**：**CLA 通过且 CI 全绿、无冲突，建议直接合入**

### PR #46：ci: 重构 Action CI 流水线并支持 ARM smoke

- **作者**：`@ZhouBX` · **停留自然时长**：9h · **AI 判定**：**🤖 值得合入**
- **代码规模**：13 个文件（实质改动文件 13 个，表面改动文件 0 个，新增测试 +0 行）
- **关联 Issue 对齐**：已针对性支持 #25 的 aarch64 smoke
- **核心改动摘要**：重构 Action CI 流水线，新增 ARM smoke 支持
  - pre_smoke_for_action.sh 归一化架构名、精确匹配 linux-<arch> 包名，并预检 en_dtypes 工具链，覆盖 #25 三点痛点
  - py37_compat_action.yml 与 scan_action.yml 的 name 字段误写为 compile_action，建议改为对应工作流名称
- **committer 建议动作**：**CLA 与 CI 全绿且无冲突，建议直接合入**

### PR #45：fix(report): 跳过无执行指令的空 kernel DB

- **作者**：`@ZhouBX` · **停留自然时长**：9h · **AI 判定**：**🤖 值得合入**
- **代码规模**：3 个文件（实质改动文件 3 个，表面改动文件 0 个，新增测试 +53 行）
- **关联 Issue 对齐**：针对性修复 #24 空 DB 报告失败
- **核心改动摘要**：分析前检查空 kernel DB 并跳过，避免除零导致报告生成失败
  - reporters.py 在分析前判断 ExecutedInstructions 表缺失或 0 行则跳过，避免 exec_time_ticks=0 除零
  - 新增 test_reporters.py 并补强 prof_demo 用例，覆盖空 DB 场景，回归风险低
- **committer 建议动作**：**CLA 与 CI 均通过且无冲突，建议直接合入**

### PR #44：docs: 修正无 record DB 时 report 的行为说明

- **作者**：`@ZhouBX` · **停留自然时长**：9h · **AI 判定**：**🤖 值得合入**
- **代码规模**：1 个文件（实质改动文件 1 个，表面改动文件 0 个，新增测试 +0 行）
- **关联 Issue 对齐**：针对性修复 #36 文档错误描述
- **核心改动摘要**：修正数据竞争检测文档，明确 report 缺 record DB 时直接失败退出
  - 仅改 1 个文档文件（+5/-1），与 report.py 缺 DB 即 return None 的实际行为一致
  - 补充重新采集命令并声明 instr.bin / log_ca 不再支持，消除用户误解
- **committer 建议动作**：**CLA 与 CI 均通过、无冲突，建议直接合入**

### PR #41：feat(record): -c 模式支持 -n 并明确 --chip/-u 不生效

- **作者**：`@zhengronggui` · **停留自然时长**：11.7h · **AI 判定**：**🤖 阻塞待解**
- **代码规模**：8 个文件（实质改动文件 8 个，表面改动文件 0 个，新增测试 +72 行）
- **关联 Issue 对齐**：已针对性修复 #32 参数静默忽略缺陷
- **核心改动摘要**：修复 record -c 下 -n 不生效、--chip/-u 静默忽略的问题
  - 新增 KtestConfig.core_id，Stage1 用 parse_core_id 校验核数，Stage3 注入 CORE_ENABLE_MASK，逻辑闭环
  - 未指定 -n 时不注入 mask，保持仅 core 0 的原有行为，兼容性说明充分；已补 3 个测试文件覆盖告警与 mask 注入
  - 已有 liangbinglong 的 approve 与 cann-cla/yes、ci-pipeline-passed，但存在 merge_conflicts 门禁阻塞
- **committer 建议动作**：**需作者先解决 merge 冲突并重跑 CI，全绿后再合入**

### PR #37：fix(record): 不再在用户工作目录创建/搬运 log、run_log，避免静默删除用户数据

- **作者**：`@zengzihui` · **停留自然时长**：30.6h · **AI 判定**：**🤖 阻塞待解**
- **代码规模**：3 个文件（实质改动文件 3 个，表面改动文件 0 个，新增测试 +32 行）
- **关联 Issue 对齐**：针对性修复 #29 静默删除用户数据缺陷
- **核心改动摘要**：移除 cwd 下 log/run_log 的创建、归档与删除逻辑，避免误删用户数据
  - runtime.py 收紧 CAMODEL_ASSETS 并删除 RUNTIME_DIRS，仅保留 stars_log*_task.dump，方向正确
  - 新增回归测试验证 prepare_runtime_dirs 不再污染用户 cwd；仅剩 stat/needs-squash 门禁待解
- **committer 建议动作**：**功能与测试均认可，需作者 squash 为单提交后合入**

### PR #36：fix(record): 同名产物按来源优先级归档，低优先级不再覆盖（#18）

- **作者**：`@yampolskiy` · **停留自然时长**：31.4h · **AI 判定**：**🤖 值得合入**
- **代码规模**：2 个文件（实质改动文件 2 个，表面改动文件 0 个，新增测试 +54 行）
- **关联 Issue 对齐**：已针对性修复 #18 归档覆盖缺陷
- **核心改动摘要**：修复归档同名产物被低优先级来源覆盖的问题
  - 三个归档入口改为按目标文件名去重，同名保留高优先级来源，低优先级文件留在原处
  - 新增三个同名冲突用例，复现失败→修复后 FIRST 保留、来源文件正确移动，测试覆盖充分
- **committer 建议动作**：**CLA 与 CI 均通过且无冲突，建议直接合入**

### PR #23：fix: preserve first-root artifact when names collide

- **作者**：`@gxhgxh2475698` · **停留自然时长**：376.3h · **AI 判定**：**🤖 值得合入**
- **代码规模**：2 个文件（实质改动文件 2 个，表面改动文件 0 个，新增测试 +25 行）
- **关联 Issue 对齐**：针对性修复 #18 同名产物覆盖缺陷
- **核心改动摘要**：修复多来源同名产物归档时被后来源覆盖的问题
  - 通配符归档加入 seen_names 去重，三个归档入口统一按首个来源优先，逻辑一致
  - 新增覆盖三条归档路径的回归用例，验证首来源保留且目标缺失时清理行为不变
- **committer 建议动作**：**CLA 已签、CI 通过且无阻塞，建议直接合入**

### PR #22：docs: match in-page links to rendered heading IDs

- **作者**：`@gxhgxh2475698` · **停留自然时长**：376.5h · **AI 判定**：**🤖 值得合入**
- **代码规模**：1 个文件（实质改动文件 1 个，表面改动文件 0 个，新增测试 +0 行）
- **关联 Issue 对齐**：已针对性修复 #17 锚点不匹配
- **核心改动摘要**：修正安全说明两处附录锚点链接，恢复文档跳转定位
  - 仅改 docs/zh/security_statement.md 两处 fragment 为 a-文件夹各场景…，与渲染 heading id 一致
  - 按检视意见撤回 README 与用户指南改动，未破坏原有可用链接，纯文档无兼容性风险
- **committer 建议动作**：**已获 approved 且门禁全绿，建议直接合入**

### PR #21：fix: reserve separate output directories for same-second runs

- **作者**：`@gxhgxh2475698` · **停留自然时长**：376.7h · **AI 判定**：**🤖 阻塞待解**
- **代码规模**：5 个文件（实质改动文件 5 个，表面改动文件 0 个，新增测试 +46 行）
- **关联 Issue 对齐**：已针对性修复 #16 同秒目录复用缺陷
- **核心改动摘要**：修复同秒运行复用输出目录，改用独占 mkdir 分配
  - 新增 create_unique_target_dir，独占 mkdir 并以 _1/_2 后缀避让，record 与 ktest 共用
  - 附带修复 Python 3.7 不兼容的备份清理，两模式各补同秒回归测试
- **committer 建议动作**：**需作者 squash 压缩提交历史后重跑门禁再合入**

