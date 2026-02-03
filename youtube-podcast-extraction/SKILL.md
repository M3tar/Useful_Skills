---
name: youtube-podcast-extraction
description: 从 YouTube 播客/访谈等长内容中提取、翻译、分析并产出结构化成果（字幕文本、中英对照翻译、金字塔/黄金圈分析、金句卡片、HTML/PNG 可视化）。当用户提供 YouTube 链接并要求生成摘要、洞见、金句卡片或可分享可视化时使用。
---

# 工作流程

1. 进行前置检查（yt-dlp、ffmpeg、python3、Playwright 或 Chrome、ImageMagick），缺失即停止。
2. 以视频标题创建输出目录，所有产出都放在该目录内。
3. 下载英文字幕，清洗生成 `transcript_en.txt`，并生成 `timestamp_map.json`，保留原始 `.vtt`。
4. 生成 `transcript_zh.md`，在金句位置嵌入英文原句，便于后续时间戳定位。
5. 生成 `pyramid_analysis_zh.md`，包含必要章节（核心论点、子论点、金句、洞见、行动、延伸阅读），金句英文必须逐字原文。
6. 生成金句截图与双语卡片，并回填卡片链接到 `transcript_zh.md` 与 `pyramid_analysis_zh.md`。
7. 生成 `pyramid.html` 并用 Playwright 或 Chrome 导出高分辨率 `pyramid.png`。
8. 可选生成 `publish_content.md`（多平台发布文案）。

# 输出

- `transcript_en.txt`
- `timestamp_map.json`
- `transcript_zh.md`
- `pyramid_analysis_zh.md`
- `quotes_list.json`
- `quotes/` (screenshots, quote cards, `index.md`)
- `pyramid.html`
- `pyramid.png`
- `publish_content.md` (optional)

# 质量要求

- 金句英文必须与字幕原文逐字一致，便于时间戳匹配。
- 在完成金句截图前保留 `subtitle.en.vtt`。
- 产出写入文件，不在回复里粘贴长内容。
- 输出文件内不使用 emoji。

# 参考资料

- 详细命令、验证、故障排查与格式要求见 `references/workflow_zh.md`。
