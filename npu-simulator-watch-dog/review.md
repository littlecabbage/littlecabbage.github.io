# PR & Issue 智能治理 Review 报告 · cann/npu-simulator

| 维度 | 详情 |
|---|---|
| **目标仓库** | [cann/npu-simulator](https://gitcode.com/cann/npu-simulator)（GitCode） |
| **巡检时间** | 2026-11-22 15:38 (UTC+8) |
| **分析引擎** | `gitcode-issue-triage` 确定性守卫 + Pi Agent (`cannbot/deepseek-v4.1-flash`) |
| **判定原则** | 宁漏勿错：强灌水信号 + 无安全否决 → 低价值候选；有任何实质代码/测试/关联 Issue → 保留并给出合路建议 |

---

## 一、执行摘要（供 on-call & committer 速览）

- **Issue 巡检**：共扫描 **66** 条 Issue，判定 KEEP **65** / CLOSE 候选 **0** / 待人工复核 **1**。
- **Open PR 总览（共 13 个）**：
  - ✅ **可立即合入（7 个）**：#68、#63、#59、#58、#56、#55、#54
  - ⚠️ **实质贡献但门禁阻塞（6 个）**：#70、#67、#64、#60、#57、#53
  - 🧹 **低价值/表面改动候选（0 个）**：无

## 二、Open PR 逐条深度评审与行动清单

| PR | AI 结论 | 合路门禁 | 关联 Issue | 改动规模 (实质文件) | AI 改动摘要与关联对齐 | committer 建议动作 |
|---|---|---|---|---|---|---|
| [#70](https://gitcode.com/cann/npu-simulator/pulls/70) | **🤖 阻塞待解** | ❌ 缺 ci-pipeline-passed | [#66](https://gitcode.com/cann/npu-simulator/issues/66) | +5/-5 (0/2 实质) | 修正两份最佳实践文档中英文间距，提升中文可读性（已针对性修复 #66 列明的 5 处间距问题） | 文档改动无害，需等待 ci-pipeline-passed 打标后合入 |
| [#68](https://gitcode.com/cann/npu-simulator/pulls/68) | **🤖 值得合入** | ✅ 可合入 | [#65](https://gitcode.com/cann/npu-simulator/issues/65) | +41/-949 (19/19 实质) | 删除逐指令动态 IPC 计算、trace 字段与相关表，保留聚合 IPC 指标（已针对性实现 #65 需求，移除逐指令 IPC） | CLA 与 CI 全绿、无冲突阻塞，建议直接合入 |
| [#67](https://gitcode.com/cann/npu-simulator/pulls/67) | **🤖 阻塞待解** | ❌ 阻塞标签 stat/needs-squash | [#63](https://gitcode.com/cann/npu-simulator/issues/63) | +67/-145 (11/11 实质) | 可选处理失败时保留基础报告，移除非必要 Roofline JSON 导出（针对性修复 #63 可选报告失败阻塞导出） | 需作者 squash 提交并重跑门禁，通过后再合入 |
| [#64](https://gitcode.com/cann/npu-simulator/pulls/64) | **🤖 阻塞待解** | ❌ 阻塞标签 stat/needs-squash | — | +330/-2 (6/6 实质) | 新增 SOL 分析器与 --sol 选项，评估内核吞吐上限（无关联 Issue，新特性未先走方案讨论） | 需作者 squash 提交、补测试并关联 Issue 后再评审 |
| [#63](https://gitcode.com/cann/npu-simulator/pulls/63) | **🤖 值得合入** | ✅ 可合入 | [#64](https://gitcode.com/cann/npu-simulator/issues/64) | +92/-11 (4/4 实质) | 为 SourceFiles 增加源码全文列并在报告阶段回填，修复报告缺源码（针对性修复 #64 报告缺失完整源文件） | CLA 已签、CI 通过且无冲突，建议 committer 直接合入 |
| [#60](https://gitcode.com/cann/npu-simulator/pulls/60) | **🤖 阻塞待解** | ❌ 缺 ci-pipeline-passed | [#56](https://gitcode.com/cann/npu-simulator/issues/56) | +11/-5 (1/1 实质) | 把 pending 单槽改为按 twin_key 索引的字典，折叠 fixpipe 孪生行，修复 UB 写重复计数（已针对性修复 #56 孪生行重复计数缺陷） | 暂缓合入：需补齐 ci-pipeline-passed，并回应评审的 key 收紧建议 |
| [#59](https://gitcode.com/cann/npu-simulator/pulls/59) | **🤖 值得合入** | ✅ 可合入 | [#60](https://gitcode.com/cann/npu-simulator/issues/60) | +14/-16 (1/1 实质) | 用正则统一识别 python3.11 等版本化解释器并修正 Python 路径判定（针对性修复 #60 版本化解释器漏判） | CLA 与 CI 均通过且无冲突，建议直接合入 |
| [#58](https://gitcode.com/cann/npu-simulator/pulls/58) | **🤖 值得合入** | ✅ 可合入 | [#59](https://gitcode.com/cann/npu-simulator/issues/59) | +63/-28 (2/2 实质) | 实质代码改动（2 文件 +63/-28），门禁全绿（已关联 #59） | CLA 与 CI 已通过，建议 committer 完成最终代码检视后合入 |
| [#57](https://gitcode.com/cann/npu-simulator/pulls/57) | **🤖 阻塞待解** | ❌ 阻塞标签 stat/needs-squash | [#27](https://gitcode.com/cann/npu-simulator/issues/27) | +63/-2 (2/2 实质) | 修正 LOAD_2D 查询中 K 起始位置误取 MStartPosition 的缺陷，并补充回归测试（已针对性修复 #27 的 K 起始位置映射错误） | 需作者去除重复 import、squash 提交并重跑 CI，门禁满足后再合入 |
| [#56](https://gitcode.com/cann/npu-simulator/pulls/56) | **🤖 值得合入** | ✅ 可合入 | [#55](https://gitcode.com/cann/npu-simulator/issues/55) | +49/-1 (2/2 实质) | 改用 as_uri 构造 SQLite 只读连接，修复特殊字符路径下报告归档遗漏（已针对性修复 #55 特殊字符路径打包缺陷） | CLA 与 CI 均已通过，外部参与者已复现验证，建议直接合入 |
| [#55](https://gitcode.com/cann/npu-simulator/pulls/55) | **🤖 值得合入** | ✅ 可合入 | [#58](https://gitcode.com/cann/npu-simulator/issues/58) | +2/-2 (2/2 实质) | record 入口保留 user_app 原始字符串，避免 Path 归一化篡改命令（针对性修复 #58 引号命令与 URL 被改写缺陷） | CLA 与 CI 门禁全绿，无冲突，建议尽快合入 |
| [#54](https://gitcode.com/cann/npu-simulator/pulls/54) | **🤖 值得合入** | ✅ 可合入 | [#54](https://gitcode.com/cann/npu-simulator/issues/54) | +2/-3 (1/1 实质) | 修正 report 示例，将 -o 误写为 JSON 文件路径改为输出目录（已按 #54 修正 report 示例与产物说明） | CLA 已签、CI 通过且冲突已解，建议直接合入 |
| [#53](https://gitcode.com/cann/npu-simulator/pulls/53) | **🤖 阻塞待解** | ❌ 缺 ci-pipeline-passed | [#53](https://gitcode.com/cann/npu-simulator/issues/53) | +9/-0 (1/1 实质) | 修正吞吐统计区间并集算法，扫描前按起点排序，避免占用时间多算（已针对性修复 #53 带宽低估缺陷） | 已获 lgtm，但缺 ci-pipeline-passed，需重跑 CI 全绿后合入 |

### PR #70：docs(npu-simulator): fix spacing in examples

- **作者**：`@gcw_WJCkAUuk` · **停留自然时长**：10.4h · **AI 判定**：**🤖 阻塞待解**
- **代码规模**：2 个文件（实质改动文件 0 个，表面改动文件 0 个，新增测试 +0 行）
- **关联 Issue 对齐**：已针对性修复 #66 列明的 5 处间距问题
- **核心改动摘要**：修正两份最佳实践文档中英文间距，提升中文可读性
  - 纯文档改动，仅调中英文空格，未改示例命令、参数或技术语义，无回归风险
  - Issue 标题称 26 项但正文仅列 5 项，本 MR 已覆盖全部可核验条目，剩余项需后续 Issue 补充
- **committer 建议动作**：**文档改动无害，需等待 ci-pipeline-passed 打标后合入**

### PR #68：Remove misleading per-instruction IPC metrics

- **作者**：`@churkinaleksandr` · **停留自然时长**：43.1h · **AI 判定**：**🤖 值得合入**
- **代码规模**：19 个文件（实质改动文件 19 个，表面改动文件 0 个，新增测试 +10 行）
- **关联 Issue 对齐**：已针对性实现 #65 需求，移除逐指令 IPC
- **核心改动摘要**：删除逐指令动态 IPC 计算、trace 字段与相关表，保留聚合 IPC 指标
  - 净删约 900 行，移除 ScalarIpcDynamic/VfIPCDynamic 表、视图及 prof_demo 回退实现，降低维护成本
  - 同步更新文档与参数说明，并新增测试校验旧库重分析后不再生成动态 IPC 表
- **committer 建议动作**：**CLA 与 CI 全绿、无冲突阻塞，建议直接合入**

### PR #67：fix(prof): preserve base reports when optional processing fails

- **作者**：`@churkinaleksandr` · **停留自然时长**：65.2h · **AI 判定**：**🤖 阻塞待解**
- **代码规模**：11 个文件（实质改动文件 11 个，表面改动文件 0 个，新增测试 +15 行）
- **关联 Issue 对齐**：针对性修复 #63 可选报告失败阻塞导出
- **核心改动摘要**：可选处理失败时保留基础报告，移除非必要 Roofline JSON 导出
  - 删除独立 roofline.json 导出，Roofline 数据仍保留在 SQLite 表与 CSV 中，避免可选失败阻断打包
  - Critical Path 改为临时目录生成、成功后再发布，ELF 解码失败仅告警并继续基础报告
  - 新增单测覆盖对象处理失败时基础报告继续且上下文恢复，符合真实缺陷修复
  - 仅剩 stat/needs-squash 阻塞，CLA 与 CI 已通过，squash 后即可合入
- **committer 建议动作**：**需作者 squash 提交并重跑门禁，通过后再合入**

### PR #64：Add Speed-of-light profiling feature

- **作者**：`@fomichevoleg5` · **停留自然时长**：112.9h · **AI 判定**：**🤖 阻塞待解**
- **代码规模**：6 个文件（实质改动文件 6 个，表面改动文件 0 个，新增测试 +0 行）
- **关联 Issue 对齐**：无关联 Issue，新特性未先走方案讨论
- **核心改动摘要**：新增 SOL 分析器与 --sol 选项，评估内核吞吐上限
  - 新增 276 行 SOL 分析器和峰值常量表，需确认 V100 以外架构取值来源
  - report 契约版本放宽到 7 或 8，需评估向后兼容与迁移说明
  - 本次无新增测试文件覆盖，建议补 SpeedOfLightData 生成用例
- **committer 建议动作**：**需作者 squash 提交、补测试并关联 Issue 后再评审**

### PR #63：fix(report): Store operator source text in SourceFiles

- **作者**：`@churkinaleksandr` · **停留自然时长**：115.1h · **AI 判定**：**🤖 值得合入**
- **代码规模**：4 个文件（实质改动文件 4 个，表面改动文件 0 个，新增测试 +0 行）
- **关联 Issue 对齐**：针对性修复 #64 报告缺失完整源文件
- **核心改动摘要**：为 SourceFiles 增加源码全文列并在报告阶段回填，修复报告缺源码
  - bridge.sql 新增可空 SourceFileText 列，SourceFileId 与归档格式保持向后兼容
  - save_source_file_texts 在分析器登记路径后快照全文，并在 tracing 重连前 commit
  - 仅对可读取文件落库，读取失败置空，避免报告生成因路径缺失中断
  - 文档同步说明 SourceFiles 新增全文语义，测试覆盖见作者 654 项 pytest 通过记录
- **committer 建议动作**：**CLA 已签、CI 通过且无冲突，建议 committer 直接合入**

### PR #60：fix(report): collapse the fixpipe twin rows by identity, not by adjacency

- **作者**：`@gcw_EkTYFH3T` · **停留自然时长**：160.3h · **AI 判定**：**🤖 阻塞待解**
- **代码规模**：1 个文件（实质改动文件 1 个，表面改动文件 0 个，新增测试 +0 行）
- **关联 Issue 对齐**：已针对性修复 #56 孪生行重复计数缺陷
- **核心改动摘要**：把 pending 单槽改为按 twin_key 索引的字典，折叠 fixpipe 孪生行，修复 UB 写重复计数
  - SQL 按 CoreId 排序使孪生行不相邻，改用 twin_key 字典匹配，逻辑正确且注释到位
  - 评审建议将指令 ID 纳入 twin_key，避免地址/时刻/大小相同的两次写被误合并
  - 缺少 ci-pipeline-passed 门禁标签，也未新增覆盖该折叠路径的单元测试
- **committer 建议动作**：**暂缓合入：需补齐 ci-pipeline-passed，并回应评审的 key 收紧建议**

### PR #59：fix(record): recognize versioned Python executables

- **作者**：`@liangjinxuan-2026` · **停留自然时长**：186.7h · **AI 判定**：**🤖 值得合入**
- **代码规模**：1 个文件（实质改动文件 1 个，表面改动文件 0 个，新增测试 +0 行）
- **关联 Issue 对齐**：针对性修复 #60 版本化解释器漏判
- **核心改动摘要**：用正则统一识别 python3.11 等版本化解释器并修正 Python 路径判定
  - 将 _PYTHON_COMMAND 改为正则，覆盖 python、python2/3、python3.11、pytest 等命名
  - 同步收敛解释器与 Python 前缀集合，避免两处判定逻辑漂移
  - 作者已同步 master、解决冲突并完成 CPU 验证（11 项测试通过）；建议后续补单测固化
- **committer 建议动作**：**CLA 与 CI 均通过且无冲突，建议直接合入**

### PR #58：fix(report): handle detector output write failures

- **作者**：`@liangjinxuan-2026` · **停留自然时长**：186.7h · **AI 判定**：**🤖 值得合入**
- **代码规模**：2 个文件（实质改动文件 2 个，表面改动文件 0 个，新增测试 +39 行）
- **关联 Issue 对齐**：已关联 #59
- **核心改动摘要**：实质代码改动（2 文件 +63/-28），门禁全绿
  - 守卫判定：substantive_diff: 2 file(s); adds_tests; linked_issue_legit: #59; external_participant: ZhouBX
- **committer 建议动作**：**CLA 与 CI 已通过，建议 committer 完成最终代码检视后合入**

### PR #57：fix(trace): 正确读取 LOAD_2D 的 K 起始位置 (#27)

- **作者**：`@lilong555` · **停留自然时长**：189.8h · **AI 判定**：**🤖 阻塞待解**
- **代码规模**：2 个文件（实质改动文件 2 个，表面改动文件 0 个，新增测试 +62 行）
- **关联 Issue 对齐**：已针对性修复 #27 的 K 起始位置映射错误
- **核心改动摘要**：修正 LOAD_2D 查询中 K 起始位置误取 MStartPosition 的缺陷，并补充回归测试
  - 仅为一行 SQL 字段映射修正，把 KStartPosition 改用真实列，改动精准、风险低
  - 新增 62 行回归测试覆盖 LOAD_2Dv2、LOAD_MX_2Dv2 及三种报告，但测试文件存在重复 import 触发 F811
  - CLA 已签、CI 通过，唯一阻塞为 stat/needs-squash 待清理提交历史
  - 外部参与者已验证修复，建议解决 Ruff 告警后尽快合入
- **committer 建议动作**：**需作者去除重复 import、squash 提交并重跑 CI，门禁满足后再合入**

### PR #56：fix(report): 保留 npu-rep 打包数据库路径中的特殊字符 (#55)

- **作者**：`@lilong555` · **停留自然时长**：190.4h · **AI 判定**：**🤖 值得合入**
- **代码规模**：2 个文件（实质改动文件 2 个，表面改动文件 0 个，新增测试 +48 行）
- **关联 Issue 对齐**：已针对性修复 #55 特殊字符路径打包缺陷
- **核心改动摘要**：改用 as_uri 构造 SQLite 只读连接，修复特殊字符路径下报告归档遗漏
  - db_path.resolve().as_uri() 保留 #、?、%23 等字符，避免 URI 截断导致元数据回退默认值
  - 新增 13 项参数化回归覆盖相对/绝对路径、空格与中文目录及缺失元数据场景，补测充分
  - 仅改一行源码，CLI、DB schema 与报告格式兼容，风险可控
- **committer 建议动作**：**CLA 与 CI 均已通过，外部参与者已复现验证，建议直接合入**

### PR #55：fix(record): preserve shell command strings before launch

- **作者**：`@liangjinxuan-2026` · **停留自然时长**：190.8h · **AI 判定**：**🤖 值得合入**
- **代码规模**：2 个文件（实质改动文件 2 个，表面改动文件 0 个，新增测试 +0 行）
- **关联 Issue 对齐**：针对性修复 #58 引号命令与 URL 被改写缺陷
- **核心改动摘要**：record 入口保留 user_app 原始字符串，避免 Path 归一化篡改命令
  - 两处入口改为传原始 str，build_launch_spec 仍支持 Path，文件目标路径解析行为不变
  - 修复 // 与 https:// 被折叠为单斜杠的问题，作者已本地 CPU 复现并验证 16 项 record 配置测试
- **committer 建议动作**：**CLA 与 CI 门禁全绿，无冲突，建议尽快合入**

### PR #54：docs: fix the npusim report output example

- **作者**：`@liangjinxuan-2026` · **停留自然时长**：191.9h · **AI 判定**：**🤖 值得合入**
- **代码规模**：1 个文件（实质改动文件 1 个，表面改动文件 0 个，新增测试 +0 行）
- **关联 Issue 对齐**：已按 #54 修正 report 示例与产物说明
- **核心改动摘要**：修正 report 示例，将 -o 误写为 JSON 文件路径改为输出目录
  - 仅改 main.py docstring 说明文字，不改变 CLI 行为，风险极低
  - 示例与 report -o 接收目录、按核生成 Chrome Tracing JSON 的实现一致
- **committer 建议动作**：**CLA 已签、CI 通过且冲突已解，建议直接合入**

### PR #53：fix(report): order the busy-time sweep by interval start

- **作者**：`@gcw_EkTYFH3T` · **停留自然时长**：211h · **AI 判定**：**🤖 阻塞待解**
- **代码规模**：1 个文件（实质改动文件 1 个，表面改动文件 0 个，新增测试 +0 行）
- **关联 Issue 对齐**：已针对性修复 #53 带宽低估缺陷
- **核心改动摘要**：修正吞吐统计区间并集算法，扫描前按起点排序，避免占用时间多算
  - 在 calc_throughput_stats 入参处补按 TickStart 排序，固化区间并集前提，避免重复结算已关闭窗口
  - 作者称同文件 get_fixp_throughput_ub 内联副本亦同步修正，需确认第二处排序已落到 diff 中
  - 评审者用 [0,10)[10,20)[2,50) 复现：占用时间 58→50，其余 37 项吞吐指标无回归
- **committer 建议动作**：**已获 lgtm，但缺 ci-pipeline-passed，需重跑 CI 全绿后合入**

