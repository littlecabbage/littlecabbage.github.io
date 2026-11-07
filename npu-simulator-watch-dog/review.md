# PR & Issue 智能治理 Review 报告 · cann/npu-simulator

| 维度 | 详情 |
|---|---|
| **目标仓库** | [cann/npu-simulator](https://gitcode.com/cann/npu-simulator)（GitCode） |
| **巡检时间** | 2026-11-08 02:37 (UTC+8) |
| **分析引擎** | `gitcode-issue-triage` 确定性守卫 + Pi Agent (`cannbot/deepseek-v4.1-flash`) |
| **判定原则** | 宁漏勿错：强灌水信号 + 无安全否决 → 低价值候选；有任何实质代码/测试/关联 Issue → 保留并给出合路建议 |

---

## 一、执行摘要（供 on-call & committer 速览）

- **Issue 巡检**：共扫描 **26** 条 Issue，判定 KEEP **26** / CLOSE 候选 **0** / 待人工复核 **0**。
- **Open PR 总览（共 7 个）**：
  - ✅ **可立即合入（3 个）**：#26、#23、#20
  - ⚠️ **实质贡献但门禁阻塞（3 个）**：#31、#22、#21
  - 🧹 **低价值/表面改动候选（1 个）**：#11

## 二、Open PR 逐条深度评审与行动清单

| PR | AI 结论 | 合路门禁 | 关联 Issue | 改动规模 (实质文件) | AI 改动摘要与关联对齐 | committer 建议动作 |
|---|---|---|---|---|---|---|
| [#31](https://gitcode.com/cann/npu-simulator/pulls/31) | **🤖 阻塞待解** | ❌ 缺 ci-pipeline-passed | [#26](https://gitcode.com/cann/npu-simulator/issues/26) | +7/-2 (1/1 实质) | 为 summary 报告两处除法补零分母保护，避免报告崩溃（针对性修复 #26 除零崩溃缺陷） | 需补 ci-pipeline-passed 门禁并重跑 CI 全绿后再合入 |
| [#26](https://gitcode.com/cann/npu-simulator/pulls/26) | **🤖 值得合入** | ✅ 可合入 (已 approved) | [#19](https://gitcode.com/cann/npu-simulator/issues/19) | +136/-31 (4/4 实质) | 保留 trace 分片序号，修复 report 后处理覆盖分片导致事件丢失（针对性修复 #19 分片覆盖与合并漏读缺陷） | 已获 approved 且门禁全绿，建议直接合入 |
| [#23](https://gitcode.com/cann/npu-simulator/pulls/23) | **🤖 值得合入** | ✅ 可合入 | [#18](https://gitcode.com/cann/npu-simulator/issues/18) | +34/-3 (2/2 实质) | 修复多来源目录同名产物归档时后来源覆盖首选来源的问题（已针对性修复 #18 三处归档覆盖缺陷） | 门禁全绿且关联 Issue 已闭环，建议直接合入 |
| [#22](https://gitcode.com/cann/npu-simulator/pulls/22) | **🤖 阻塞待解** | ❌ 缺 ci-pipeline-passed；阻塞标签 stat/needs-squash | [#17](https://gitcode.com/cann/npu-simulator/issues/17) | +5/-5 (1/3 实质) | 修正README、用户指南与安全声明共四处页内锚点链接（针对性修复 #17 锚点不匹配） | 需作者squash提交并重跑CI，门禁全绿后再合入 |
| [#21](https://gitcode.com/cann/npu-simulator/pulls/21) | **🤖 阻塞待解** | ❌ 缺 ci-pipeline-passed；阻塞标签 stat/needs-squash | [#16](https://gitcode.com/cann/npu-simulator/issues/16) | +75/-6 (5/5 实质) | 用独占 mkdir 分配 _N 后缀目录，避免同秒运行复用输出目录（已针对性修复 #16 同秒目录复用缺陷） | 需作者 squash 提交并补 ci-pipeline-passed 后再合入 |
| [#20](https://gitcode.com/cann/npu-simulator/pulls/20) | **🤖 值得合入** | ✅ 可合入 (已 approved) | [#15](https://gitcode.com/cann/npu-simulator/issues/15) | +3/-2 (2/2 实质) | 为 record 帮助与中文指南中的多词命令示例补上引号（已针对性修复 #15 命令示例缺引号问题） | 已获 approved 且门禁全绿无阻塞，建议直接合入 |
| [#11](https://gitcode.com/cann/npu-simulator/pulls/11) | **🤖 低价值候选** | ❌ CLA 未签 (cann-cla/no)；缺 cann-cla/yes | — | +1/-1 (0/1 实质) | 仅删除文档中1处中文标点前多余空格（无关联 Issue，纯排版修正） | 建议直接关闭；如保留需作者补签 CLA 并重跑门禁 |

### PR #31：fix(report): guard the summary metrics against zero denominators

- **作者**：`@gcw_EkTYFH3T` · **停留自然时长**：36.8h · **AI 判定**：**🤖 阻塞待解**
- **代码规模**：1 个文件（实质改动文件 1 个，表面改动文件 0 个，新增测试 +0 行）
- **关联 Issue 对齐**：针对性修复 #26 除零崩溃缺陷
- **核心改动摘要**：为 summary 报告两处除法补零分母保护，避免报告崩溃
  - get_imbalance_ratio 过滤零跨度核并空列表返回 0.0，规避 ZeroDivisionError
  - 建议同步为标量指令占比补零分母保护，并补一条零跨度单测
- **committer 建议动作**：**需补 ci-pipeline-passed 门禁并重跑 CI 全绿后再合入**

### PR #26：fix(report): 保留 trace 分片序号，修复 --json-max-size 分片被覆盖丢失

- **作者**：`@lizhe_li` · **停留自然时长**：219h · **AI 判定**：**🤖 值得合入**
- **代码规模**：4 个文件（实质改动文件 4 个，表面改动文件 0 个，新增测试 +67 行）
- **关联 Issue 对齐**：针对性修复 #19 分片覆盖与合并漏读缺陷
- **核心改动摘要**：保留 trace 分片序号，修复 report 后处理覆盖分片导致事件丢失
  - _TRACE_REPORT_RE 捕获分片序号，重命名不再覆盖同名文件
  - TRACE_FILE_RE 支持带序号分片，merge-trace 可读全部分片
  - 新增两个回归测试覆盖分片保留与合并读取场景
- **committer 建议动作**：**已获 approved 且门禁全绿，建议直接合入**

### PR #23：fix: preserve first-root artifact when names collide

- **作者**：`@gxhgxh2475698` · **停留自然时长**：280.3h · **AI 判定**：**🤖 值得合入**
- **代码规模**：2 个文件（实质改动文件 2 个，表面改动文件 0 个，新增测试 +25 行）
- **关联 Issue 对齐**：已针对性修复 #18 三处归档覆盖缺陷
- **核心改动摘要**：修复多来源目录同名产物归档时后来源覆盖首选来源的问题
  - 三个归档入口新增按文件名去重，仅保留首个来源，符合优先级语义
  - 新增三路径回归用例覆盖 FIRST/SECOND 场景，含目标不可用清理分支验证
- **committer 建议动作**：**门禁全绿且关联 Issue 已闭环，建议直接合入**

### PR #22：docs: match in-page links to rendered heading IDs

- **作者**：`@gxhgxh2475698` · **停留自然时长**：280.5h · **AI 判定**：**🤖 阻塞待解**
- **代码规模**：3 个文件（实质改动文件 1 个，表面改动文件 0 个，新增测试 +0 行）
- **关联 Issue 对齐**：针对性修复 #17 锚点不匹配
- **核心改动摘要**：修正README、用户指南与安全声明共四处页内锚点链接
  - diff 仅调整 Markdown 链接片段，无代码改动，风险极低
  - 缺 ci-pipeline-passed，且带 needs-squash，CI 多次未通过
- **committer 建议动作**：**需作者squash提交并重跑CI，门禁全绿后再合入**

### PR #21：fix: reserve separate output directories for same-second runs

- **作者**：`@gxhgxh2475698` · **停留自然时长**：280.7h · **AI 判定**：**🤖 阻塞待解**
- **代码规模**：5 个文件（实质改动文件 5 个，表面改动文件 0 个，新增测试 +46 行）
- **关联 Issue 对齐**：已针对性修复 #16 同秒目录复用缺陷
- **核心改动摘要**：用独占 mkdir 分配 _N 后缀目录，避免同秒运行复用输出目录
  - create_unique_target_dir 以独占 mkdir 抢锁并递增后缀，消除存在即复用竞态，ktest 与 record 共用同一实现
  - runtime.py 改用 copy2+unlink 兼容 Python 3.7，保留缺失容忍但不再吞掉其他异常，方向正确
  - 两种模式各补一个同秒回归测试（46 行），但需确认重试边界与 _N 目录命名上限是否被测试覆盖
  - 门禁仍缺 ci-pipeline-passed 且带 needs-squash，需压缩为单提交并重跑全量兼容性检查
- **committer 建议动作**：**需作者 squash 提交并补 ci-pipeline-passed 后再合入**

### PR #20：docs: quote multiword record command examples

- **作者**：`@gxhgxh2475698` · **停留自然时长**：280.9h · **AI 判定**：**🤖 值得合入**
- **代码规模**：2 个文件（实质改动文件 2 个，表面改动文件 0 个，新增测试 +0 行）
- **关联 Issue 对齐**：已针对性修复 #15 命令示例缺引号问题
- **核心改动摘要**：为 record 帮助与中文指南中的多词命令示例补上引号
  - main.py 中 user_app 帮助改为带引号示例，并说明含空格命令需整体作为一个参数传入
  - 同步修正 01_user_guide.md 参数表，作者已用 argparse 复现验证；仅改文档与提示、风险低
- **committer 建议动作**：**已获 approved 且门禁全绿无阻塞，建议直接合入**

### PR #11：docs: 修复中文标点前多余空格（1 处）

- **作者**：`@gcw_2C7pfVg4` · **停留自然时长**：528h · **AI 判定**：**🤖 低价值候选**
- **代码规模**：1 个文件（实质改动文件 0 个，表面改动文件 0 个，新增测试 +0 行）
- **关联 Issue 对齐**：无关联 Issue，纯排版修正
- **核心改动摘要**：仅删除文档中1处中文标点前多余空格
  - diff 仅 1 行空格调整，属表面改动，无实质代码或逻辑变更
  - cann-cla/no 未签署且无关联 Issue、无测试，合入收益极低
- **committer 建议动作**：**建议直接关闭；如保留需作者补签 CLA 并重跑门禁**
- **治理可执行命令（先 dry-run）**：
  ```bash
  python3 skills/gitcode-issue-triage/scripts/gitcode_issue.py \
    --owner cann --repo npu-simulator \
    --bot-logins cann-robot \
    process-pr --number 11 --dry-run
  ```

