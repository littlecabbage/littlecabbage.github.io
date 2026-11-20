# PR & Issue 智能治理 Review 报告 · cann/npu-simulator

| 维度 | 详情 |
|---|---|
| **目标仓库** | [cann/npu-simulator](https://gitcode.com/cann/npu-simulator)（GitCode） |
| **巡检时间** | 2026-11-20 22:38 (UTC+8) |
| **分析引擎** | `gitcode-issue-triage` 确定性守卫 + Pi Agent (`cannbot/deepseek-v4.1-flash`) |
| **判定原则** | 宁漏勿错：强灌水信号 + 无安全否决 → 低价值候选；有任何实质代码/测试/关联 Issue → 保留并给出合路建议 |

---

## 一、执行摘要（供 on-call & committer 速览）

- **Issue 巡检**：共扫描 **65** 条 Issue，判定 KEEP **64** / CLOSE 候选 **0** / 待人工复核 **1**。
- **Open PR 总览（共 12 个）**：
  - ✅ **可立即合入（4 个）**：#68、#63、#57、#56
  - ⚠️ **实质贡献但门禁阻塞（8 个）**：#67、#64、#60、#59、#58、#55、#54、#53
  - 🧹 **低价值/表面改动候选（0 个）**：无

## 二、Open PR 逐条深度评审与行动清单

| PR | AI 结论 | 合路门禁 | 关联 Issue | 改动规模 (实质文件) | AI 改动摘要与关联对齐 | committer 建议动作 |
|---|---|---|---|---|---|---|
| [#68](https://gitcode.com/cann/npu-simulator/pulls/68) | **🤖 值得合入** | ✅ 可合入 | [#65](https://gitcode.com/cann/npu-simulator/issues/65) | +41/-949 (19/19 实质) | 删除逐指令动态 IPC 计算、trace 字段与相关表，保留聚合 IPC 指标（已针对性实现 #65 需求，移除逐指令 IPC） | CLA 与 CI 全绿、无冲突阻塞，建议直接合入 |
| [#67](https://gitcode.com/cann/npu-simulator/pulls/67) | **🤖 阻塞待解** | ❌ 阻塞标签 stat/needs-squash | [#63](https://gitcode.com/cann/npu-simulator/issues/63) | +67/-145 (11/11 实质) | 可选处理失败时保留基础报告，移除非必要 Roofline JSON 导出（针对性修复 #63 可选报告失败阻塞导出） | 需作者 squash 提交并重跑门禁，通过后再合入 |
| [#64](https://gitcode.com/cann/npu-simulator/pulls/64) | **🤖 阻塞待解** | ❌ 阻塞标签 stat/needs-squash | — | +330/-2 (6/6 实质) | 新增 SOL 分析器与 --sol 选项，评估内核吞吐上限（无关联 Issue，新特性未先走方案讨论） | 需作者 squash 提交、补测试并关联 Issue 后再评审 |
| [#63](https://gitcode.com/cann/npu-simulator/pulls/63) | **🤖 值得合入** | ✅ 可合入 | [#64](https://gitcode.com/cann/npu-simulator/issues/64) | +92/-11 (4/4 实质) | 为 SourceFiles 增加源码全文列并在报告阶段回填，修复报告缺源码（针对性修复 #64 报告缺失完整源文件） | CLA 已签、CI 通过且无冲突，建议 committer 直接合入 |
| [#60](https://gitcode.com/cann/npu-simulator/pulls/60) | **🤖 阻塞待解** | ❌ 缺 ci-pipeline-passed | [#56](https://gitcode.com/cann/npu-simulator/issues/56) | +11/-5 (1/1 实质) | 把 pending 单槽改为按 twin_key 索引的字典，折叠 fixpipe 孪生行，修复 UB 写重复计数（已针对性修复 #56 孪生行重复计数缺陷） | 暂缓合入：需补齐 ci-pipeline-passed，并回应评审的 key 收紧建议 |
| [#59](https://gitcode.com/cann/npu-simulator/pulls/59) | **🤖 阻塞待解** | ❌ 缺 ci-pipeline-passed | [#60](https://gitcode.com/cann/npu-simulator/issues/60) | +26/-20 (1/1 实质) | 用正则匹配 python3.11 等带版本号的 Python 解释器，修复记录分类（针对性修复 #60 版本化解释器识别缺陷） | 需先修复 CI 失败并重跑流水线通过后再合入 |
| [#58](https://gitcode.com/cann/npu-simulator/pulls/58) | **🤖 阻塞待解** | ❌ 缺 ci-pipeline-passed；存在代码冲突 | [#59](https://gitcode.com/cann/npu-simulator/issues/59) | +66/-27 (2/2 实质) | 修复检测报告写入失败再次抛错，改为记录日志并返回失败（针对性修复 #59 报告写失败逃逸缺陷） | 需作者解决合并冲突、修复 CI 失败并重跑门禁 |
| [#57](https://gitcode.com/cann/npu-simulator/pulls/57) | **🤖 值得合入** | ✅ 可合入 | [#27](https://gitcode.com/cann/npu-simulator/issues/27) | +64/-2 (2/2 实质) | 修正 LOAD_2D 查询误将 MStartPosition 当作 K 起始位置（已针对性修复 #27 的 K 起始位置缺陷） | 门禁全绿，建议作者清理重复导入后合入 |
| [#56](https://gitcode.com/cann/npu-simulator/pulls/56) | **🤖 值得合入** | ✅ 可合入 | [#55](https://gitcode.com/cann/npu-simulator/issues/55) | +49/-1 (2/2 实质) | 修复 npu-rep 打包时特殊字符路径下 SQLite URI 解析错误，避免报告 JSON 遗漏（已针对性修复 #55 URI 路径缺陷） | 门禁全绿且经社区独立复现验证，建议直接合入 |
| [#55](https://gitcode.com/cann/npu-simulator/pulls/55) | **🤖 阻塞待解** | ❌ 缺 ci-pipeline-passed | [#58](https://gitcode.com/cann/npu-simulator/issues/58) | +2/-2 (2/2 实质) | 将记录入口的 user_app 保持原始字符串，避免 Path 归一化破坏 shell 命令（针对性修复 #58 引号命令被改写缺陷） | 需排查 UT checkout 凭证故障并重跑 CI，通过后再合入 |
| [#54](https://gitcode.com/cann/npu-simulator/pulls/54) | **🤖 阻塞待解** | ❌ 存在代码冲突 | [#54](https://gitcode.com/cann/npu-simulator/issues/54) | +2/-3 (1/1 实质) | 修正 npusim report 示例，将 -o 改为输出目录并更新产物说明（已针对性修复 #54 报告输出路径描述缺陷） | 需作者先解决合并冲突并重跑 CI，门禁全绿后再评审合入 |
| [#53](https://gitcode.com/cann/npu-simulator/pulls/53) | **🤖 阻塞待解** | ❌ 缺 ci-pipeline-passed | [#53](https://gitcode.com/cann/npu-simulator/issues/53) | +9/-0 (1/1 实质) | 修正吞吐统计区间并集算法，扫描前按起点排序，避免占用时间多算（已针对性修复 #53 带宽低估缺陷） | 已获 lgtm，但缺 ci-pipeline-passed，需重跑 CI 全绿后合入 |

### PR #68：Remove misleading per-instruction IPC metrics

- **作者**：`@churkinaleksandr` · **停留自然时长**：2.1h · **AI 判定**：**🤖 值得合入**
- **代码规模**：19 个文件（实质改动文件 19 个，表面改动文件 0 个，新增测试 +10 行）
- **关联 Issue 对齐**：已针对性实现 #65 需求，移除逐指令 IPC
- **核心改动摘要**：删除逐指令动态 IPC 计算、trace 字段与相关表，保留聚合 IPC 指标
  - 净删约 900 行，移除 ScalarIpcDynamic/VfIPCDynamic 表、视图及 prof_demo 回退实现，降低维护成本
  - 同步更新文档与参数说明，并新增测试校验旧库重分析后不再生成动态 IPC 表
- **committer 建议动作**：**CLA 与 CI 全绿、无冲突阻塞，建议直接合入**

### PR #67：fix(prof): preserve base reports when optional processing fails

- **作者**：`@churkinaleksandr` · **停留自然时长**：24.2h · **AI 判定**：**🤖 阻塞待解**
- **代码规模**：11 个文件（实质改动文件 11 个，表面改动文件 0 个，新增测试 +15 行）
- **关联 Issue 对齐**：针对性修复 #63 可选报告失败阻塞导出
- **核心改动摘要**：可选处理失败时保留基础报告，移除非必要 Roofline JSON 导出
  - 删除独立 roofline.json 导出，Roofline 数据仍保留在 SQLite 表与 CSV 中，避免可选失败阻断打包
  - Critical Path 改为临时目录生成、成功后再发布，ELF 解码失败仅告警并继续基础报告
  - 新增单测覆盖对象处理失败时基础报告继续且上下文恢复，符合真实缺陷修复
  - 仅剩 stat/needs-squash 阻塞，CLA 与 CI 已通过，squash 后即可合入
- **committer 建议动作**：**需作者 squash 提交并重跑门禁，通过后再合入**

### PR #64：Add Speed-of-light profiling feature

- **作者**：`@fomichevoleg5` · **停留自然时长**：71.9h · **AI 判定**：**🤖 阻塞待解**
- **代码规模**：6 个文件（实质改动文件 6 个，表面改动文件 0 个，新增测试 +0 行）
- **关联 Issue 对齐**：无关联 Issue，新特性未先走方案讨论
- **核心改动摘要**：新增 SOL 分析器与 --sol 选项，评估内核吞吐上限
  - 新增 276 行 SOL 分析器和峰值常量表，需确认 V100 以外架构取值来源
  - report 契约版本放宽到 7 或 8，需评估向后兼容与迁移说明
  - 本次无新增测试文件覆盖，建议补 SpeedOfLightData 生成用例
- **committer 建议动作**：**需作者 squash 提交、补测试并关联 Issue 后再评审**

### PR #63：fix(report): Store operator source text in SourceFiles

- **作者**：`@churkinaleksandr` · **停留自然时长**：74.1h · **AI 判定**：**🤖 值得合入**
- **代码规模**：4 个文件（实质改动文件 4 个，表面改动文件 0 个，新增测试 +0 行）
- **关联 Issue 对齐**：针对性修复 #64 报告缺失完整源文件
- **核心改动摘要**：为 SourceFiles 增加源码全文列并在报告阶段回填，修复报告缺源码
  - bridge.sql 新增可空 SourceFileText 列，SourceFileId 与归档格式保持向后兼容
  - save_source_file_texts 在分析器登记路径后快照全文，并在 tracing 重连前 commit
  - 仅对可读取文件落库，读取失败置空，避免报告生成因路径缺失中断
  - 文档同步说明 SourceFiles 新增全文语义，测试覆盖见作者 654 项 pytest 通过记录
- **committer 建议动作**：**CLA 已签、CI 通过且无冲突，建议 committer 直接合入**

### PR #60：fix(report): collapse the fixpipe twin rows by identity, not by adjacency

- **作者**：`@gcw_EkTYFH3T` · **停留自然时长**：119.3h · **AI 判定**：**🤖 阻塞待解**
- **代码规模**：1 个文件（实质改动文件 1 个，表面改动文件 0 个，新增测试 +0 行）
- **关联 Issue 对齐**：已针对性修复 #56 孪生行重复计数缺陷
- **核心改动摘要**：把 pending 单槽改为按 twin_key 索引的字典，折叠 fixpipe 孪生行，修复 UB 写重复计数
  - SQL 按 CoreId 排序使孪生行不相邻，改用 twin_key 字典匹配，逻辑正确且注释到位
  - 评审建议将指令 ID 纳入 twin_key，避免地址/时刻/大小相同的两次写被误合并
  - 缺少 ci-pipeline-passed 门禁标签，也未新增覆盖该折叠路径的单元测试
- **committer 建议动作**：**暂缓合入：需补齐 ci-pipeline-passed，并回应评审的 key 收紧建议**

### PR #59：fix(record): recognize versioned Python executables

- **作者**：`@liangjinxuan-2026` · **停留自然时长**：145.7h · **AI 判定**：**🤖 阻塞待解**
- **代码规模**：1 个文件（实质改动文件 1 个，表面改动文件 0 个，新增测试 +0 行）
- **关联 Issue 对齐**：针对性修复 #60 版本化解释器识别缺陷
- **核心改动摘要**：用正则匹配 python3.11 等带版本号的 Python 解释器，修复记录分类
  - 将 _PYTHON_TOKENS 集合替换为 _PYTHON_COMMAND 正则，覆盖 python3.x/pytest 前缀匹配
  - 需确认 _INTERPRETER_TOKENS 移除 python 后，archive 标签回退到脚本名的逻辑无回归
- **committer 建议动作**：**需先修复 CI 失败并重跑流水线通过后再合入**

### PR #58：fix(report): handle detector output write failures

- **作者**：`@liangjinxuan-2026` · **停留自然时长**：145.7h · **AI 判定**：**🤖 阻塞待解**
- **代码规模**：2 个文件（实质改动文件 2 个，表面改动文件 0 个，新增测试 +41 行）
- **关联 Issue 对齐**：针对性修复 #59 报告写失败逃逸缺陷
- **核心改动摘要**：修复检测报告写入失败再次抛错，改为记录日志并返回失败
  - 抽出 _write_detection_report 统一处理 OSError，避免错误处理二次写同路径导致异常逃逸
  - 新增 41 行 UT 覆盖写失败后可写与持续失败两种场景，测试覆盖充分
- **committer 建议动作**：**需作者解决合并冲突、修复 CI 失败并重跑门禁**

### PR #57：fix(trace): 正确读取 LOAD_2D 的 K 起始位置 (#27)

- **作者**：`@lilong555` · **停留自然时长**：148.8h · **AI 判定**：**🤖 值得合入**
- **代码规模**：2 个文件（实质改动文件 2 个，表面改动文件 0 个，新增测试 +63 行）
- **关联 Issue 对齐**：已针对性修复 #27 的 K 起始位置缺陷
- **核心改动摘要**：修正 LOAD_2D 查询误将 MStartPosition 当作 K 起始位置
  - SQL 字段改为 DmaMovLoad2dParams.KStartPosition，与消费处 k_start_pos_bytes 对齐
  - 新增 18 项回归覆盖 LOAD_2Dv2/LOAD_MX_2Dv2 及默认、Smart Pipe、Critical Path 报告
  - 外部评审确认回归全通过，仅剩 tests 中 biprof_ctx 重复导入引发 Ruff F811，需顺手清掉
  - DB schema、报告字段名与 CLI 均无变化，向后兼容风险低
- **committer 建议动作**：**门禁全绿，建议作者清理重复导入后合入**

### PR #56：fix(report): 保留 npu-rep 打包数据库路径中的特殊字符 (#55)

- **作者**：`@lilong555` · **停留自然时长**：149.4h · **AI 判定**：**🤖 值得合入**
- **代码规模**：2 个文件（实质改动文件 2 个，表面改动文件 0 个，新增测试 +48 行）
- **关联 Issue 对齐**：已针对性修复 #55 URI 路径缺陷
- **核心改动摘要**：修复 npu-rep 打包时特殊字符路径下 SQLite URI 解析错误，避免报告 JSON 遗漏
  - 改用 db_path.resolve().as_uri() 构造只读 URI，正确保留 #、?、%23 等特殊字符，kernel 元数据不再回退默认值
  - 新增 13 项参数化回归，覆盖相对与绝对路径、特殊字符、空格及中文目录，并校验归档内容完整性
- **committer 建议动作**：**门禁全绿且经社区独立复现验证，建议直接合入**

### PR #55：fix(record): preserve shell command strings before launch

- **作者**：`@liangjinxuan-2026` · **停留自然时长**：149.8h · **AI 判定**：**🤖 阻塞待解**
- **代码规模**：2 个文件（实质改动文件 2 个，表面改动文件 0 个，新增测试 +0 行）
- **关联 Issue 对齐**：针对性修复 #58 引号命令被改写缺陷
- **核心改动摘要**：将记录入口的 user_app 保持原始字符串，避免 Path 归一化破坏 shell 命令
  - 改动仅两处：移除 handle_record_command 与 build_record_config_from_args 中的 Path() 转换
  - build_launch_spec 已支持 str/Path，文件路径解析逻辑不受影响，修复思路正确
  - CI 因 UT 取码认证失败（HTTP Basic Access denied）未通过，需基础设施侧修复后重跑
  - 缺少新增测试覆盖引号命令与 URL 保留场景，建议补充回归用例
- **committer 建议动作**：**需排查 UT checkout 凭证故障并重跑 CI，通过后再合入**

### PR #54：docs: fix the npusim report output example

- **作者**：`@liangjinxuan-2026` · **停留自然时长**：150.9h · **AI 判定**：**🤖 阻塞待解**
- **代码规模**：1 个文件（实质改动文件 1 个，表面改动文件 0 个，新增测试 +0 行）
- **关联 Issue 对齐**：已针对性修复 #54 报告输出路径描述缺陷
- **核心改动摘要**：修正 npusim report 示例，将 -o 改为输出目录并更新产物说明
  - 仅改 main.py docstring 示例文字，不改变 CLI 行为，与 report 参数定义一致
  - 示例 -e 改为运行记录目录、-o 改为 ./output/reports，并说明生成按核拆分 JSON，语义正确
  - 当前存在 merge_conflicts 阻塞，需 rebase 解决后再触发编译验证
- **committer 建议动作**：**需作者先解决合并冲突并重跑 CI，门禁全绿后再评审合入**

### PR #53：fix(report): order the busy-time sweep by interval start

- **作者**：`@gcw_EkTYFH3T` · **停留自然时长**：170h · **AI 判定**：**🤖 阻塞待解**
- **代码规模**：1 个文件（实质改动文件 1 个，表面改动文件 0 个，新增测试 +0 行）
- **关联 Issue 对齐**：已针对性修复 #53 带宽低估缺陷
- **核心改动摘要**：修正吞吐统计区间并集算法，扫描前按起点排序，避免占用时间多算
  - 在 calc_throughput_stats 入参处补按 TickStart 排序，固化区间并集前提，避免重复结算已关闭窗口
  - 作者称同文件 get_fixp_throughput_ub 内联副本亦同步修正，需确认第二处排序已落到 diff 中
  - 评审者用 [0,10)[10,20)[2,50) 复现：占用时间 58→50，其余 37 项吞吐指标无回归
- **committer 建议动作**：**已获 lgtm，但缺 ci-pipeline-passed，需重跑 CI 全绿后合入**

