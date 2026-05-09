# Heartbeat Check List

This file contains tasks for the heartbeat service to check periodically.

## Examples

- Check for unread messages
- Review upcoming calendar events
- Check device status (e.g., MaixCam)

## Instructions

- Execute ALL tasks listed below. Do NOT skip any task.
- For simple tasks (e.g., report current time), respond directly.
- For complex tasks that may take time, use the spawn tool to create a subagent.
- The spawn tool is async - subagent results will be sent to the user automatically.
- After spawning a subagent, CONTINUE to process remaining tasks.
- Only respond with HEARTBEAT_OK when ALL tasks are done AND nothing needs attention.

- 📋 今日任务：撰写一篇 OpenWrt 教程文章
  1. 读取 memory/MEMORY.md，了解已写过的主题和读者反馈
  2. 选择一个尚未写过的 OpenWrt 主题（如随身WiFi刷机、网络设置、插件安装等）
  3. 使用 spawn 工具依次调用：researcher → analyzer → rewriter → designer → reviewer
  4. 主编汇总各成员输出，生成最终文章，保存到 article/文章标题.md
  5. 更新 memory/MEMORY.md，记录本次写作主题和简要评价
  6. 完成后回复 HEARTBEAT_OK

---

Add your heartbeat tasks below this line:
