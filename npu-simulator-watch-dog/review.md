# PR & Issue 智能治理 Review 报告 · cann/npu-simulator

| 维度 | 详情 |
|---|---|
| **目标仓库** | [cann/npu-simulator](https://gitcode.com/cann/npu-simulator)（GitCode） |
| **巡检时间** | 2026-11-09 22:37 (UTC+8) |
| **分析引擎** | `gitcode-issue-triage` 确定性守卫 + Pi Agent (`cannbot/deepseek-v4.1-flash`) |
| **判定原则** | 宁漏勿错：强灌水信号 + 无安全否决 → 低价值候选；有任何实质代码/测试/关联 Issue → 保留并给出合路建议 |

---

## 一、执行摘要（供 on-call & committer 速览）

- **Issue 巡检**：共扫描 **26** 条 Issue，判定 KEEP **26** / CLOSE 候选 **0** / 待人工复核 **0**。
- **Open PR 总览（共 7 个）**：
  - ✅ **可立即合入（2 个）**：#33、#23
  - ⚠️ **实质贡献但门禁阻塞（5 个）**：#34、#32、#31、#22、#21
  - 🧹 **低价值/表面改动候选（1 个）**：#33

## 二、Open PR 逐条深度评审与行动清单

| PR | AI 结论 | 合路门禁 | 关联 Issue | 改动规模 (实质文件) | AI 改动摘要与关联对齐 | committer 建议动作 |
|---|---|---|---|---|---|---|
| [#34](https://gitcode.com/cann/npu-simulator/pulls/34) | **🤖 阻塞待解** | ❌ 阻塞标签 stat/needs-squash | [#24](https://gitcode.com/cann/npu-simulator/issues/24) [#25](https://gitcode.com/cann/npu-simulator/issues/25) | +1005/-369 (16/16 实质) | 重构 CI 流水线并支持 ARM smoke，空 kernel DB 时跳过报告避免除零失败（针对性修复 #24 空 DB 报告失败，并落地 #25 ARM 适配） | 需作者 squash 提交历史后重跑门禁，全绿再合入 |
| [#33](https://gitcode.com/cann/npu-simulator/pulls/33) | **🤖 低价值候选** | ✅ 可合入 | — | +2/-2 (0/1 实质) | 重排 UbAccessType 枚举顺序以匹配数据契约，修正吞吐统计（无关联 Issue，属独立缺陷修复） | 纯枚举重排无实质改动，可在说明风险后低优先级关闭 |
| [#32](https://gitcode.com/cann/npu-simulator/pulls/32) | **🤖 阻塞待解** | ❌ 缺 ci-pipeline-passed；存在代码冲突 | — | +81/-22 (6/6 实质) | 用 --sim_mode {ca,pv} 替换 --pv，支持两种仿真模式（无关联 Issue，属自驱 CLI 接口改进） | 需作者解决合并冲突，并补跑 CI 以取得 ci-pipeline-passed 标签后再合入 |
| [#31](https://gitcode.com/cann/npu-simulator/pulls/31) | **🤖 阻塞待解** | ❌ 缺 ci-pipeline-passed | [#26](https://gitcode.com/cann/npu-simulator/issues/26) | +7/-2 (1/1 实质) | 为 summary 报告两处除法补零分母保护，避免报告崩溃（针对性修复 #26 除零崩溃缺陷） | 需补 ci-pipeline-passed 门禁并重跑 CI 全绿后再合入 |
| [#23](https://gitcode.com/cann/npu-simulator/pulls/23) | **🤖 值得合入** | ✅ 可合入 | [#18](https://gitcode.com/cann/npu-simulator/issues/18) | +34/-3 (2/2 实质) | 修复多来源同名产物归档时被后来源覆盖的问题（针对性修复 #18 同名产物覆盖缺陷） | CLA 已签、CI 通过且无阻塞，建议直接合入 |
| [#22](https://gitcode.com/cann/npu-simulator/pulls/22) | **🤖 阻塞待解** | ❌ 阻塞标签 stat/needs-squash | [#17](https://gitcode.com/cann/npu-simulator/issues/17) | +5/-5 (1/3 实质) | 修正 README、用户指南、安全声明三处文档的页内锚点链接，使其匹配渲染后的标题 ID（已针对性修复 #17 锚点不匹配缺陷） | 需作者 squash 提交解除 needs-squash 阻塞，再重跑门禁后合入 |
| [#21](https://gitcode.com/cann/npu-simulator/pulls/21) | **🤖 阻塞待解** | ❌ 缺 ci-pipeline-passed；阻塞标签 stat/needs-squash | [#16](https://gitcode.com/cann/npu-simulator/issues/16) | +75/-6 (5/5 实质) | 用独占 mkdir 分配运行目录，避免同秒运行复用归档（针对性修复 #16 目录复用缺陷） | 请作者 squash 提交并补 CI 通过标签后再评审合入 |

### PR #34：ci: 重构Action CI 流水线并支持 ARM smoke，修复空 kernel DB 报告失败

- **作者**：`@ZhouBX` · **停留自然时长**：2.1h · **AI 判定**：**🤖 阻塞待解**
- **代码规模**：16 个文件（实质改动文件 16 个，表面改动文件 0 个，新增测试 +53 行）
- **关联 Issue 对齐**：针对性修复 #24 空 DB 报告失败，并落地 #25 ARM 适配
- **核心改动摘要**：重构 CI 流水线并支持 ARM smoke，空 kernel DB 时跳过报告避免除零失败
  - reporters.py 在分析前检查 ExecutedInstructions 表为空则跳过，新增 2 个测试覆盖
  - 新增 compile/llt/scan/py37 工作流与脚本，pre_smoke 归一化架构并校验 en_dtypes 编译依赖
  - 仍存在 stat/needs-squash 阻塞，需压缩提交后重新触发 CI 验证
- **committer 建议动作**：**需作者 squash 提交历史后重跑门禁，全绿再合入**

### PR #33：Align UbAccessType enum with data contract

- **作者**：`@fomichevoleg5` · **停留自然时长**：3.2h · **AI 判定**：**🤖 低价值候选**
- **代码规模**：1 个文件（实质改动文件 0 个，表面改动文件 0 个，新增测试 +0 行）
- **关联 Issue 对齐**：无关联 Issue，属独立缺陷修复
- **核心改动摘要**：重排 UbAccessType 枚举顺序以匹配数据契约，修正吞吐统计
  - 仅调整 SIMD/SIMT 读写常量定义顺序，未改变取值语义与逻辑
  - 需确认依赖枚举序号的调用方及 DB 契约，避免隐式兼容性破坏
- **committer 建议动作**：**纯枚举重排无实质改动，可在说明风险后低优先级关闭**
- **治理可执行命令（先 dry-run）**：
  ```bash
  python3 skills/gitcode-issue-triage/scripts/gitcode_issue.py \
    --owner cann --repo npu-simulator \
    --bot-logins cann-robot \
    process-pr --number 33 --dry-run
  ```

### PR #32：feat: --pv 替换为 --sim_mode，支持 ca/pv 两种仿真模式

- **作者**：`@zhiweiyuan` · **停留自然时长**：5.1h · **AI 判定**：**🤖 阻塞待解**
- **代码规模**：6 个文件（实质改动文件 6 个，表面改动文件 0 个，新增测试 +48 行）
- **关联 Issue 对齐**：无关联 Issue，属自驱 CLI 接口改进
- **核心改动摘要**：用 --sim_mode {ca,pv} 替换 --pv，支持两种仿真模式
  - 接口语义由布尔开关升级为枚举模式，默认 ca 保持兼容，大小写不敏感，非法值由 argparse 拒绝
  - 新增 normalize_sim_mode 归一化为 CA/PV，注入 CAMODEL_SIM_TYPE，下游无需改动；两条 record 路径均覆盖
  - 单测覆盖默认值、大写、非法值、ktest 路径，共 48 行测试；文档同步更新
  - 存在合并冲突且缺 ci-pipeline-passed，暂不满足合入门禁
- **committer 建议动作**：**需作者解决合并冲突，并补跑 CI 以取得 ci-pipeline-passed 标签后再合入**

### PR #31：fix(report): guard the summary metrics against zero denominators

- **作者**：`@gcw_EkTYFH3T` · **停留自然时长**：80.8h · **AI 判定**：**🤖 阻塞待解**
- **代码规模**：1 个文件（实质改动文件 1 个，表面改动文件 0 个，新增测试 +0 行）
- **关联 Issue 对齐**：针对性修复 #26 除零崩溃缺陷
- **核心改动摘要**：为 summary 报告两处除法补零分母保护，避免报告崩溃
  - get_imbalance_ratio 过滤零跨度核并空列表返回 0.0，规避 ZeroDivisionError
  - 建议同步为标量指令占比补零分母保护，并补一条零跨度单测
- **committer 建议动作**：**需补 ci-pipeline-passed 门禁并重跑 CI 全绿后再合入**

### PR #23：fix: preserve first-root artifact when names collide

- **作者**：`@gxhgxh2475698` · **停留自然时长**：324.3h · **AI 判定**：**🤖 值得合入**
- **代码规模**：2 个文件（实质改动文件 2 个，表面改动文件 0 个，新增测试 +25 行）
- **关联 Issue 对齐**：针对性修复 #18 同名产物覆盖缺陷
- **核心改动摘要**：修复多来源同名产物归档时被后来源覆盖的问题
  - 通配符归档加入 seen_names 去重，三个归档入口统一按首个来源优先，逻辑一致
  - 新增覆盖三条归档路径的回归用例，验证首来源保留且目标缺失时清理行为不变
- **committer 建议动作**：**CLA 已签、CI 通过且无阻塞，建议直接合入**

### PR #22：docs: match in-page links to rendered heading IDs

- **作者**：`@gxhgxh2475698` · **停留自然时长**：324.5h · **AI 判定**：**🤖 阻塞待解**
- **代码规模**：3 个文件（实质改动文件 1 个，表面改动文件 0 个，新增测试 +0 行）
- **关联 Issue 对齐**：已针对性修复 #17 锚点不匹配缺陷
- **核心改动摘要**：修正 README、用户指南、安全声明三处文档的页内锚点链接，使其匹配渲染后的标题 ID
  - 锚点统一改为渲染后的小写、去标点 ID，与 GitCode 实际标题 id 一致
  - 纯文档改动无代码风险，CLA 与 CI 已通过且有人工 /approve
  - 唯一门禁阻塞为 stat/needs-squash，需压缩为单一提交后再合入
- **committer 建议动作**：**需作者 squash 提交解除 needs-squash 阻塞，再重跑门禁后合入**

### PR #21：fix: reserve separate output directories for same-second runs

- **作者**：`@gxhgxh2475698` · **停留自然时长**：324.7h · **AI 判定**：**🤖 阻塞待解**
- **代码规模**：5 个文件（实质改动文件 5 个，表面改动文件 0 个，新增测试 +46 行）
- **关联 Issue 对齐**：针对性修复 #16 目录复用缺陷
- **核心改动摘要**：用独占 mkdir 分配运行目录，避免同秒运行复用归档
  - 新增 create_unique_target_dir 以独占 mkdir 加 _N 后缀，record 与 ktest 两模式共用，逻辑正确
  - 附带修复 runtime.py 备份清理的 Py3.7 兼容问题，但 os.rename 改 copy2 需确认语义无回退
  - 两模式各新增同秒回归测试，覆盖仍开放 #16 的复现场景，建议补并发竞争用例
- **committer 建议动作**：**请作者 squash 提交并补 CI 通过标签后再评审合入**

