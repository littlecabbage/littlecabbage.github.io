# cann/npu-simulator 看板

更新：2026-10-27T12:03:44Z　·　数据源：GitCode CLI（全指标自算，自然时间口径）

## 1. 总览指标

**不合规 8 项 / 合规 0 项 / 仅展示 6 项**

### ❌ 不合规

| 指标 | 当前值 | 阈值 | 原因 |
| --- | --- | --- | --- |
| 无关联 PR 的开启 Issue | 2 | = 0 | 当前 2 个 —— 这些开启 issue 没有任何 PR 承接，需要回复或建 PR |
| 无 Issue 关联的开启 PR | 1 | = 0 | 当前 1 个 —— 这些 PR 没有关联 issue，无法回溯需求来源 |
| Issue 闭环率 | 56% | 蓝 ≥90%，橙 50%~90%，红 <50% | 56% 未达 90% 蓝线，落在橙区 |
| 开启且未响应数 | 7 | = 0 | 当前 7 个 —— 仍有开启 issue 未收到任何非创建者（非机器人）回复 |
| 开启未响应超时数 | 2 | = 0 | 当前 2 个 —— 未响应且停留 >24h |
| 首次响应未达标数 | 12 | = 0 | 当前 12 个 —— 首次响应 >24h 或未响应且停留 >24h |
| 首次响应达标率 | 33% | 蓝 ≥80%，橙 50%~80%，红 <50% | 33% 未达 80% 蓝线，落在红区 |
| 平均首次响应(H) | 60.2 | ≤ 24h | 60.2h 超过 24h 达标线 |

### ➖ 仅展示（无平台阈值）

| 指标 | 当前值 |
| --- | --- |
| 开启 Issue | 8 |
| 开启 PR | 7 |
| 有关联 Issue 的开启 PR | 6 |
| Issue 总数 | 18 |
| 开启总数 | 8 |
| 平均闭环时长(D) | 11.5 |

## 2. 应该回复的 Issue（2，无关联 PR）

- **#9 [建议] npu-simulator 文档补充性能调优章节**  ·  [打开](https://gitcode.com/cann/npu-simulator/issues/9)
  open · 无关联 PR · 停留 5.7 天 · 0 评论 · @2601_96050445
  创建 2026-10-22 · labels: 无
- **#12 "[Bug-Report|缺陷反馈] 仿真器跨核同步 flag 内部状态池在大规模高频 set/wait 场景下溢出——flagId 合法（10/11 < 16）仍报 "flag ID overflows"，导致仿真崩溃或同步语义损坏**  ·  [打开](https://gitcode.com/cann/npu-simulator/issues/12)
  open · 无关联 PR · 停留 5.2 天 · 1 评论 · @chenjiayi_
  创建 2026-10-22 · labels: 无

## 3. 应该关注的 PR（6，有 Issue 关联）

- **#23 fix: preserve first-root artifact when names collide**  ·  [打开](https://gitcode.com/cann/npu-simulator/merge_requests/23)
  open · 关联 Issue #18 · 停留 0.4 天 · 0 评论 · @gxhgxh2475698
  fix/preserve-first-asset-root-20261027 → master · 可合并 ✅
- **#22 docs: match in-page links to rendered heading IDs**  ·  [打开](https://gitcode.com/cann/npu-simulator/merge_requests/22)
  open · 关联 Issue #17 · 停留 0.4 天 · 0 评论 · @gxhgxh2475698
  docs/fix-rendered-anchors-20261027 → master · 不可合并 ❌（缺少 ci-pipeline-passed）
- **#21 fix: reserve separate output directories for same-second runs**  ·  [打开](https://gitcode.com/cann/npu-simulator/merge_requests/21)
  open · 关联 Issue #16 · 停留 0.4 天 · 0 评论 · @gxhgxh2475698
  fix/unique-record-output-20261027 → master · 不可合并 ❌（缺少 ci-pipeline-passed）
- **#20 docs: quote multiword record command examples**  ·  [打开](https://gitcode.com/cann/npu-simulator/merge_requests/20)
  open · 关联 Issue #15 · 停留 0.4 天 · 0 评论 · @gxhgxh2475698
  docs/quote-user-app-20261027 → master · 可合并 ✅
- **#19 fix: preserve Python 3.7 HCCL backup cleanup**  ·  [打开](https://gitcode.com/cann/npu-simulator/merge_requests/19)
  open · 关联 Issue #14 · 停留 0.4 天 · 0 评论 · @gxhgxh2475698
  fix/python37-hccl-restore-unlink-20261027 → master · 可合并 ✅
- **#9 fix(report): 只读 DB URI 统一 resolve+编码，修复 '#' 路径读错文件与相对路径 ValueError**  ·  [打开](https://gitcode.com/cann/npu-simulator/merge_requests/9)
  open · 关联 Issue #5 · 停留 25.1 天 · 0 评论 · @lizhe_li
  fix/readonly-db-uri-resolve-encode → master · 可合并 ✅

## 4. 无 Issue 关联的 PR（1）

- **#11 docs: 修复中文标点前多余空格（1 处）**  ·  [打开](https://gitcode.com/cann/npu-simulator/merge_requests/11)
  open · 无关联 Issue · 停留 10.7 天 · 0 评论 · @gcw_2C7pfVg4
  docs/fix-punct-space → master · 不可合并 ❌（缺少 cann-cla/yes）

---

口径：见 docs/metrics.md（自然时间，不剔除周末/节假日）。
