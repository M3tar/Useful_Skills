# Skills 目录说明（README）

更新日期：2026-02-03

## 更新记录
- 2026-02-03：新增 README，补充三个 skill 的用途、使用方式与注意事项。

本 README 说明此目录下每个 skill 的用途、触发场景、产出与使用方式，便于后续放到 GitHub 后回顾学习。

## 统一使用方式（所有 skills）

1) 目录与软链接
- 真实目录：`/Users/mercury/Codex+Claude_Code/Skills/<skill-name>`
- 软链接入口：`/Users/mercury/.codex/skills/<skill-name>`
- 说明：superpowers 从 `~/.codex/skills/` 查找技能，软链接必须保留。

2) 调用命令
```bash
~/.codex/superpowers/.codex/superpowers-codex use-skill <skill-name>
```

3) 可选：首次运行 superpowers（若环境提示需要）
```bash
~/.codex/superpowers/.codex/superpowers-codex bootstrap
```

---

## 1) march-text-polish

- 目录：`/Users/mercury/Codex+Claude_Code/Skills/march-text-polish`
- 入口：`/Users/mercury/.codex/skills/march-text-polish`
- 用途：把口语/零散文本整理为清晰文案；生成一句话提示；多语输出；文案风格优化；受控扩写。

### 适用场景
- 口语化内容需要结构化整理
- 需要一句话 UI 提示/说明
- 需要多语版本（中文简体 / English / 中文繁体 / 港澳繁体）
- 需要文案风格优化（不主动扩写）
- 需要受控扩写（默认 +200 字上限）

### 类型提示（必须先展示类型图）
```
1 = 口语内容整理
2 = 一句话提示文案 / 说明文案
3 = 多语版本（中文简体 / English / 中文繁体 / 港澳繁体）
4 = 文案风格优化（不主动扩写）
5 = 扩写 / 丰富（默认上限 +200 字）
```

### 核心规则（简版）
- 类型 1/2/3：必须给 3 个备选 + 理由 + 推荐。
- 类型 4：短文 2-3 个版本；长文 1 个优化版。
- 类型 5：先给 1 个扩写版本，超上限需确认。
- 多语输出顺序固定：中文简体 / English / 中文繁体 / 港澳繁体。
- 中文与英文、数字之间要留空格。
- 每次回复后提供 A/B/C 方向选项 + D（轻度润色与逻辑检查）。

### 演示示例（简版）
用户输入：
“点击按钮后，候选额外增加验证间隔时间，每隔 10 分钟才可以再次点击。”

输出示例：
备选 1：点击后新增验证间隔，10 分钟内不可再次点击。
备选 2：点击按钮后进入验证间隔，每 10 分钟可再次点击一次。
备选 3：每次点击后需等待 10 分钟，才可再次点击。

理由：
- 备选 1 最简洁，适合提示类文案
- 备选 2 说明更完整，适合需要机制说明的界面
- 备选 3 语气更直接，适合提醒场景

推荐：备选 1

### 注意事项
- 只改真实目录里的文件，不要删软链接。
- 三/四语输出顺序固定，不可打乱。
- 港澳繁体优先用“伺服器”。

---

## 2) skill-creator

- 目录：`/Users/mercury/Codex+Claude_Code/Skills/skill-creator`
- 入口：`/Users/mercury/.codex/skills/skill-creator`
- 用途：指导如何创建/迭代一个标准 skill，包含结构规范、写作风格、脚本与打包流程。

### 适用场景
- 想新建一个 skill
- 想升级/迭代已有 skill
- 想打包发布 skill

### 目录结构要点
```
<skill-name>/
├── SKILL.md (必需)
├── scripts/        (可选)
├── references/     (可选)
└── assets/         (可选)
```

### 关键流程（简版）
1. 通过示例明确触发场景和使用方式。
2. 规划可复用内容（scripts / references / assets）。
3. 初始化：运行 `scripts/init_skill.py` 生成模板目录。
4. 编辑 SKILL.md（动词开头指令式写法）。
5. 打包：运行 `scripts/package_skill.py`（先自动校验）。
6. 迭代优化。

### 常用脚本
```bash
# 创建新 skill 模板
/Users/mercury/Codex+Claude_Code/Skills/skill-creator/scripts/init_skill.py <skill-name> --path <output-directory>

# 打包 skill
/Users/mercury/Codex+Claude_Code/Skills/skill-creator/scripts/package_skill.py <path/to/skill-folder>
```

### 备注
- 许可证：见 `skill-creator/LICENSE.txt`。

---

## 3) youtube-podcast-extraction

- 目录：`/Users/mercury/Codex+Claude_Code/Skills/youtube-podcast-extraction`
- 入口：`/Users/mercury/.codex/skills/youtube-podcast-extraction`
- 用途：从 YouTube 播客/访谈等长内容中提取、翻译、分析并生成结构化成果（文本 + 可视化）。

### 触发场景
- 用户提供 YouTube 链接
- 需要摘要/洞见/金句卡片/可分享可视化

### 产出清单（核心）
- `transcript_en.txt`
- `timestamp_map.json`
- `transcript_zh.md`
- `pyramid_analysis_zh.md`
- `quotes_list.json`
- `quotes/`（截图与卡片）
- `pyramid.html`
- `pyramid.png`
- `publish_content.md`（可选）

### 流程概览（简版）
1. 前置检查（yt-dlp / ffmpeg / python3 / Playwright 或 Chrome / ImageMagick）。
2. 下载字幕并清洗生成英文文本与时间戳映射。
3. 翻译成中文（保留关键英文原句用于定位）。
4. 金字塔分析（含金句中英对照）。
5. 生成金句截图与双语卡片，回填到文档。
6. 生成 HTML 可视化与 PNG 导出。
7. 可选生成多平台发布文案。

### 质量与规范（重点）
- 金句英文必须与字幕原文逐字一致。
- 保留 `subtitle.en.vtt` 直到金句截图完成。
- 产出写入文件，不在回复里粘贴长内容。
- 输出文件内不使用 emoji。

### 详细参考
- 详尽命令、验证与故障排查：
  `youtube-podcast-extraction/references/workflow_zh.md`

---

## 变更与维护建议

- 修改 skill 时优先改真实目录；软链接只用于挂载。
- 如果目录名改变，必须重建 `~/.codex/skills/` 下的软链接。
- 需要对外发布时，建议先用 `skill-creator` 的打包脚本校验。
