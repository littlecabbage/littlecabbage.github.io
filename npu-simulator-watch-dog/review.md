# PR & Issue 智能治理 Review 报告 · cann/npu-simulator

| 维度 | 详情 |
|---|---|
| **目标仓库** | [cann/npu-simulator](https://gitcode.com/cann/npu-simulator)（GitCode） |
| **巡检时间** | 2026-11-20 05:38 (UTC+8) |
| **分析引擎** | `gitcode-issue-triage` 确定性守卫 + Pi Agent (`cannbot/deepseek-v4.1-flash`) |
| **判定原则** | 宁漏勿错：强灌水信号 + 无安全否决 → 低价值候选；有任何实质代码/测试/关联 Issue → 保留并给出合路建议 |

---

## 一、执行摘要（供 on-call & committer 速览）

- **Issue 巡检**：共扫描 **63** 条 Issue，判定 KEEP **62** / CLOSE 候选 **0** / 待人工复核 **1**。
- **Open PR 总览（共 13 个）**：
  - ✅ **可立即合入（4 个）**：#66、#57、#56、#54
  - ⚠️ **实质贡献但门禁阻塞（9 个）**：#67、#64、#63、#60、#59、#58、#55、#53、#52
  - 🧹 **低价值/表面改动候选（0 个）**：无

## 二、Open PR 逐条深度评审与行动清单

| PR | AI 结论 | 合路门禁 | 关联 Issue | 改动规模 (实质文件) | AI 改动摘要与关联对齐 | committer 建议动作 |
|---|---|---|---|---|---|---|
| [#67](https://gitcode.com/cann/npu-simulator/pulls/67) | **🤖 阻塞待解** | ❌ 阻塞标签 stat/needs-squash | [#63](https://gitcode.com/cann/npu-simulator/issues/63) | +67/-145 (11/11 实质) | 移除 roofline.json 导出，可选处理失败降级保留基础报告（针对性修复 #63 可选报告失败缺陷） | 需作者 squash 提交并重跑门禁后再合入 |
| [#66](https://gitcode.com/cann/npu-simulator/pulls/66) | **🤖 值得合入** | ✅ 可合入 | [#61](https://gitcode.com/cann/npu-simulator/issues/61) | +1/-1 (1/1 实质) | 修正 compile.sh 中误写的仓库名 ops-math 为 npu-simulator（已针对性修复 #61 仓库名复制残留） | CLA 与 CI 门禁全绿、无冲突，建议直接合入 |
| [#64](https://gitcode.com/cann/npu-simulator/pulls/64) | **🤖 阻塞待解** | ❌ 阻塞标签 stat/needs-squash | — | +330/-2 (6/6 实质) | 新增 SOL 分析器与 --sol 选项，评估内核吞吐上限（无关联 Issue，新特性未先走方案讨论） | 需作者 squash 提交、补测试并关联 Issue 后再评审 |
| [#63](https://gitcode.com/cann/npu-simulator/pulls/63) | **🤖 阻塞待解** | ❌ 缺 ci-pipeline-passed；阻塞标签 stat/needs-squash | — | +92/-15 (3/3 实质) | 将算子源文件以 txt 类型嵌入 .npu-rep 归档，补全源码查看功能（无关联 Issue，属功能补全） | 需作者 squash 提交、补充测试并重跑 CI 取得通过标签后再合入 |
| [#60](https://gitcode.com/cann/npu-simulator/pulls/60) | **🤖 阻塞待解** | ❌ 缺 ci-pipeline-passed | [#56](https://gitcode.com/cann/npu-simulator/issues/56) | +11/-5 (1/1 实质) | 将孪生行折叠由相邻匹配改为按 twin_key 字典匹配,修复 UB 写重复计数（已针对性修复 #56 孪生行不相邻导致的重复计入） | 需作者触发 CI 并获 ci-pipeline-passed 标签后,再复核合入 |
| [#59](https://gitcode.com/cann/npu-simulator/pulls/59) | **🤖 阻塞待解** | ❌ 缺 ci-pipeline-passed | [#60](https://gitcode.com/cann/npu-simulator/issues/60) | +26/-20 (1/1 实质) | 用正则匹配 python3.11 等带版本号的 Python 解释器，修复记录分类（针对性修复 #60 版本化解释器识别缺陷） | 需先修复 CI 失败并重跑流水线通过后再合入 |
| [#58](https://gitcode.com/cann/npu-simulator/pulls/58) | **🤖 阻塞待解** | ❌ 缺 ci-pipeline-passed | [#59](https://gitcode.com/cann/npu-simulator/issues/59) | +23/-27 (1/1 实质) | 修复检测报告写入失败时重复抛错并中断后续检测（针对性修复 #59 报告写入异常逃逸） | CI 流水线失败，需作者修复后重跑并通过再合入 |
| [#57](https://gitcode.com/cann/npu-simulator/pulls/57) | **🤖 值得合入** | ✅ 可合入 | [#27](https://gitcode.com/cann/npu-simulator/issues/27) | +64/-2 (2/2 实质) | 修正 LOAD_2D 查询把 K 起始位置错取为 MStartPosition 的缺陷（已针对性修复 #27 的 K 起始位置缺陷） | CLA 与 CI 全绿、无冲突，建议检视通过后直接合入 |
| [#56](https://gitcode.com/cann/npu-simulator/pulls/56) | **🤖 值得合入** | ✅ 可合入 | [#55](https://gitcode.com/cann/npu-simulator/issues/55) | +49/-1 (2/2 实质) | 用 as_uri 修复 SQLite 路径特殊字符，报告打包不再遗漏 JSON（针对性修复 #55 的 URI 特殊字符路径缺陷） | CLA 与 CI 已全绿，检视通过后可直接合入 |
| [#55](https://gitcode.com/cann/npu-simulator/pulls/55) | **🤖 阻塞待解** | ❌ 缺 ci-pipeline-passed | [#58](https://gitcode.com/cann/npu-simulator/issues/58) | +2/-2 (2/2 实质) | 将记录入口的 user_app 保持原始字符串，避免 Path 归一化破坏 shell 命令（针对性修复 #58 引号命令被改写缺陷） | 需排查 UT checkout 凭证故障并重跑 CI，通过后再合入 |
| [#54](https://gitcode.com/cann/npu-simulator/pulls/54) | **🤖 值得合入** | ✅ 可合入 | [#54](https://gitcode.com/cann/npu-simulator/issues/54) | +2/-3 (1/1 实质) | 修正 npusim report 示例输出路径为目录，并说明按核生成 tracing JSON（已针对性修复 #54 报告输出路径示例错误） | CLA 与 CI 均已通过、无冲突，建议直接合入 |
| [#53](https://gitcode.com/cann/npu-simulator/pulls/53) | **🤖 阻塞待解** | ❌ 缺 ci-pipeline-passed | [#53](https://gitcode.com/cann/npu-simulator/issues/53) | +9/-0 (1/1 实质) | 两处区间并集扫描前按 TickStart 预排序，修正带宽统计被低估（已针对性修复 #53 带宽低估缺陷） | 需作者补齐 ci-pipeline-passed 门禁并重跑流水线，全绿后可合入 |
| [#52](https://gitcode.com/cann/npu-simulator/pulls/52) | **🤖 阻塞待解** | ❌ 阻塞标签 stat/needs-squash | — | +360/-114 (13/13 实质) | 为 record 新增 --timeout 超时限制，超时后终止进程组并归档部分产物（无关联 Issue，属新功能提案） | 需作者 squash 提交以清除 stat/needs-squash 阻塞，再重跑 CI 后合入 |

### PR #67：fix(prof): preserve base reports when optional processing fails

- **作者**：`@churkinaleksandr` · **停留自然时长**：7.2h · **AI 判定**：**🤖 阻塞待解**
- **代码规模**：11 个文件（实质改动文件 11 个，表面改动文件 0 个，新增测试 +15 行）
- **关联 Issue 对齐**：针对性修复 #63 可选报告失败缺陷
- **核心改动摘要**：移除 roofline.json 导出，可选处理失败降级保留基础报告
  - 删除独立 roofline.json 导出，Roofline 结果保留在 SQLite 表及 CSV
  - 设备 ELF 解码与 Critical Path 失败改为告警并继续基础报告，已补测试
- **committer 建议动作**：**需作者 squash 提交并重跑门禁后再合入**

### PR #66：fix(ci): correct REPOSITORY_NAME in compile.sh

- **作者**：`@chenge1` · **停留自然时长**：32.5h · **AI 判定**：**🤖 值得合入**
- **代码规模**：1 个文件（实质改动文件 1 个，表面改动文件 0 个，新增测试 +0 行）
- **关联 Issue 对齐**：已针对性修复 #61 仓库名复制残留
- **核心改动摘要**：修正 compile.sh 中误写的仓库名 ops-math 为 npu-simulator
  - 单行修正 REPOSITORY_NAME，使日志与断言信息指向正确仓库 npu-simulator
  - 关联 Issue #61 描述的具体缺陷被精准覆盖，改动风险低、无副作用
- **committer 建议动作**：**CLA 与 CI 门禁全绿、无冲突，建议直接合入**

### PR #64：Add Speed-of-light profiling feature

- **作者**：`@fomichevoleg5` · **停留自然时长**：54.9h · **AI 判定**：**🤖 阻塞待解**
- **代码规模**：6 个文件（实质改动文件 6 个，表面改动文件 0 个，新增测试 +0 行）
- **关联 Issue 对齐**：无关联 Issue，新特性未先走方案讨论
- **核心改动摘要**：新增 SOL 分析器与 --sol 选项，评估内核吞吐上限
  - 新增 276 行 SOL 分析器和峰值常量表，需确认 V100 以外架构取值来源
  - report 契约版本放宽到 7 或 8，需评估向后兼容与迁移说明
  - 本次无新增测试文件覆盖，建议补 SpeedOfLightData 生成用例
- **committer 建议动作**：**需作者 squash 提交、补测试并关联 Issue 后再评审**

### PR #63：[WIP] fix(report): Embed operator source files into .npu-rep archives (fix to complete Source/Assembly feature support)

- **作者**：`@churkinaleksandr` · **停留自然时长**：57.1h · **AI 判定**：**🤖 阻塞待解**
- **代码规模**：3 个文件（实质改动文件 3 个，表面改动文件 0 个，新增测试 +0 行）
- **关联 Issue 对齐**：无关联 Issue，属功能补全
- **核心改动摘要**：将算子源文件以 txt 类型嵌入 .npu-rep 归档，补全源码查看功能
  - 新增 .txt=7 文件类型，打包时写入完整源文件，根因修复清晰
  - 同步更新 source_assembly_data_format.md，格式说明一致
  - 无新增测试，缺 ci-pipeline-passed 且含 needs-squash 阻塞
  - PR 仍标 WIP，需作者确认可评审并逐条答复意见
- **committer 建议动作**：**需作者 squash 提交、补充测试并重跑 CI 取得通过标签后再合入**

### PR #60：fix(report): collapse the fixpipe twin rows by identity, not by adjacency

- **作者**：`@gcw_EkTYFH3T` · **停留自然时长**：102.3h · **AI 判定**：**🤖 阻塞待解**
- **代码规模**：1 个文件（实质改动文件 1 个，表面改动文件 0 个，新增测试 +0 行）
- **关联 Issue 对齐**：已针对性修复 #56 孪生行不相邻导致的重复计入
- **核心改动摘要**：将孪生行折叠由相邻匹配改为按 twin_key 字典匹配,修复 UB 写重复计数
  - 孪生行 CoreId 不同且查询按 CoreId 排序,原相邻假设确实不成立,改用 twin_key 字典正确
  - 改动仅 11 增 5 删、单文件,风险可控,但缺少回归测试验证双视图计数不再翻倍
- **committer 建议动作**：**需作者触发 CI 并获 ci-pipeline-passed 标签后,再复核合入**

### PR #59：fix(record): recognize versioned Python executables

- **作者**：`@liangjinxuan-2026` · **停留自然时长**：128.7h · **AI 判定**：**🤖 阻塞待解**
- **代码规模**：1 个文件（实质改动文件 1 个，表面改动文件 0 个，新增测试 +0 行）
- **关联 Issue 对齐**：针对性修复 #60 版本化解释器识别缺陷
- **核心改动摘要**：用正则匹配 python3.11 等带版本号的 Python 解释器，修复记录分类
  - 将 _PYTHON_TOKENS 集合替换为 _PYTHON_COMMAND 正则，覆盖 python3.x/pytest 前缀匹配
  - 需确认 _INTERPRETER_TOKENS 移除 python 后，archive 标签回退到脚本名的逻辑无回归
- **committer 建议动作**：**需先修复 CI 失败并重跑流水线通过后再合入**

### PR #58：fix(report): handle detector output write failures

- **作者**：`@liangjinxuan-2026` · **停留自然时长**：128.7h · **AI 判定**：**🤖 阻塞待解**
- **代码规模**：1 个文件（实质改动文件 1 个，表面改动文件 0 个，新增测试 +0 行）
- **关联 Issue 对齐**：针对性修复 #59 报告写入异常逃逸
- **核心改动摘要**：修复检测报告写入失败时重复抛错并中断后续检测
  - 将报告写入抽为 _write_detection_report，捕获 OSError 并返回布尔失败，避免二次异常逃逸
  - 单文件实质改动，无新增测试；CI 失败需排查，建议补充目录路径写入失败用例
- **committer 建议动作**：**CI 流水线失败，需作者修复后重跑并通过再合入**

### PR #57：fix(trace): 正确读取 LOAD_2D 的 K 起始位置 (#27)

- **作者**：`@lilong555` · **停留自然时长**：131.8h · **AI 判定**：**🤖 值得合入**
- **代码规模**：2 个文件（实质改动文件 2 个，表面改动文件 0 个，新增测试 +63 行）
- **关联 Issue 对齐**：已针对性修复 #27 的 K 起始位置缺陷
- **核心改动摘要**：修正 LOAD_2D 查询把 K 起始位置错取为 MStartPosition 的缺陷
  - SQL 字段映射由 MStartPosition 改为 KStartPosition，与 DB 真实列一致，改动最小且精准
  - 新增 63 行回归测试，覆盖 LOAD_2Dv2/LOAD_MX_2Dv2、独立 M/K 起点及三种报告链路
- **committer 建议动作**：**CLA 与 CI 全绿、无冲突，建议检视通过后直接合入**

### PR #56：fix(report): 保留 npu-rep 打包数据库路径中的特殊字符 (#55)

- **作者**：`@lilong555` · **停留自然时长**：132.4h · **AI 判定**：**🤖 值得合入**
- **代码规模**：2 个文件（实质改动文件 2 个，表面改动文件 0 个，新增测试 +48 行）
- **关联 Issue 对齐**：针对性修复 #55 的 URI 特殊字符路径缺陷
- **核心改动摘要**：用 as_uri 修复 SQLite 路径特殊字符，报告打包不再遗漏 JSON
  - 单行改动将 db_path 转为 as_uri() 只读 URI，避免 #、?、%23 被 URI 解析截断
  - 新增 13 项参数化回归，覆盖相对/绝对路径、特殊字符、中文空格及归档内容
- **committer 建议动作**：**CLA 与 CI 已全绿，检视通过后可直接合入**

### PR #55：fix(record): preserve shell command strings before launch

- **作者**：`@liangjinxuan-2026` · **停留自然时长**：132.8h · **AI 判定**：**🤖 阻塞待解**
- **代码规模**：2 个文件（实质改动文件 2 个，表面改动文件 0 个，新增测试 +0 行）
- **关联 Issue 对齐**：针对性修复 #58 引号命令被改写缺陷
- **核心改动摘要**：将记录入口的 user_app 保持原始字符串，避免 Path 归一化破坏 shell 命令
  - 改动仅两处：移除 handle_record_command 与 build_record_config_from_args 中的 Path() 转换
  - build_launch_spec 已支持 str/Path，文件路径解析逻辑不受影响，修复思路正确
  - CI 因 UT 取码认证失败（HTTP Basic Access denied）未通过，需基础设施侧修复后重跑
  - 缺少新增测试覆盖引号命令与 URL 保留场景，建议补充回归用例
- **committer 建议动作**：**需排查 UT checkout 凭证故障并重跑 CI，通过后再合入**

### PR #54：docs: fix the npusim report output example

- **作者**：`@liangjinxuan-2026` · **停留自然时长**：133.9h · **AI 判定**：**🤖 值得合入**
- **代码规模**：1 个文件（实质改动文件 1 个，表面改动文件 0 个，新增测试 +0 行）
- **关联 Issue 对齐**：已针对性修复 #54 报告输出路径示例错误
- **核心改动摘要**：修正 npusim report 示例输出路径为目录，并说明按核生成 tracing JSON
  - 仅改 main.py docstring 示例文字，未变动 CLI 行为，风险极低
  - 示例与 -o 接收目录、按核 trace_coreN.json 的实现一致，文档更准确
- **committer 建议动作**：**CLA 与 CI 均已通过、无冲突，建议直接合入**

### PR #53：fix(report): order the busy-time sweep by interval start

- **作者**：`@gcw_EkTYFH3T` · **停留自然时长**：153h · **AI 判定**：**🤖 阻塞待解**
- **代码规模**：1 个文件（实质改动文件 1 个，表面改动文件 0 个，新增测试 +0 行）
- **关联 Issue 对齐**：已针对性修复 #53 带宽低估缺陷
- **核心改动摘要**：两处区间并集扫描前按 TickStart 预排序，修正带宽统计被低估
  - 在 calc_throughput_stats 与被调内联副本两处扫描前各加一次按起点排序，代价 O(n log n)、可接受
  - 选择在调用方固化有序前提、保留原 ORDER BY TickEnd，避免改动 8 处 SQL，兼容性更好
  - 逻辑正确但未新增单测；建议补充交错区间用例（长传输与短传输重叠）以防回归
  - 仅缺 ci-pipeline-passed 标签，CLA 已通过、无冲突与 squash 问题，补跑 CI 即可
- **committer 建议动作**：**需作者补齐 ci-pipeline-passed 门禁并重跑流水线，全绿后可合入**

### PR #52：feat(record): 支持 --timeout 限制仿真时长并在超时后自动终止

- **作者**：`@Li_cube` · **停留自然时长**：157.4h · **AI 判定**：**🤖 阻塞待解**
- **代码规模**：13 个文件（实质改动文件 13 个，表面改动文件 0 个，新增测试 +3 行）
- **关联 Issue 对齐**：无关联 Issue，属新功能提案
- **核心改动摘要**：为 record 新增 --timeout 超时限制，超时后终止进程组并归档部分产物
  - 核心改动合理：计时仅覆盖仿真段，超时后 SIGTERM→5s→SIGKILL 终止整个进程组，兼容孙进程
  - 配置解析与回填链路完整：parse_duration/resolve_timeout 支持环境变量回退，RunResult.timed_out 贯通 record 与 ktest
  - 测试覆盖偏弱：13 个文件改动但仅新增 3 行测试，主要为 mock 补字段，缺少超时终止路径的用例
  - 已有 committer /approve 与 ci-pipeline-passed，仅剩 stat/needs-squash 门禁待清理
- **committer 建议动作**：**需作者 squash 提交以清除 stat/needs-squash 阻塞，再重跑 CI 后合入**

