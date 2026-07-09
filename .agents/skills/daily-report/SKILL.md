---
name: Daily AI Report Generator
slug: daily-report
version: 1.0.0
homepage: https://clawic.com/skills/daily-report
description: "Generate a comprehensive, visually stunning HTML daily report on AI developments based on specified topics. Automatically runs a history check on previous reports to avoid repetition of topics, metrics, and news."
changelog: Relocated to workspace agent skills folder with explicit DailyNews output configurations.
metadata: {"clawdbot":{"emoji":"📰","requires":{"bins":[]},"os":["linux","darwin","win32"]}}
---

## When to Use

Use when the task requires generating the daily AI Frontier HTML report (or equivalent news digests) and associated community post drafts from the latest AI developments, while ensuring that the generated content contains only new information and does not duplicate news from previous days' HTML files in the `DailyNews` folder. The generated HTML report files must always be outputted into `c:\Projects\WorkSpace\DailyNews\`.

## Core Rules

### 1. Run History Verification first

- Before gathering information or writing any content, run the history checker utility:
  `python c:\Projects\WorkSpace\DailyNews\check_history.py` (or view `c:\Projects\WorkSpace\DailyNews\covered_topics.txt`).
- Identify the list of news headlines, benchmarks, metrics, and announcements that have already been covered in previous days.
- Ensure that the new report covers different details/news.

### 2. Prioritize new and incremental updates

- Focus on new model releases, pricing changes, benchmarks, funding rounds, or breakthroughs that happened since the last report.
- Do not repeat historical data (such as Anthropic's $65B Series H or DeepSeek's permanent 75% price cut to $0.435) as "new today" updates.
- If a requested topic has no new updates for today, write a brief, professional summary stating there are no major changes since the previous report (referencing the date of the last report), rather than copying and pasting the same news block.

### 3. Maintain premium glassmorphism styling and structure

- Ensure the output HTML keeps the exact premium glassmorphic light/dark-themed dashboard layout.
- Use Outfit and Inter Google Fonts.
- Provide interactive elements: a sidebar navigation menu to toggle tabs and a filterable model comparison table, both implemented in vanilla JavaScript.
- Maintain custom SVG icons for each topic section.

### 4. Create correct output files in DailyNews folder

- The main output file must be saved as `c:\Projects\WorkSpace\DailyNews\daily_report.html` (always containing the latest version).
- A date-specific copy of the report must also be created in the same directory and named matching the pattern `c:\Projects\WorkSpace\DailyNews\daily_report_DD_MM_YY.html` (e.g. `daily_report_07_06_26.html` for June 7th, 2026).

## Common Traps

- **Repeating News**: Carrying over old news items (like Google I/O 2026 or the DeepSeek price cut) into a new report as if they are fresh.
- **Skipping the Checker**: Generating content without running the `check_history.py` script, resulting in repetitive content.
- **Visual Inconsistency**: Breaking the responsive sidebar navigation or light/dark mode styling during updates.
- **Wrong Output Directory**: Saving the output HTML files to the `.agents/skills` folder instead of the `c:\Projects\WorkSpace\DailyNews\` directory.
- **Wrong Date Formatting**: Naming the date-specific report with the wrong format (e.g. using slashes or dashes instead of underscores like `daily_report_07_06_26.html`).
- **Hardcoding Date**: Forgetting to update the date badge or banner heading in the HTML file to match the current date.
