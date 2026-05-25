---
name: feedback_do_not_overwrite_wati
description: 填表时不要覆盖 C 列（WATI）字段，写入范围必须跳过 C 列
metadata:
  type: feedback
---

填写评论数据时，写入 B:L 范围会包含 C 列（WATI），导致用户手动填入的 WATI 值被清空。

**Why:** 用户会在 C 列手动填写 WATI 数字（如 19194125792），这是独立录入的数据，agent 写入时不应覆盖。第14行的 SwitchBot Lock Pro 填写时就因为用 B14:L14 整段写入，把 C14 的 WATI 值清成了 null。

**How to apply:**
- 写入第一段时，拆成 B 单列 + D:L 两段，跳过 C 列；或确认 C 列有值时先读出再带入写入
- 具体写法：先写 `B{row}` 单格，再写 `D{row}:L{row}`，不要用 `B{row}:L{row}` 连续范围
- 同理，M 列（截图）也已有规则跳过，见 [[feedback_sheet_filler_star_rating]]
