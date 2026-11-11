# PR & Issue 智能治理 Review 报告 · cann/npu-simulator

| 维度 | 详情 |
|---|---|
| **目标仓库** | [cann/npu-simulator](https://gitcode.com/cann/npu-simulator)（GitCode） |
| **巡检时间** | 2026-11-11 15:38 (UTC+8) |
| **分析引擎** | `gitcode-issue-triage` 确定性守卫 + Pi Agent (`cannbot/deepseek-v4.1-flash`) |
| **判定原则** | 宁漏勿错：强灌水信号 + 无安全否决 → 低价值候选；有任何实质代码/测试/关联 Issue → 保留并给出合路建议 |

---

## 一、执行摘要（供 on-call & committer 速览）

- **Issue 巡检**：共扫描 **39** 条 Issue，判定 KEEP **39** / CLOSE 候选 **0** / 待人工复核 **0**。
- **Open PR 总览（共 15 个）**：
  - ✅ **可立即合入（5 个）**：#38、#36、#35、#33、#23
  - ⚠️ **实质贡献但门禁阻塞（10 个）**：#43、#42、#41、#40、#39、#37、#34、#31、#22、#21
  - 🧹 **低价值/表面改动候选（1 个）**：#33

## 二、Open PR 逐条深度评审与行动清单

| PR | AI 结论 | 合路门禁 | 关联 Issue | 改动规模 (实质文件) | AI 改动摘要与关联对齐 | committer 建议动作 |
|---|---|---|---|---|---|---|
| [#43](https://gitcode.com/cann/npu-simulator/pulls/43) | **🤖 阻塞待解** | ❌ 缺 ci-pipeline-passed | [#34](https://gitcode.com/cann/npu-simulator/issues/34) [#42](https://gitcode.com/cann/npu-simulator/issues/42) | +8/-6 (3/3 实质) | 修正三份文档中报告目录命名，使其与主后端实际格式一致（已针对性修复 #34 目录命名不一致） | 等待 CI 流水通过并补齐 ci-pipeline-passed 后再合入 |
| [#42](https://gitcode.com/cann/npu-simulator/pulls/42) | **🤖 阻塞待解** | ❌ 缺 ci-pipeline-passed；阻塞标签 stat/needs-squash | [#35](https://gitcode.com/cann/npu-simulator/issues/35) | +14/-5 (4/4 实质) | 修正 report -o 默认输出目录的文档与 help 文案并加回归测试（针对修复 #35 默认目录描述错误） | 需作者先 squash 提交并等待 CI 转 passed 后再合入 |
| [#41](https://gitcode.com/cann/npu-simulator/pulls/41) | **🤖 阻塞待解** | ❌ 缺 ci-pipeline-passed；存在代码冲突 | [#32](https://gitcode.com/cann/npu-simulator/issues/32) | +112/-6 (8/8 实质) | ktest 模式新增 -n 生效并对 --chip/-u 打印告警（针对性修复 #32 参数静默忽略问题） | 需作者先解决合并冲突并等 CI 全绿后再复审合入 |
| [#40](https://gitcode.com/cann/npu-simulator/pulls/40) | **🤖 阻塞待解** | ❌ 缺 ci-pipeline-passed | [#33](https://gitcode.com/cann/npu-simulator/issues/33) | +101/-11 (2/2 实质) | 新增 prof_demo 目录名解析分支，修复 kernel 索引恒为 0 导致的产物覆盖（针对性修复 #33 kernel 索引塌缩缺陷） | 等待 ci-pipeline-passed 标签生成后再复核合入，作者已触发 /compile |
| [#39](https://gitcode.com/cann/npu-simulator/pulls/39) | **🤖 阻塞待解** | ❌ 缺 ci-pipeline-passed | [#37](https://gitcode.com/cann/npu-simulator/issues/37) | +5/-4 (2/3 实质) | 统一 -n 默认核描述为 core 0，修正帮助文本与用户指南不一致（已针对 #37 修正文档与 --help 措辞矛盾） | 待 ci-pipeline-passed 通过后复核合入，当前缺 CI 通过标签 |
| [#38](https://gitcode.com/cann/npu-simulator/pulls/38) | **🤖 值得合入** | ✅ 可合入 | [#39](https://gitcode.com/cann/npu-simulator/issues/39) | +1/-1 (1/1 实质) | 修正安装指南 ops 包名芯片代号说明，避免文件名不匹配（已针对性修复 #39 文档包名错误） | CLA与CI均通过且无冲突，建议采纳评审意见后合入 |
| [#37](https://gitcode.com/cann/npu-simulator/pulls/37) | **🤖 阻塞待解** | ❌ 缺 ci-pipeline-passed | [#29](https://gitcode.com/cann/npu-simulator/issues/29) | +48/-26 (3/3 实质) | 移除 record 在用户 cwd 建/搬 log、run_log，避免误删用户数据（针对修复 #29 静默删除用户目录的缺陷） | 需先定位并修复 CI 流水线失败，重跑通过后再合入 |
| [#36](https://gitcode.com/cann/npu-simulator/pulls/36) | **🤖 值得合入** | ✅ 可合入 | [#18](https://gitcode.com/cann/npu-simulator/issues/18) | +70/-0 (2/2 实质) | 修复归档同名产物被低优先级来源覆盖的问题（已针对性修复 #18 归档覆盖缺陷） | CLA 与 CI 均通过且无冲突，建议直接合入 |
| [#35](https://gitcode.com/cann/npu-simulator/pulls/35) | **🤖 值得合入** | ✅ 可合入 | [#31](https://gitcode.com/cann/npu-simulator/issues/31) | +8/-2 (2/2 实质) | 修正 record 文档与注释，说明本地脚本需执行位及 shebang（对齐 #31，仅澄清脚本启动限制，不改实现） | CLA 与 CI 均通过，无冲突，建议直接合入 |
| [#34](https://gitcode.com/cann/npu-simulator/pulls/34) | **🤖 阻塞待解** | ❌ 阻塞标签 stat/needs-squash | [#24](https://gitcode.com/cann/npu-simulator/issues/24) [#25](https://gitcode.com/cann/npu-simulator/issues/25) [#28](https://gitcode.com/cann/npu-simulator/issues/28) [#36](https://gitcode.com/cann/npu-simulator/issues/36) | +1145/-400 (21/21 实质) | 重构CI流水线+ARM smoke，修复空kernel DB报告失败（对应#24/#25/#36/#28四议题） | 需作者squash提交后重跑CI再合入 |
| [#33](https://gitcode.com/cann/npu-simulator/pulls/33) | **🤖 低价值候选** | ✅ 可合入 | — | +2/-2 (0/1 实质) | 重排 UbAccessType 枚举常量顺序，意图修正 Vector 吞吐统计（无关联 Issue，仅为枚举常量顺序调整） | 建议关闭；如需保留，要求显式声明枚举值并补验证 |
| [#31](https://gitcode.com/cann/npu-simulator/pulls/31) | **🤖 阻塞待解** | ❌ 缺 ci-pipeline-passed | [#26](https://gitcode.com/cann/npu-simulator/issues/26) | +7/-2 (1/1 实质) | 为 summary 报告两处除法补零分母保护，避免报告崩溃（针对性修复 #26 除零崩溃缺陷） | 需补 ci-pipeline-passed 门禁并重跑 CI 全绿后再合入 |
| [#23](https://gitcode.com/cann/npu-simulator/pulls/23) | **🤖 值得合入** | ✅ 可合入 | [#18](https://gitcode.com/cann/npu-simulator/issues/18) | +34/-3 (2/2 实质) | 修复多来源同名产物归档时被后来源覆盖的问题（针对性修复 #18 同名产物覆盖缺陷） | CLA 已签、CI 通过且无阻塞，建议直接合入 |
| [#22](https://gitcode.com/cann/npu-simulator/pulls/22) | **🤖 阻塞待解** | ❌ 阻塞标签 stat/needs-squash | [#17](https://gitcode.com/cann/npu-simulator/issues/17) | +5/-5 (1/3 实质) | 修正 README、用户指南、安全声明三处文档的页内锚点链接，使其匹配渲染后的标题 ID（已针对性修复 #17 锚点不匹配缺陷） | 需作者 squash 提交解除 needs-squash 阻塞，再重跑门禁后合入 |
| [#21](https://gitcode.com/cann/npu-simulator/pulls/21) | **🤖 阻塞待解** | ❌ 缺 ci-pipeline-passed；阻塞标签 stat/needs-squash | [#16](https://gitcode.com/cann/npu-simulator/issues/16) | +75/-6 (5/5 实质) | 用独占 mkdir 分配运行目录，避免同秒运行复用归档（针对性修复 #16 目录复用缺陷） | 请作者 squash 提交并补 CI 通过标签后再评审合入 |

### PR #43：docs(report): 修正报告目录命名为主后端实际格式

- **作者**：`@Li_cube` · **停留自然时长**：0.1h · **AI 判定**：**🤖 阻塞待解**
- **代码规模**：3 个文件（实质改动文件 3 个，表面改动文件 0 个，新增测试 +0 行）
- **关联 Issue 对齐**：已针对性修复 #34 目录命名不一致
- **核心改动摘要**：修正三份文档中报告目录命名，使其与主后端实际格式一致
  - 仅涉及文档修改、无测试代码，核对源码 reporters.py 后确认命名说明准确
  - 当前缺少 ci-pipeline-passed 标签，门禁未全绿，需作者重跑 CI
- **committer 建议动作**：**等待 CI 流水通过并补齐 ci-pipeline-passed 后再合入**

### PR #42：docs(report): 修正 -o 未指定时的默认输出目录说明

- **作者**：`@Li_cube` · **停留自然时长**：0.4h · **AI 判定**：**🤖 阻塞待解**
- **代码规模**：4 个文件（实质改动文件 4 个，表面改动文件 0 个，新增测试 +9 行）
- **关联 Issue 对齐**：针对修复 #35 默认目录描述错误
- **核心改动摘要**：修正 report -o 默认输出目录的文档与 help 文案并加回归测试
  - 修正文档、main.py 与 report.py 中 help 文案为 <export>/report，与 report.py 实际默认路径一致
  - 新增 test_main 回归测试断言 help 含 <export>/report 且不再出现 same as export，防止回退
- **committer 建议动作**：**需作者先 squash 提交并等待 CI 转 passed 后再合入**

### PR #41：feat(record): ktest 模式支持 -n 并明确 --chip/-u 不生效

- **作者**：`@zhengronggui` · **停留自然时长**：0.7h · **AI 判定**：**🤖 阻塞待解**
- **代码规模**：8 个文件（实质改动文件 8 个，表面改动文件 0 个，新增测试 +72 行）
- **关联 Issue 对齐**：针对性修复 #32 参数静默忽略问题
- **核心改动摘要**：ktest 模式新增 -n 生效并对 --chip/-u 打印告警
  - 改动实质：新增 KtestConfig.core_id，Stage1 用 parse_core_id 校验，Stage3 注入 CORE_ENABLE_MASK
  - 测试覆盖充分：新增 72 行用例覆盖 core-id 解析、非法值、mask 注入与告警输出
  - 文档与兼容性说明到位：CLI 参数未变动，未指定 -n 时行为与旧版一致
  - 门禁阻塞：缺 ci-pipeline-passed 标签且存在合并冲突，当前不可合入
- **committer 建议动作**：**需作者先解决合并冲突并等 CI 全绿后再复审合入**

### PR #40：fix(report): 识别 prof_demo kernel_<launch>_<name>_reports 命名

- **作者**：`@zhengronggui` · **停留自然时长**：0.7h · **AI 判定**：**🤖 阻塞待解**
- **代码规模**：2 个文件（实质改动文件 2 个，表面改动文件 0 个，新增测试 +70 行）
- **关联 Issue 对齐**：针对性修复 #33 kernel 索引塌缩缺陷
- **核心改动摘要**：新增 prof_demo 目录名解析分支，修复 kernel 索引恒为 0 导致的产物覆盖
  - 新增 ^kernel_(\d+)_.*_reports$ 分支取 launch 号作索引，修复 KERNEL0 塌缩与事件误判重复
  - 不可解析目录名改为打印 warn 并对输出名追加序号，避免静默覆盖；新增 70 行单测覆盖
- **committer 建议动作**：**等待 ci-pipeline-passed 标签生成后再复核合入，作者已触发 /compile**

### PR #39：docs: 统一 -n 默认行为描述为模型默认（core 0）

- **作者**：`@zhengronggui` · **停留自然时长**：0.7h · **AI 判定**：**🤖 阻塞待解**
- **代码规模**：3 个文件（实质改动文件 2 个，表面改动文件 0 个，新增测试 +0 行）
- **关联 Issue 对齐**：已针对 #37 修正文档与 --help 措辞矛盾
- **核心改动摘要**：统一 -n 默认核描述为 core 0，修正帮助文本与用户指南不一致
  - PR 结论（camodel 默认仅 core 0）与 Issue 原文（不注入即全开）相反，需确认实测依据可信
  - 改动仅涉及帮助文本、注释与文档，无行为变化，但 npusim/main.py 属代码文件需回归 test_main.py
- **committer 建议动作**：**待 ci-pipeline-passed 通过后复核合入，当前缺 CI 通过标签**

### PR #38：CANN开发者共建计划-docs: correct chip code in ops package filename

- **作者**：`@weixin_xiaobai` · **停留自然时长**：18.9h · **AI 判定**：**🤖 值得合入**
- **代码规模**：1 个文件（实质改动文件 1 个，表面改动文件 0 个，新增测试 +0 行）
- **关联 Issue 对齐**：已针对性修复 #39 文档包名错误
- **核心改动摘要**：修正安装指南 ops 包名芯片代号说明，避免文件名不匹配
  - 单行文档修正，明确包名用950而非Ascend950，避免安装命令找不到文件
  - 已有官方分发目录实测证据，CLA/CI通过；建议按Li_cube意见精简措辞后合入
- **committer 建议动作**：**CLA与CI均通过且无冲突，建议采纳评审意见后合入**

### PR #37：fix(record): 不再在用户工作目录创建/搬运 log、run_log，避免静默删除用户数据

- **作者**：`@zengzihui` · **停留自然时长**：19.6h · **AI 判定**：**🤖 阻塞待解**
- **代码规模**：3 个文件（实质改动文件 3 个，表面改动文件 0 个，新增测试 +32 行）
- **关联 Issue 对齐**：针对修复 #29 静默删除用户目录的缺陷
- **核心改动摘要**：移除 record 在用户 cwd 建/搬 log、run_log，避免误删用户数据
  - runtime.py 从 CAMODEL_ASSETS 摘除 log/run_log 并删除 RUNTIME_DIRS，消除归档后删除用户同名目录的路径
  - 新增 test_prepare_runtime_dirs_leaves_user_cwd_untouched 回归用例覆盖 #29，建议补充失败路径清理断言
- **committer 建议动作**：**需先定位并修复 CI 流水线失败，重跑通过后再合入**

### PR #36：fix(record): 同名产物按来源优先级归档，低优先级不再覆盖（#18）

- **作者**：`@yampolskiy` · **停留自然时长**：20.4h · **AI 判定**：**🤖 值得合入**
- **代码规模**：2 个文件（实质改动文件 2 个，表面改动文件 0 个，新增测试 +54 行）
- **关联 Issue 对齐**：已针对性修复 #18 归档覆盖缺陷
- **核心改动摘要**：修复归档同名产物被低优先级来源覆盖的问题
  - 三个归档入口改为按目标文件名去重，同名保留高优先级来源，低优先级文件留在原处
  - 新增三个同名冲突用例，复现失败→修复后 FIRST 保留、来源文件正确移动，测试覆盖充分
- **committer 建议动作**：**CLA 与 CI 均通过且无冲突，建议直接合入**

### PR #35：docs(record): 修正本地脚本启动方式的误导性注释，补充脚本执行要求

- **作者**：`@zengzihui` · **停留自然时长**：20.4h · **AI 判定**：**🤖 值得合入**
- **代码规模**：2 个文件（实质改动文件 2 个，表面改动文件 0 个，新增测试 +0 行）
- **关联 Issue 对齐**：对齐 #31，仅澄清脚本启动限制，不改实现
- **核心改动摘要**：修正 record 文档与注释，说明本地脚本需执行位及 shebang
  - docstring 由误导性描述改为与 bash -c 实现一致，仅注释改动无行为变化
  - 用户指南补充 chmod +x 与 shebang 要求及命令模式替代写法
- **committer 建议动作**：**CLA 与 CI 均通过，无冲突，建议直接合入**

### PR #34：ci: 重构Action CI 流水线并支持 ARM smoke，修复空 kernel DB 报告失败

- **作者**：`@ZhouBX` · **停留自然时长**：43.1h · **AI 判定**：**🤖 阻塞待解**
- **代码规模**：21 个文件（实质改动文件 21 个，表面改动文件 0 个，新增测试 +159 行）
- **关联 Issue 对齐**：对应#24/#25/#36/#28四议题
- **核心改动摘要**：重构CI流水线+ARM smoke，修复空kernel DB报告失败
  - reporters.py 跳过无执行指令的空 kernel DB，避免除零，新增测试覆盖
  - ARM smoke 归一化 uname -m 并按 linux-<arch> 精确匹配 CANN 包
  - CI 工作流拆分为 compile/llt/scan/py37_compat，删除旧 codecheck/staticcheck
  - 唯一阻塞为 stat/needs-squash，需压缩提交历史后再触发门禁
- **committer 建议动作**：**需作者squash提交后重跑CI再合入**

### PR #33：Align UbAccessType enum with data contract

- **作者**：`@fomichevoleg5` · **停留自然时长**：44.2h · **AI 判定**：**🤖 低价值候选**
- **代码规模**：1 个文件（实质改动文件 0 个，表面改动文件 0 个，新增测试 +0 行）
- **关联 Issue 对齐**：无关联 Issue，仅为枚举常量顺序调整
- **核心改动摘要**：重排 UbAccessType 枚举常量顺序，意图修正 Vector 吞吐统计
  - 仅调换枚举顺序，auto() 隐式取值随之变化，需确认无持久化或 DB 依赖
  - 无新增测试、无关联 Issue，SIMD 吞吐修复缺少可复核证据
- **committer 建议动作**：**建议关闭；如需保留，要求显式声明枚举值并补验证**
- **治理可执行命令（先 dry-run）**：
  ```bash
  python3 skills/gitcode-issue-triage/scripts/gitcode_issue.py \
    --owner cann --repo npu-simulator \
    --bot-logins cann-robot \
    process-pr --number 33 --dry-run
  ```

### PR #31：fix(report): guard the summary metrics against zero denominators

- **作者**：`@gcw_EkTYFH3T` · **停留自然时长**：121.8h · **AI 判定**：**🤖 阻塞待解**
- **代码规模**：1 个文件（实质改动文件 1 个，表面改动文件 0 个，新增测试 +0 行）
- **关联 Issue 对齐**：针对性修复 #26 除零崩溃缺陷
- **核心改动摘要**：为 summary 报告两处除法补零分母保护，避免报告崩溃
  - get_imbalance_ratio 过滤零跨度核并空列表返回 0.0，规避 ZeroDivisionError
  - 建议同步为标量指令占比补零分母保护，并补一条零跨度单测
- **committer 建议动作**：**需补 ci-pipeline-passed 门禁并重跑 CI 全绿后再合入**

### PR #23：fix: preserve first-root artifact when names collide

- **作者**：`@gxhgxh2475698` · **停留自然时长**：365.4h · **AI 判定**：**🤖 值得合入**
- **代码规模**：2 个文件（实质改动文件 2 个，表面改动文件 0 个，新增测试 +25 行）
- **关联 Issue 对齐**：针对性修复 #18 同名产物覆盖缺陷
- **核心改动摘要**：修复多来源同名产物归档时被后来源覆盖的问题
  - 通配符归档加入 seen_names 去重，三个归档入口统一按首个来源优先，逻辑一致
  - 新增覆盖三条归档路径的回归用例，验证首来源保留且目标缺失时清理行为不变
- **committer 建议动作**：**CLA 已签、CI 通过且无阻塞，建议直接合入**

### PR #22：docs: match in-page links to rendered heading IDs

- **作者**：`@gxhgxh2475698` · **停留自然时长**：365.5h · **AI 判定**：**🤖 阻塞待解**
- **代码规模**：3 个文件（实质改动文件 1 个，表面改动文件 0 个，新增测试 +0 行）
- **关联 Issue 对齐**：已针对性修复 #17 锚点不匹配缺陷
- **核心改动摘要**：修正 README、用户指南、安全声明三处文档的页内锚点链接，使其匹配渲染后的标题 ID
  - 锚点统一改为渲染后的小写、去标点 ID，与 GitCode 实际标题 id 一致
  - 纯文档改动无代码风险，CLA 与 CI 已通过且有人工 /approve
  - 唯一门禁阻塞为 stat/needs-squash，需压缩为单一提交后再合入
- **committer 建议动作**：**需作者 squash 提交解除 needs-squash 阻塞，再重跑门禁后合入**

### PR #21：fix: reserve separate output directories for same-second runs

- **作者**：`@gxhgxh2475698` · **停留自然时长**：365.7h · **AI 判定**：**🤖 阻塞待解**
- **代码规模**：5 个文件（实质改动文件 5 个，表面改动文件 0 个，新增测试 +46 行）
- **关联 Issue 对齐**：针对性修复 #16 目录复用缺陷
- **核心改动摘要**：用独占 mkdir 分配运行目录，避免同秒运行复用归档
  - 新增 create_unique_target_dir 以独占 mkdir 加 _N 后缀，record 与 ktest 两模式共用，逻辑正确
  - 附带修复 runtime.py 备份清理的 Py3.7 兼容问题，但 os.rename 改 copy2 需确认语义无回退
  - 两模式各新增同秒回归测试，覆盖仍开放 #16 的复现场景，建议补并发竞争用例
- **committer 建议动作**：**请作者 squash 提交并补 CI 通过标签后再评审合入**

