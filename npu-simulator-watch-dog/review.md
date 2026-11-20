# PR & Issue 智能治理 Review 报告 · cann/npu-simulator

| 维度 | 详情 |
|---|---|
| **目标仓库** | [cann/npu-simulator](https://gitcode.com/cann/npu-simulator)（GitCode） |
| **巡检时间** | 2026-11-20 17:38 (UTC+8) |
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
| [#67](https://gitcode.com/cann/npu-simulator/pulls/67) | **🤖 阻塞待解** | ❌ 缺 ci-pipeline-passed；阻塞标签 stat/needs-squash | [#63](https://gitcode.com/cann/npu-simulator/issues/63) | +67/-145 (11/11 实质) | 可选 Roofline/CriticalPath 失败降级，保留基础报告与 .npu-rep 导出（针对性修复 #63 可选报告阻断导出缺陷） | 需作者压缩提交并补 CI 通过后，再安排合入 |
| [#66](https://gitcode.com/cann/npu-simulator/pulls/66) | **🤖 值得合入** | ✅ 可合入 | [#61](https://gitcode.com/cann/npu-simulator/issues/61) | +1/-1 (1/1 实质) | 修正compile.sh中仓库名残留，改为npu-simulator（已针对性修复 #61 仓库名残留缺陷） | CLA与CI已通过、无冲突，建议合入并纳入统一清理 |
| [#64](https://gitcode.com/cann/npu-simulator/pulls/64) | **🤖 阻塞待解** | ❌ 阻塞标签 stat/needs-squash | — | +330/-2 (6/6 实质) | 新增 SOL 分析器与 --sol 选项，评估内核吞吐上限（无关联 Issue，新特性未先走方案讨论） | 需作者 squash 提交、补测试并关联 Issue 后再评审 |
| [#63](https://gitcode.com/cann/npu-simulator/pulls/63) | **🤖 阻塞待解** | ❌ 缺 ci-pipeline-passed；阻塞标签 stat/needs-squash | — | +92/-15 (3/3 实质) | 将算子源文件以 txt 类型嵌入 .npu-rep 归档，补全源码查看功能（无关联 Issue，属功能补全） | 需作者 squash 提交、补充测试并重跑 CI 取得通过标签后再合入 |
| [#60](https://gitcode.com/cann/npu-simulator/pulls/60) | **🤖 阻塞待解** | ❌ 缺 ci-pipeline-passed | [#56](https://gitcode.com/cann/npu-simulator/issues/56) | +11/-5 (1/1 实质) | 将孪生行折叠由相邻匹配改为按 twin_key 字典匹配,修复 UB 写重复计数（已针对性修复 #56 孪生行不相邻导致的重复计入） | 需作者触发 CI 并获 ci-pipeline-passed 标签后,再复核合入 |
| [#59](https://gitcode.com/cann/npu-simulator/pulls/59) | **🤖 阻塞待解** | ❌ 缺 ci-pipeline-passed | [#60](https://gitcode.com/cann/npu-simulator/issues/60) | +26/-20 (1/1 实质) | 用正则匹配 python3.11 等带版本号的 Python 解释器，修复记录分类（针对性修复 #60 版本化解释器识别缺陷） | 需先修复 CI 失败并重跑流水线通过后再合入 |
| [#58](https://gitcode.com/cann/npu-simulator/pulls/58) | **🤖 阻塞待解** | ❌ 缺 ci-pipeline-passed | [#59](https://gitcode.com/cann/npu-simulator/issues/59) | +23/-27 (1/1 实质) | 修复检测报告写入失败时二次抛错逃逸、阻断后续检测的问题（针对性修复 #59 报告写入异常逃逸） | 需补充 UT 与失败兜底写入，CI 通过后再评审合入 |
| [#57](https://gitcode.com/cann/npu-simulator/pulls/57) | **🤖 值得合入** | ✅ 可合入 | [#27](https://gitcode.com/cann/npu-simulator/issues/27) | +64/-2 (2/2 实质) | 修正 LOAD_2D 查询误将 MStartPosition 当作 K 起始位置（已针对性修复 #27 的 K 起始位置缺陷） | 门禁全绿，建议作者清理重复导入后合入 |
| [#56](https://gitcode.com/cann/npu-simulator/pulls/56) | **🤖 值得合入** | ✅ 可合入 | [#55](https://gitcode.com/cann/npu-simulator/issues/55) | +49/-1 (2/2 实质) | 修复 npu-rep 打包时特殊字符路径下 SQLite URI 解析错误，避免报告 JSON 遗漏（已针对性修复 #55 URI 路径缺陷） | 门禁全绿且经社区独立复现验证，建议直接合入 |
| [#55](https://gitcode.com/cann/npu-simulator/pulls/55) | **🤖 阻塞待解** | ❌ 缺 ci-pipeline-passed | [#58](https://gitcode.com/cann/npu-simulator/issues/58) | +2/-2 (2/2 实质) | 将记录入口的 user_app 保持原始字符串，避免 Path 归一化破坏 shell 命令（针对性修复 #58 引号命令被改写缺陷） | 需排查 UT checkout 凭证故障并重跑 CI，通过后再合入 |
| [#54](https://gitcode.com/cann/npu-simulator/pulls/54) | **🤖 值得合入** | ✅ 可合入 | [#54](https://gitcode.com/cann/npu-simulator/issues/54) | +2/-3 (1/1 实质) | 修正 npusim report 示例输出路径为目录，并说明按核生成 tracing JSON（已针对性修复 #54 报告输出路径示例错误） | CLA 与 CI 均已通过、无冲突，建议直接合入 |
| [#53](https://gitcode.com/cann/npu-simulator/pulls/53) | **🤖 阻塞待解** | ❌ 缺 ci-pipeline-passed | [#53](https://gitcode.com/cann/npu-simulator/issues/53) | +9/-0 (1/1 实质) | 两处区间并集扫描前按 TickStart 预排序，修正带宽统计被低估（已针对性修复 #53 带宽低估缺陷） | 需作者补齐 ci-pipeline-passed 门禁并重跑流水线，全绿后可合入 |
| [#52](https://gitcode.com/cann/npu-simulator/pulls/52) | **🤖 阻塞待解** | ❌ 阻塞标签 stat/needs-squash | — | +360/-114 (13/13 实质) | 新增 --timeout 限制仿真时长，超时后终止进程组并归档（无关联 Issue，属自主增强超时保护能力） | 已 approved，需作者 squash 提交重跑 CI 后再合入 |

### PR #67：fix(prof): preserve base reports when optional processing fails

- **作者**：`@churkinaleksandr` · **停留自然时长**：19.2h · **AI 判定**：**🤖 阻塞待解**
- **代码规模**：11 个文件（实质改动文件 11 个，表面改动文件 0 个，新增测试 +15 行）
- **关联 Issue 对齐**：针对性修复 #63 可选报告阻断导出缺陷
- **核心改动摘要**：可选 Roofline/CriticalPath 失败降级，保留基础报告与 .npu-rep 导出
  - 删除独立 roofline.json 导出，改保留四张 Roofline 表及 CSV，缩小失败面
  - ELF 解码与 Critical Path 失败改为告警降级，单测覆盖上下文恢复与基础报告继续
- **committer 建议动作**：**需作者压缩提交并补 CI 通过后，再安排合入**

### PR #66：fix(ci): correct REPOSITORY_NAME in compile.sh

- **作者**：`@chenge1` · **停留自然时长**：44.5h · **AI 判定**：**🤖 值得合入**
- **代码规模**：1 个文件（实质改动文件 1 个，表面改动文件 0 个，新增测试 +0 行）
- **关联 Issue 对齐**：已针对性修复 #61 仓库名残留缺陷
- **核心改动摘要**：修正compile.sh中仓库名残留，改为npu-simulator
  - 仅改1行环境变量，修正构建日志与断言中的错误仓库标识
  - 维护者称compile.sh有冗余将统一清理，合入前需协调避免重复改动
- **committer 建议动作**：**CLA与CI已通过、无冲突，建议合入并纳入统一清理**

### PR #64：Add Speed-of-light profiling feature

- **作者**：`@fomichevoleg5` · **停留自然时长**：66.9h · **AI 判定**：**🤖 阻塞待解**
- **代码规模**：6 个文件（实质改动文件 6 个，表面改动文件 0 个，新增测试 +0 行）
- **关联 Issue 对齐**：无关联 Issue，新特性未先走方案讨论
- **核心改动摘要**：新增 SOL 分析器与 --sol 选项，评估内核吞吐上限
  - 新增 276 行 SOL 分析器和峰值常量表，需确认 V100 以外架构取值来源
  - report 契约版本放宽到 7 或 8，需评估向后兼容与迁移说明
  - 本次无新增测试文件覆盖，建议补 SpeedOfLightData 生成用例
- **committer 建议动作**：**需作者 squash 提交、补测试并关联 Issue 后再评审**

### PR #63：[WIP] fix(report): Embed operator source files into .npu-rep archives (fix to complete Source/Assembly feature support)

- **作者**：`@churkinaleksandr` · **停留自然时长**：69.1h · **AI 判定**：**🤖 阻塞待解**
- **代码规模**：3 个文件（实质改动文件 3 个，表面改动文件 0 个，新增测试 +0 行）
- **关联 Issue 对齐**：无关联 Issue，属功能补全
- **核心改动摘要**：将算子源文件以 txt 类型嵌入 .npu-rep 归档，补全源码查看功能
  - 新增 .txt=7 文件类型，打包时写入完整源文件，根因修复清晰
  - 同步更新 source_assembly_data_format.md，格式说明一致
  - 无新增测试，缺 ci-pipeline-passed 且含 needs-squash 阻塞
  - PR 仍标 WIP，需作者确认可评审并逐条答复意见
- **committer 建议动作**：**需作者 squash 提交、补充测试并重跑 CI 取得通过标签后再合入**

### PR #60：fix(report): collapse the fixpipe twin rows by identity, not by adjacency

- **作者**：`@gcw_EkTYFH3T` · **停留自然时长**：114.3h · **AI 判定**：**🤖 阻塞待解**
- **代码规模**：1 个文件（实质改动文件 1 个，表面改动文件 0 个，新增测试 +0 行）
- **关联 Issue 对齐**：已针对性修复 #56 孪生行不相邻导致的重复计入
- **核心改动摘要**：将孪生行折叠由相邻匹配改为按 twin_key 字典匹配,修复 UB 写重复计数
  - 孪生行 CoreId 不同且查询按 CoreId 排序,原相邻假设确实不成立,改用 twin_key 字典正确
  - 改动仅 11 增 5 删、单文件,风险可控,但缺少回归测试验证双视图计数不再翻倍
- **committer 建议动作**：**需作者触发 CI 并获 ci-pipeline-passed 标签后,再复核合入**

### PR #59：fix(record): recognize versioned Python executables

- **作者**：`@liangjinxuan-2026` · **停留自然时长**：140.7h · **AI 判定**：**🤖 阻塞待解**
- **代码规模**：1 个文件（实质改动文件 1 个，表面改动文件 0 个，新增测试 +0 行）
- **关联 Issue 对齐**：针对性修复 #60 版本化解释器识别缺陷
- **核心改动摘要**：用正则匹配 python3.11 等带版本号的 Python 解释器，修复记录分类
  - 将 _PYTHON_TOKENS 集合替换为 _PYTHON_COMMAND 正则，覆盖 python3.x/pytest 前缀匹配
  - 需确认 _INTERPRETER_TOKENS 移除 python 后，archive 标签回退到脚本名的逻辑无回归
- **committer 建议动作**：**需先修复 CI 失败并重跑流水线通过后再合入**

### PR #58：fix(report): handle detector output write failures

- **作者**：`@liangjinxuan-2026` · **停留自然时长**：140.7h · **AI 判定**：**🤖 阻塞待解**
- **代码规模**：1 个文件（实质改动文件 1 个，表面改动文件 0 个，新增测试 +0 行）
- **关联 Issue 对齐**：针对性修复 #59 报告写入异常逃逸
- **核心改动摘要**：修复检测报告写入失败时二次抛错逃逸、阻断后续检测的问题
  - 抽出 _write_detection_report 统一捕获 OSError 并以布尔值返回失败，避免异常二次逃逸
  - 缺少回归测试与失败时兜底写 detection failed，且 ci-pipeline 未通过，需作者补齐
- **committer 建议动作**：**需补充 UT 与失败兜底写入，CI 通过后再评审合入**

### PR #57：fix(trace): 正确读取 LOAD_2D 的 K 起始位置 (#27)

- **作者**：`@lilong555` · **停留自然时长**：143.8h · **AI 判定**：**🤖 值得合入**
- **代码规模**：2 个文件（实质改动文件 2 个，表面改动文件 0 个，新增测试 +63 行）
- **关联 Issue 对齐**：已针对性修复 #27 的 K 起始位置缺陷
- **核心改动摘要**：修正 LOAD_2D 查询误将 MStartPosition 当作 K 起始位置
  - SQL 字段改为 DmaMovLoad2dParams.KStartPosition，与消费处 k_start_pos_bytes 对齐
  - 新增 18 项回归覆盖 LOAD_2Dv2/LOAD_MX_2Dv2 及默认、Smart Pipe、Critical Path 报告
  - 外部评审确认回归全通过，仅剩 tests 中 biprof_ctx 重复导入引发 Ruff F811，需顺手清掉
  - DB schema、报告字段名与 CLI 均无变化，向后兼容风险低
- **committer 建议动作**：**门禁全绿，建议作者清理重复导入后合入**

### PR #56：fix(report): 保留 npu-rep 打包数据库路径中的特殊字符 (#55)

- **作者**：`@lilong555` · **停留自然时长**：144.4h · **AI 判定**：**🤖 值得合入**
- **代码规模**：2 个文件（实质改动文件 2 个，表面改动文件 0 个，新增测试 +48 行）
- **关联 Issue 对齐**：已针对性修复 #55 URI 路径缺陷
- **核心改动摘要**：修复 npu-rep 打包时特殊字符路径下 SQLite URI 解析错误，避免报告 JSON 遗漏
  - 改用 db_path.resolve().as_uri() 构造只读 URI，正确保留 #、?、%23 等特殊字符，kernel 元数据不再回退默认值
  - 新增 13 项参数化回归，覆盖相对与绝对路径、特殊字符、空格及中文目录，并校验归档内容完整性
- **committer 建议动作**：**门禁全绿且经社区独立复现验证，建议直接合入**

### PR #55：fix(record): preserve shell command strings before launch

- **作者**：`@liangjinxuan-2026` · **停留自然时长**：144.8h · **AI 判定**：**🤖 阻塞待解**
- **代码规模**：2 个文件（实质改动文件 2 个，表面改动文件 0 个，新增测试 +0 行）
- **关联 Issue 对齐**：针对性修复 #58 引号命令被改写缺陷
- **核心改动摘要**：将记录入口的 user_app 保持原始字符串，避免 Path 归一化破坏 shell 命令
  - 改动仅两处：移除 handle_record_command 与 build_record_config_from_args 中的 Path() 转换
  - build_launch_spec 已支持 str/Path，文件路径解析逻辑不受影响，修复思路正确
  - CI 因 UT 取码认证失败（HTTP Basic Access denied）未通过，需基础设施侧修复后重跑
  - 缺少新增测试覆盖引号命令与 URL 保留场景，建议补充回归用例
- **committer 建议动作**：**需排查 UT checkout 凭证故障并重跑 CI，通过后再合入**

### PR #54：docs: fix the npusim report output example

- **作者**：`@liangjinxuan-2026` · **停留自然时长**：145.9h · **AI 判定**：**🤖 值得合入**
- **代码规模**：1 个文件（实质改动文件 1 个，表面改动文件 0 个，新增测试 +0 行）
- **关联 Issue 对齐**：已针对性修复 #54 报告输出路径示例错误
- **核心改动摘要**：修正 npusim report 示例输出路径为目录，并说明按核生成 tracing JSON
  - 仅改 main.py docstring 示例文字，未变动 CLI 行为，风险极低
  - 示例与 -o 接收目录、按核 trace_coreN.json 的实现一致，文档更准确
- **committer 建议动作**：**CLA 与 CI 均已通过、无冲突，建议直接合入**

### PR #53：fix(report): order the busy-time sweep by interval start

- **作者**：`@gcw_EkTYFH3T` · **停留自然时长**：165h · **AI 判定**：**🤖 阻塞待解**
- **代码规模**：1 个文件（实质改动文件 1 个，表面改动文件 0 个，新增测试 +0 行）
- **关联 Issue 对齐**：已针对性修复 #53 带宽低估缺陷
- **核心改动摘要**：两处区间并集扫描前按 TickStart 预排序，修正带宽统计被低估
  - 在 calc_throughput_stats 与被调内联副本两处扫描前各加一次按起点排序，代价 O(n log n)、可接受
  - 选择在调用方固化有序前提、保留原 ORDER BY TickEnd，避免改动 8 处 SQL，兼容性更好
  - 逻辑正确但未新增单测；建议补充交错区间用例（长传输与短传输重叠）以防回归
  - 仅缺 ci-pipeline-passed 标签，CLA 已通过、无冲突与 squash 问题，补跑 CI 即可
- **committer 建议动作**：**需作者补齐 ci-pipeline-passed 门禁并重跑流水线，全绿后可合入**

### PR #52：feat(record): 支持 --timeout 限制仿真时长并在超时后自动终止

- **作者**：`@Li_cube` · **停留自然时长**：169.4h · **AI 判定**：**🤖 阻塞待解**
- **代码规模**：13 个文件（实质改动文件 13 个，表面改动文件 0 个，新增测试 +3 行）
- **关联 Issue 对齐**：无关联 Issue，属自主增强超时保护能力
- **核心改动摘要**：新增 --timeout 限制仿真时长，超时后终止进程组并归档
  - 超时覆盖经典 record 与 ktest 模式，SIGTERM→5s 宽限→SIGKILL 终止整个进程组，兼容孙进程
  - CLI 显式值优先于 NPUSIM_TIMEOUT，非法单位报错退出码 2，超时按失败退出码 1 并保留 partial 产物
  - 改动 13 文件含文档与测试，但仅 3 行测试新增，建议补充超时终止与时长的用例覆盖
- **committer 建议动作**：**已 approved，需作者 squash 提交重跑 CI 后再合入**

