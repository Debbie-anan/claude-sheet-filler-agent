# Sheet-filler Agent Memory

- [填表时不要覆盖 WATI 列（C 列）](feedback_do_not_overwrite_wati.md) — 写入范围必须跳过 C 列，分拆避免清空用户手动填的 WATI 值
- [Sheet-filler 星级填写规则](feedback_sheet_filler_star_rating.md) — 填星级优先读截图文字（"X stelle su 5"等），不要靠数图标；Amazon 反爬无法在线验证，截图是唯一真相源
- [Sheet-filler 截图填 M 列规则](feedback_sheet_filler_screenshot.md) — 用户在聊天窗口发的评论截图必须填到 M 列，无条件覆盖；写入用 embed-image 不能用 url 超链接
- [Sheet-filler 跳过列规则](feedback_sheet_filler_skip_columns.md) — A/C/E/M 四列必须跳过，既不写入也不清空（null 占位会清空 C 列 WATI 和 E 列礼品选择）
