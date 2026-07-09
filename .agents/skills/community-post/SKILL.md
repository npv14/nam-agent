---
name: Community Post Generator
slug: community-post
version: 1.0.0
homepage: https://clawic.com/skills/community-post
description: "Transform the daily HTML report into an engaging, bilingual (Vietnamese/English) social media/community post with high engagement headlines, formatted bullet points, and discussion calls."
changelog: Initial release as a structured agent skill following the daily-report pattern.
metadata: {"clawdbot":{"emoji":"📢","requires":{"bins":[]},"os":["linux","darwin","win32"]}}
---

## When to Use

Use when the task requires generating a social media or community post draft from the daily AI Frontier HTML report, converting its key updates, quantitative metrics, and news into a structured, bilingual format (Vietnamese and English).

## Core Rules

### 1. Analyze the Input HTML Report

- Read the latest daily report from `c:\Projects\WorkSpace\DailyNews\daily_report.html`.
- Parse the report's date, metrics, and key updates.

### 2. Format the Bilingual Post

- Output must contain two clearly separated versions: **Bản tiếng Việt** first, followed by **English Version**.
- Each version must strictly follow this structure:
  1. **Headline (Tiêu đề)**: Use eye-catching emojis (e.g., 🔥, 🚀, 💡, 💻) and summarize the most exciting news in a single line.
  2. **Intro (Lời dẫn)**: State the date and introduce the critical AI news.
  3. **Core Topics (Nội dung chính)**: Cover 2 to 4 major topics with short, bulleted points. Bold key numbers, product names, and benchmarks (e.g., **$0.435/1M**, **Claude Opus 4.8**).
  4. **Call to Action / Discussion (Kêu gọi thảo luận)**: End with a compelling, open-ended question prompting community discussion.
  5. **Hashtags**: Add 4 to 6 relevant hashtags (e.g., `#AIFrontier`, `#TechNews`, `#ClaudeCode`).

### 3. Maintain Tone and Style

- **Tone**: Insightful, forward-looking, professional, and engaging.
- **Style**: Bulleted, concise, utilizing whitespace, avoiding blocky paragraphs.

### 4. Create the correct output file

- Save the bilingual post draft to `c:\Projects\WorkSpace\DailyNews\community_post_draft.txt`.

## Common Traps

- **Incorrect Input File**: Attempting to read input from somewhere other than `c:\Projects\WorkSpace\DailyNews\daily_report.html`.
- **Incorrect Output File**: Saving to a file other than `c:\Projects\WorkSpace\DailyNews\community_post_draft.txt` or saving it in the `.agents/skills` folder.
- **Missing Bilingual Separation**: Combining the languages or forgetting to label the **Bản tiếng Việt** and **English Version** headings clearly.
- **Missing Quantitative Details**: Omitting specific metrics (like prices, benchmarks, valuations) that make the post valuable.
- **Lack of Emojis and Spacing**: Creating dense blocks of text without emojis or spacing, which reduces readability.
