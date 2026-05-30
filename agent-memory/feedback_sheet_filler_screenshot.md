---
name: feedback-sheet-filler-screenshot
description: sheet-filler 填表时，用户在聊天窗口发的评论截图就是要填进 L 列的截图，应直接覆盖 L 列已有内容
metadata: 
  node_type: memory
  type: feedback
  originSessionId: 24d0a5a2-d4ec-4f1a-85ff-53a0dbe40b76
---

当 Debbie 在聊天窗口发评论截图并要求填某一行时，那张窗口里的截图**就是**要填到 L 列（评论截图列）的东西，agent 必须把它填进 L 列，即使 L 列已经有内容也要覆盖。

**Why:** Debbie 之前的流程是把截图直接放在 L 列里，但 CC 反馈"从 L 列读取截图麻烦"，所以她改成把截图发到聊天窗口。这意味着窗口截图取代了 L 列截图作为输入源——如果 agent 跳过 L 列，那这次发的截图就丢了。L 列原有的内容（无论是飞书链接还是占位符）都应该被这次窗口截图覆盖。

**How to apply:** sheet-filler agent 在写入某一行时，如果用户在本轮对话窗口里附了评论截图，必须把该截图写入 L 列，无条件覆盖 L 列原有内容。不要因为"L 列非空"就跳过——这正是用户期望被覆盖的情况。只有在用户**没有**发截图的情况下，才保留 L 列原值。

**写入方式必须是 embed-image（嵌入图片），不是 url 超链接**：用 `lark-cli sheets +write-image` 这类接口把图片上传到 sheets 的 sheet_image 挂载点，写入 type=`embed-image` 的对象。如果写成 type=`url`（指向云空间文件链接），表格里只会显示一行可点击的文件名超链接，不会显示图片缩略图——这跟历史行形式不一致，用户会要求重做。

相关：[[feedback-sheet-filler-star-rating]]（同一 skill 的另一条规则——星级以截图文字为准）
