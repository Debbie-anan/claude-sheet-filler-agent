---
name: feedback-sheet-filler-skip-columns
description: sheet-filler 写入时必须跳过 A/C/E/M 四列——既不写入也不清空，留给用户手动管理
metadata:
  node_type: memory
  type: feedback
  originSessionId: 24d0a5a2-d4ec-4f1a-85ff-53a0dbe40b76
---

sheet-filler agent 写入新行时，A 列（状态）、C 列（WATI）、E 列（礼品选择）、M 列（评论截图）必须跳过——**不要写入、也不要写 null 清空**。

**Why:** 这四列都是 Debbie 手动维护的，agent 用 null 占位会清空她已填的数据：
- A 列：人工核对标记（"ok" 等）
- C 列：WATI 数字（如 19194125792）—— 第14行 SwitchBot Lock Pro 因为用 B14:L14 整段写入，把 C14 的 WATI 清成了 null
- E 列：礼品选择 —— Debbie 明确说过"不要填，不要清空，我来填"
- M 列：评论截图（仅当用户本轮发了新截图时写入并覆盖，否则保留原值；详见 [[feedback-sheet-filler-screenshot]]）

**How to apply:** 写入策略不能用一段连续 range（比如 B:L 含 C/E）配合 null 占位。必须拆段写入：
- `B{row}`（产品名）
- `D{row}`（评论状态 = "已上评"）—— **跳过 C**
- `F{row}:L{row}`（F=null 过程备注, G="赖丹", H=null, I=日期, J=站点, K="产品邀评EDM", L=链接）—— **跳过 E**
- M 列：仅当用户本轮发了新截图才写（用 embed-image 覆盖，见 [[feedback-sheet-filler-screenshot]]），否则不动
- `N{row}:Q{row}`（星级、Amazon profile name/link、评论类型）

A 列、C 列、E 列、M 列在写入时**完全不出现在任何 range 里**。

相关：[[feedback-sheet-filler-screenshot]]（M 列特殊规则——发了截图才写，且用 embed-image）、[[feedback_do_not_overwrite_wati]]（C 列踩坑历史的详细记录）
