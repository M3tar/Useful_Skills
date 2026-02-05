---
name: march-text-polish
description: Use when the user wants spoken or messy text reorganized, needs a one-line UI prompt or explanation, wants simplified Chinese copy translated to English/Traditional Chinese (including HK/Macau variant), wants copywriting style optimization, or wants controlled expansion.
---

# March Text Polish

## Overview
Turn messy spoken input into clear, structured copy, craft concise one-line UI text, optionally deliver a multilingual version in a fixed order, optimize copy style, or do controlled expansion.

## When to Use
- User provides long, spoken content and wants a clearer, logical version
- User asks for a one-line prompt or short explanation copy
- User wants simplified Chinese copy translated to English and traditional Chinese
- User wants copywriting style optimization (no automatic expansion)
- User wants controlled expansion to enrich content while staying on-message
- User wants a HK/Macau Traditional Chinese variant in addition to standard Traditional Chinese

Do not use when:
- User only wants literal translation without rewriting
- User explicitly asks for a full article or long-form writing

## Required Prompting
Always show the type map before producing output, and add a recommended choice with a short reason:

1 = 口语内容整理
2 = 一句话提示文案 / 说明文案
3 = 多语版本（中文简体 / English / 中文繁体 / 港澳繁体）
4 = 文案风格优化（不主动扩写）
5 = 扩写 / 丰富（默认上限 +200 字）

If the user gives only “2”, “3”, “4”, or “5”, restate the map briefly and proceed.
Only treat it as an explicit type choice if the user provides the number (1-5) or says "选择/类型/按/用 X" clearly. If they just say "优化/扩写/翻译/整理" etc., still treat it as NOT chosen.
If the user has NOT explicitly chosen a type, you MUST stop after the type map + your recommendation and ask a single short question to choose the type. Do NOT produce any content options yet.

## Core Workflow
1. Identify the type (1 / 2 / 3 / 4 / 5). If unclear or not explicitly chosen, show the type map, give your recommended type + reason, then stop and ask the user to choose. Do NOT produce any output options in this step.
2. Produce options:
   - Types 1 / 2 / 3: always 3 options.
   - Type 4: if content is long, provide 1 optimized version first; if short, provide 2-3 options.
   - Type 5: provide 1 expanded version first.
3. Explain differences and give one recommendation.
4. If user rejects, provide more options.
5. For type 3, confirm the preferred Chinese version first, then output in order: 中文简体 / English / 中文繁体 / 港澳繁体.
6. For type 4, preserve the original tone and emojis unless asked to remove.
7. For type 5, keep meaning consistent and cap expansion at +200 Chinese characters by default; if insufficient, ask whether to continue expanding or rewrite.
8. After every response, ask whether to regenerate and give change directions as lettered options (A/B/C), plus D for light polish and clarity/logic/verbosity check, to avoid collision with type selection.
9. Only ask about other language versions if the user mentions translation, multilingual output, or type 3; otherwise ask a single short question with lettered options so the user can reply with one token. When multiple versions exist, explicitly show how to select a version:
   - L1 = 不需要
   - L2 = 四语版本（中文简体 / English / 中文繁体 / 港澳繁体）
   - 版本选择：默认最新版本；如需指定，请输入 “L2 V1 / L2 V2 / L2 V3”

## Output Rules
- Keep it short, but never lose meaning
- Use Chinese punctuation
- Put spaces between Chinese and English, numbers, or symbols
- Prefer clear structure: 1 / 2 / 3 points
- Add small titles only when the content is long
- For type 4, allow slightly richer tone without expanding content unless asked
- For type 5, expand within +200 字 unless user requests more
- For 港澳繁体, prefer “伺服器” over “服務器” for “server”

## Quick Reference

| Type | Output shape | Must include |
| --- | --- | --- |
| 1 | Structured rewrite | Titles if long, 1 / 2 / 3 points |
| 2 | One-line options | 3 options + reasons + recommendation |
| 3 | Multilingual output | Confirm CN first, then CN / EN / 繁體 / 港澳繁體 |
| 4 | Copywriting optimization | 1 version if long, 2-3 if short; reasons + recommendation |
| 5 | Expansion / enrichment | 1 version; +200 字上限，必要时询问继续或重写 |

## Example (Type 2)
Input:
“点击按钮后，额外增加验证间隔时间，每隔 10 分钟才可以再次点击。”

Output:
备选 1：点击后新增验证间隔，10 分钟内不可再次点击。
备选 2：点击按钮后进入验证间隔，每 10 分钟可再次点击一次。
备选 3：每次点击后需等待 10 分钟，才可再次点击。

理由：
- 备选 1 最简洁，适合提示类文案
- 备选 2 说明更完整，适合需要机制说明的界面
- 备选 3 语气更直接，适合提醒场景

推荐：备选 1

## Common Mistakes
- 只给一个版本，没有备选
- 没有给出推荐
- 忘记中英数字空格
- 句子过长，不分点
- 三语顺序错误
- 风格优化时完全改掉原口吻
- 扩写时偏离原意或超出上限不说明

## Rationalization Table
| Excuse | Reality |
| --- | --- |
| “先给一个版本够了” | 需要 3 个备选，便于用户选择 |
| “翻译直接给了就好” | 先确认中文版本，再输出三语 |
| “太短会丢信息” | 先保证意思完整，再尽量短 |
| “扩写就随便加内容” | 扩写需忠于原意与场景，并遵守上限 |

## Red Flags
- 只给一个版本
- 没有推荐
- 三语顺序不对
- 中英数字未留空格
- 风格优化偏离原意
- 扩写不问就继续加长

## Self-Check
- 内容是否忠于原意
- 是否有 3 个备选
- 是否给出推荐
- 标点是否规范
- 中文与英文、数字之间是否有空格
- 风格优化是否保留口吻与表情
- 扩写是否在上限内且信息一致
