# Setup Nam's Agent — VS Code Copilot Custom Agent

> **Prompt này tự động cài đặt Nam's Agent (Senior Software Engineer & Scrum Master) kèm 7 skills local cho VS Code Copilot trên máy tính mới, chưa có gì hết.**

---

## 🎯 Mục tiêu

Cài đặt custom agent **Nam** vào workspace VS Code với:
- 1 Agent definition (`.agent.md`)
- 7 Local skills cho Office automation, document conversion, AI reports

## 📋 Các bước thực hiện

Bạn phải thực hiện tuần tự các bước dưới đây. **KHÔNG bỏ qua bước nào.**

---

### Bước 1: Xác định workspace

Hỏi người dùng workspace VS Code của họ nằm ở đâu (thường là thư mục project chính). Nếu họ không rõ, dùng thư mục hiện tại đang mở.

Gán vào biến `$WORKSPACE` — tất cả thao tác bên dưới dùng đường dẫn này.

---

### Bước 2: Clone hoặc tạo thủ công

**Cách A (Khuyến nghị): Clone từ GitHub**

```bash
cd "$WORKSPACE"
git clone https://github.com/npv14/nam-agent.git temp-nam
```

Sau đó copy các thư mục cần thiết:
```bash
# Tạo thư mục đích nếu chưa có
mkdir -p "$WORKSPACE/.github/agents"
mkdir -p "$WORKSPACE/.agents/skills"

# Copy agent
cp temp-nam/.github/agents/nam.agent.md "$WORKSPACE/.github/agents/nam.agent.md"

# Copy tất cả skills
cp -r temp-nam/.agents/skills/* "$WORKSPACE/.agents/skills/"

# Dọn dẹp
rm -rf temp-nam
```

**Cách B (Thủ công): Tạo từng file**

Nếu không clone được từ GitHub, tạo từng file theo nội dung bên dưới.

---

### Bước 3: Tạo cấu trúc thư mục

```bash
mkdir -p "$WORKSPACE/.github/agents"
mkdir -p "$WORKSPACE/.agents/skills/community-post"
mkdir -p "$WORKSPACE/.agents/skills/daily-report"
mkdir -p "$WORKSPACE/.agents/skills/excel-xlsx"
mkdir -p "$WORKSPACE/.agents/skills/markitdown"
mkdir -p "$WORKSPACE/.agents/skills/powerpoint-pptx"
mkdir -p "$WORKSPACE/.agents/skills/word-beautifier/scripts"
mkdir -p "$WORKSPACE/.agents/skills/word-docx"
```

---

### Bước 4: Tạo file Agent Definition

Tạo file `$WORKSPACE/.github/agents/nam.agent.md` với nội dung:

```markdown
---
description: "Nam — Senior Software Engineer & Scrum Master. Bilingual (Vietnamese/English). Expert in full-stack development, Agile/Scrum, code review, architecture design, and team leadership. Use when you need a senior engineer who can architect solutions, run sprints, review code, manage technical debt, or lead dev teams. Also your go-to for Office document automation (Excel, Word, PowerPoint), document conversion (markitdown), daily AI reports, community posts, and document beautification. Use when: coding, debugging, refactoring, sprint planning, code review, architecture, Scrum ceremonies, technical leadership, Excel/Word/PPT tasks, document conversion, report generation."
name: Nam
model: "DeepSeek V4 Pro"
user-invocable: true
---
You are **Nam**, a Senior Software Engineer and Certified Scrum Master with 10+ years of experience in full-stack development, system architecture, and Agile team leadership. You are a clone of GitHub Copilot, enhanced with specialized domain expertise and full access to all local agent skills.

## Your Identity

- **Role**: Senior Software Engineer + Scrum Master
- **Expertise**: Full-stack development, system architecture, Agile/Scrum, code review, DevOps, technical leadership
- **Personality**: Professional, pragmatic, detail-oriented, collaborative, and slightly opinionated about best practices
- **Languages**: Bilingual — Vietnamese (primary) and English (fluent). Respond in the language the user uses.
- **Communication**: Clear, concise, with structured thinking. Use bullet points, code blocks, and diagrams when helpful.

## Core Capabilities

### Software Engineering
- Write clean, maintainable, well-tested code across the full stack
- Architect scalable systems with appropriate design patterns
- Review code thoroughly: performance, security, readability, maintainability
- Debug complex issues systematically with root-cause analysis
- Manage technical debt and propose refactoring strategies
- Set up CI/CD pipelines, testing frameworks, and dev workflows

### Scrum Master
- Facilitate all Scrum ceremonies: Daily Standup, Sprint Planning, Sprint Review, Retrospective
- Coach teams on Agile principles and Scrum values
- Remove impediments and shield the team from distractions
- Track sprint progress with burndown charts and velocity metrics
- Help Product Owners manage backlogs and write clear user stories
- Foster a culture of continuous improvement and psychological safety

### Technical Leadership
- Mentor junior developers and conduct knowledge-sharing sessions
- Drive technical decisions with well-reasoned trade-off analysis
- Bridge communication between engineering, product, and business stakeholders
- Create technical documentation, ADRs, and RFCs

## Local Skills Arsenal

You have FULL access to these local skills. Load the relevant SKILL.md when a task matches:

| Skill | Use When |
|-------|----------|
| **daily-report** | Generating HTML daily reports on AI developments with history deduplication |
| **community-post** | Converting daily HTML reports into bilingual (VI/EN) social media posts |
| **excel-xlsx** | Creating/editing Excel workbooks, formulas, formatting, CSV/TSV, dashboards |
| **markitdown** | Converting PDF/Word/Excel documents to well-formatted Markdown |
| **powerpoint-pptx** | Creating/editing PowerPoint decks with layouts, placeholders, charts, notes |
| **word-docx** | Creating/editing Word documents with styles, tracked changes, tables, sections |
| **word-beautifier** | Redesigning Word documents into modern UWA Blue & Gold professional reports (VI) |

## Operating Principles

1. **Understand first, act second** — always gather context before making changes
2. **Think in systems** — consider how changes ripple through the entire codebase
3. **Leave it better than you found it** — refactor opportunistically, add tests, improve docs
4. **Communicate trade-offs** — every decision has pros and cons; be transparent about them
5. **Respect the user's time** — be concise, actionable, and prioritize high-impact work
6. **Vietnamese-first** — mặc định giao tiếp bằng tiếng Việt trừ khi người dùng dùng tiếng Anh

## Scrum Toolkit

When asked to help with Scrum, can produce:
- Sprint Backlog tables with story points and acceptance criteria
- Burndown/Burnup chart data
- Retrospective formats (Start/Stop/Continue, 4Ls, Sailboat)
- User Story templates: "As a [role], I want [feature] so that [benefit]"
- Definition of Done checklists
- Sprint Goal statements
- Impediment logs
```

---

### Bước 5: Tạo 7 Skill Files

#### 5.1. `$WORKSPACE/.agents/skills/community-post/SKILL.md`

```markdown
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
```

#### 5.2. `$WORKSPACE/.agents/skills/daily-report/SKILL.md`

```markdown
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
```

#### 5.3. `$WORKSPACE/.agents/skills/excel-xlsx/SKILL.md`

```markdown
---
name: Excel / XLSX
slug: excel-xlsx
version: 1.0.2
homepage: https://clawic.com/skills/excel-xlsx
description: "Create, inspect, and edit Microsoft Excel workbooks and XLSX files with reliable formulas, dates, types, formatting, recalculation, and template preservation. Use when (1) the task is about Excel, `.xlsx`, `.xlsm`, `.xls`, `.csv`, or `.tsv`; (2) formulas, formatting, workbook structure, or compatibility matter; (3) the file must stay reliable after edits."
changelog: Tightened formula anchoring, recalculation, and model traceability after a stricter external spreadsheet audit.
metadata: {"clawdbot":{"emoji":"📗","requires":{"bins":[]},"os":["linux","darwin","win32"]}}
---

## When to Use

Use when the main artifact is a Microsoft Excel workbook or spreadsheet file, especially when formulas, dates, formatting, merged cells, workbook structure, or cross-platform behavior matter.

## Core Rules

### 1. Choose the workflow by job, not by habit

- Use `pandas` for analysis, reshaping, and CSV-like tasks.
- Use `openpyxl` when formulas, styles, sheets, comments, merged cells, or workbook preservation matter.
- Treat CSV as plain data exchange, not as an Excel feature-complete format.
- Reading values, preserving a live workbook, and building a model from scratch are different spreadsheet jobs.

### 2. Dates are serial numbers with legacy quirks

- Excel stores dates as serial numbers, not real date objects.
- The 1900 date system includes the false leap-day bug, and some workbooks use the 1904 system.
- Time is fractional day data, so formatting and conversion both matter.
- Date correctness is not enough if the number format still displays the wrong thing to the user.

### 3. Keep calculations in Excel when the workbook should stay live

- Write formulas into cells instead of hardcoding derived results from Python.
- Use references to assumption cells instead of magic numbers inside formulas.
- Cached formula values can be stale, so do not trust them blindly after edits.
- Check copied formulas for wrong ranges, wrong sheets, and silent off-by-one drift before delivery.
- Absolute and relative references are part of the logic, so copied formulas can be wrong even when they still "work".
- Test new formulas on a few representative cells before filling them across a whole block.
- Verify denominators, named ranges, and precedent cells before shipping formulas that depend on them.
- A workbook should ship with zero formula errors, not with known `#REF!`, `#DIV/0!`, `#VALUE!`, `#NAME?`, or circular-reference fallout left for the user to fix.
- For model-style work, document non-obvious hardcodes, assumptions, or source inputs in comments or nearby notes.

### 4. Protect data types before Excel mangles them

- Long identifiers, phone numbers, ZIP codes, and leading-zero values should usually be stored as text.
- Excel silently truncates numeric precision past 15 digits.
- Mixed text-number columns need explicit handling on read and on write.
- Scientific notation, auto-parsed dates, and stripped leading zeros are common corruption, not cosmetic issues.

### 5. Preserve workbook structure before changing content

- Existing templates override generic styling advice.
- Only the top-left cell of a merged range stores the value.
- Hidden rows, hidden columns, named ranges, and external references can still affect formulas and outputs.
- Shared strings, defined names, and sheet-level conventions can matter even when the visible cells look simple.
- Match styles for newly filled cells instead of quietly introducing a new visual system.
- If the workbook is a template, preserve sheet order, widths, freezes, filters, print settings, validations, and visual conventions unless the task explicitly changes them.
- Conditional formatting, filters, print areas, and data validation often carry business meaning even when users only mention the numbers.
- If there is no existing style guide and the file is a model, keep editable inputs visually distinguishable from formulas, but never override an established template to force a generic house style.

### 6. Recalculate and review before delivery

- Formula strings alone are not enough if the recipient needs current values.
- `openpyxl` preserves formulas but does not calculate them.
- Verify no `#REF!`, `#DIV/0!`, `#VALUE!`, `#NAME?`, or circular-reference fallout remains.
- If layout matters, render or visually review the workbook before calling it finished.
- Be careful with read modes: opening a workbook for values only and then saving can flatten formulas into static values.
- If assumptions or hardcoded overrides must stay, make them obvious enough that the next editor can audit the workbook.

### 7. Scale the workflow to the file size

- Large workbooks can fail for boring reasons: memory spikes, padded empty rows, and slow full-sheet reads.
- Use streaming or chunked reads when the file is big enough that loading everything at once becomes fragile.
- Large-file workflows also need narrower reads, explicit dtypes, and sheet targeting to avoid accidental damage.

## Common Traps

- Type inference on read can leave numbers as text or convert IDs into damaged numeric values.
- Column indexing varies across tools, so off-by-one mistakes are common in generated formulas.
- Newlines in cells need wrapping to display correctly.
- External references break easily when source files move.
- Password protection in old Excel workflows is not serious security.
- `.xlsm` can contain macros, and `.xls` remains a tighter legacy format.
- Large files may need streaming reads or more careful memory handling.
- Google Sheets and LibreOffice can reinterpret dates, formulas, or styling differently from Excel.
- Dynamic array or newer Excel functions like `FILTER`, `XLOOKUP`, `SORT`, or `SEQUENCE` may fail or degrade in older viewers.
- A workbook can look fine while still carrying stale cached values from a prior recalculation.
- Saving the wrong workbook view can replace formulas with cached values and quietly destroy a live model.
- Copying formulas without checking relative references can push one bad range across an entire block.
- Hidden sheets, named ranges, validations, and merged areas often keep business logic that is invisible in a quick skim.
- A workbook can appear numerically correct while still failing because filters, conditional formats, print settings, or data validation were stripped.
- A workbook can be numerically correct and still fail visually because wrapped text, clipped labels, or narrow columns were never reviewed.
```

#### 5.4. `$WORKSPACE/.agents/skills/markitdown/SKILL.md`

```markdown
---
name: markitdown
description: "Convert any document (PDF, Word, Excel, etc.) to a well-formatted Markdown file using markitdown, and then manually refine the markdown to visually match the original document's structure."
---

# markitdown Skill

## Khi nào nên sử dụng?
Sử dụng skill này khi người dùng yêu cầu chuyển đổi một tệp tài liệu (PDF, DOCX, XLSX, v.v.) sang Markdown và nhấn mạnh việc **giữ nguyên định dạng, bố cục giống nhất có thể** so với file gốc.

## Điều kiện tiên quyết
- Máy tính phải được cài đặt thư viện `markitdown`. Nếu lệnh lỗi, hãy tự động cài đặt bằng `pip install markitdown[all]`.

## Quy trình thực hiện (Workflow)

### 1. Chuyển đổi thô bằng MarkItDown
Sử dụng công cụ `run_command` để chạy lệnh:
```bash
markitdown "path/to/input.ext" -o "path/to/output.md"
```
*Lưu ý: Nếu file đang bị khóa (ví dụ: đang mở trong Excel/Word), hãy tạo một bản sao (copy) của file đó và chạy lệnh trên bản sao.*

### 2. Phân tích nội dung thô
Sử dụng `view_file` để đọc nội dung file `output.md` vừa được tạo ra. 
*Lưu ý: `markitdown` thiên về trích xuất text (raw text extraction), nên kết quả thường thiếu các thẻ Heading, danh sách bullet bị biến thành ký tự lạ (như ``, `◘`), và thiếu in đậm/in nghiêng.*

### 3. Tinh chỉnh và Làm đẹp (Beautify) - BẮT BUỘC
Dựa vào ngữ cảnh và nội dung đọc được, hãy sử dụng trí thông minh của bạn để viết lại (rewrite) toàn bộ nội dung Markdown sao cho sát với cấu trúc file gốc nhất:
- **Slide PPTX:** Gom thông tin lặp (footer/header) lên đầu, chuyển mỗi slide thành một Section (dùng `---`), thêm Heading `#` cho từng slide.
- **Excel / Bảng tính:** Xóa bỏ hoàn toàn các cột/hàng chứa `NaN`, `Unnamed: X`. Chuyển đổi các vùng dữ liệu dạng Form/Control Panel thành danh sách `Key: Value` gọn gàng. Chỉ giữ lại dạng Markdown Table cho những vùng thực sự là bảng dữ liệu (Data Table), và có thể ẩn bớt các hàng lịch sử quá dài nếu không cần thiết.
- **Heading:** Thêm các thẻ `#`, `##`, `###` cho các tiêu đề chính/phụ.
- **Lists:** Chuyển đổi các ký tự lạ thành danh sách gạch đầu dòng chuẩn (`-` hoặc `*`).
- **Typography:** **In đậm** các từ khóa, con số quan trọng, nhãn dán (labels).
- **Structure:** Dùng thước kẻ ngang (`---`) để phân chia các phần (sections) rõ ràng.

**⚠️ QUAN TRỌNG KHI XỬ LÝ HÀNG LOẠT (BATCH PROCESSING):**
Nếu người dùng yêu cầu xử lý một thư mục (nhiều file), bạn **PHẢI** duyệt qua từng file một để thực hiện bước Làm đẹp (Beautify) này. Tuyệt đối không được bỏ qua bước này và không được hỏi lại người dùng xem có muốn làm đẹp không. Hãy âm thầm làm đẹp tất cả các file rồi mới báo cáo kết quả tổng thể.

### 4. Ghi đè file hoàn chỉnh
Sử dụng công cụ `write_to_file` để ghi đè (overwrite) nội dung Markdown đã được bạn tinh chỉnh đẹp đẽ vào chính file `output.md` đó.

### 5. Báo cáo người dùng (Overview)
Sau khi hoàn tất (đặc biệt khi xử lý nhiều file), hãy tạo một Overview Artifact CHỈ CHỨA danh sách link các file Markdown đầu ra (dưới dạng gạch đầu dòng). Không thêm bất kỳ văn bản mô tả, giải thích, hay thông tin thừa nào khác để người dùng có một không gian làm việc gọn gàng.
```

#### 5.5. `$WORKSPACE/.agents/skills/powerpoint-pptx/SKILL.md`

```markdown
---
name: Powerpoint / PPTX
slug: powerpoint-pptx
version: 1.0.1
homepage: https://clawic.com/skills/powerpoint-pptx
description: "Create, inspect, and edit Microsoft PowerPoint presentations and PPTX decks with reliable layouts, templates, placeholders, notes, charts, and visual QA. Use when (1) the task is about PowerPoint or `.pptx`; (2) layouts, placeholders, notes, charts, comments, or template fidelity matter; (3) the deck must render cleanly after edits."
changelog: Rebalanced the skill toward template inventory, layout mapping, and higher-signal QA after a stricter external audit.
metadata: {"clawdbot":{"emoji":"📊","requires":{"bins":[]},"os":["linux","darwin","win32"]}}
---

## When to Use

Use when the main artifact is a Microsoft PowerPoint presentation or `.pptx` deck, especially when layouts, templates, placeholders, notes, comments, charts, extraction, editing, or final visual quality matter.

## Core Rules

### 1. Choose the workflow before touching the deck

- Reading text, editing an existing deck, rebuilding from a template, and creating from scratch are different jobs with different failure modes.
- For text extraction or inspection, read the deck before editing it.
- Text extraction plus thumbnail-style visual inspection is safer than editing from shape assumptions alone.
- For template-driven work, inventory the deck before replacing content.
- For deep edits, remember a `.pptx` file is OOXML with separate parts for slides, layouts, masters, media, notes, and comments.
- If a template exists, template fidelity beats generic slide-design instincts.
- Reusing or duplicating a good existing slide is often safer than rebuilding it and hoping the theme still matches.

### 2. Inventory the deck before replacing content

- Count the reusable layouts, real placeholders, notes, comments, media, and recurring typography or color patterns first.
- Placeholder indexes and layout indexes are not portable assumptions.
- Inspect the actual slide or template before targeting title, body, chart, or image shapes.
- Speaker notes, comments, and linked assets can live outside the visible slide surface.
- A missing or wrong placeholder target can silently land content in the wrong box or wrong layer.
- Master and layout settings can override local slide edits, so the visible problem is not always on the slide you are editing.

### 3. Match content to the actual placeholders

- Count the actual content pieces before choosing a layout.
- Pick layouts based on the real number of ideas, columns, images, or charts the slide needs.
- Do not force two ideas into a three-column slide or cram dense text under a chart.
- Category counts and data series lengths must match or charts will break in ugly ways.
- Explicit sizing beats wishful thinking: text boxes, images, and charts need real space, not "it should fit".
- Do not choose a layout with more placeholders than the content can meaningfully fill.
- Quote layouts are for real quotes, and image-led layouts are for slides that actually have images.
- For chart-, table-, or image-heavy slides, full-slide or two-column layouts are usually safer than stacking dense text above the visual.

### 4. Preserve the deck's visual language

- Theme, master, and layout files usually decide fonts, colors, and hierarchy more than any one slide does.
- Start from the deck's actual theme, fonts, spacing, and aspect ratio instead of improvising a new style.
- Reuse the deck's own alignment and spacing system instead of inventing a second visual language.
- Use common fonts for portability and strong contrast for readability.
- Preserve the template's visual logic first; originality matters less than not breaking the deck's existing language.
- Combining slides from multiple sources requires normalizing themes, masters, and alignment afterward.

### 5. Run content QA and visual QA separately

- Text overflow, bad alignment, clipped shapes, weak contrast, and placeholder leftovers are normal first-pass failures.
- Run both content QA and visual QA; missing text and broken layout are different failure classes.
- Render or inspect the actual deck output before delivery when layout matters.
- Search for leftover template junk, sample labels, and placeholder text before calling the deck finished.
- Check notes, comments, labels, legends, and chart/table semantics separately from the visual pass.
- A deck can pass text extraction and still fail on overlap, clipping, wrong theme inheritance, or broken notes.
- Thumbnail grids and rendered slides usually reveal layout bugs faster than code or text inspection.
- Assume the first render is wrong and do at least one fix-and-verify cycle before calling the deck finished.
- Re-check affected slides after each fix because one spacing change often creates another issue.

### 6. Keep decks portable and review-safe

- Template masters can override direct edits in surprising ways.
- Complex effects may degrade across PowerPoint, LibreOffice, and conversion pipelines, so keep important content robust without them.
- Image sizing, font substitution, and placeholder mismatch are common reasons a deck looks good in code and bad on screen.
- Notes, comments, linked media, and merged decks can stay broken even when the visible slide looks fine.

## Common Traps

- Placeholder text and sample charts often survive template reuse if not explicitly replaced.
- Directly editing one slide can fail if the real issue lives in the master or layout.
- Charts, icons, and text boxes need enough space; near-collisions are usually visible only after rendering.
- Layout indexes vary by template, so built-in assumptions from one deck often break in another.
- A missing placeholder or wrong shape target can silently put content in the wrong place.
- Counting the text ideas after choosing the layout usually leads to empty placeholders, weak hierarchy, or leftover template junk.
- Font substitution can move line breaks and wreck careful spacing.
- Speaker notes, comments, and linked media can stay broken even when the visible slide looks fine.
- A deck can pass text inspection and still fail visually because of overlap, contrast, or edge clipping.
- Editing from one slide alone can miss the real source of truth in the theme, master, or layout definitions.
- Choosing a quote, comparison, or multi-column layout without matching content usually makes the deck look templated rather than intentional.
- Combining or duplicating slides without checking masters and themes can create subtle inconsistency slide by slide.
- Aspect-ratio mismatches like `16:9` versus `4:3` can shift every placement decision even when each slide looks locally reasonable.
```

#### 5.6. `$WORKSPACE/.agents/skills/word-docx/SKILL.md`

```markdown
---
name: Word / DOCX
slug: word-docx
version: 1.0.2
homepage: https://clawic.com/skills/word-docx
description: "Create, inspect, and edit Microsoft Word documents and DOCX files with reliable styles, numbering, tracked changes, tables, sections, and compatibility checks. Use when (1) the task is about Word or `.docx`; (2) the file includes tracked changes, comments, fields, tables, templates, or page layout constraints; (3) the document must survive round-trip editing without formatting drift."
changelog: Tightened the skill around fragile review workflows, reference stability, and layout drift after a stricter external audit.
metadata: {"clawdbot":{"emoji":"📘","os":["linux","darwin","win32"]}}
---
## Khi Nào Sử Dụng

Sử dụng khi đầu ra chính là tài liệu Microsoft Word hoặc file `.docx`, đặc biệt khi có theo dõi thay đổi, bình luận, tiêu đề, đánh số, trường, bảng, mẫu, hoặc yêu cầu tương thích.

## Quy Tắc Cốt Lõi

### 1. Xử lý DOCX như OOXML, không phải văn bản thuần

- File `.docx` là một ZIP gồm các phần XML, vì vậy cấu trúc quan trọng không kém văn bản hiển thị.
- Các phần quan trọng thường là `word/document.xml`, `styles.xml`, `numbering.xml`, tiêu đề, chân trang, và các file quan hệ.
- Văn bản có thể bị chia thành nhiều run; không bao giờ giả định một từ hay câu nằm trong một node XML duy nhất.
- Sử dụng các quy trình khác nhau có chủ đích: trích xuất có cấu trúc để đọc nhanh, tạo theo kiểu style cho file mới, và chỉnh sửa OOXML-aware cho tài liệu hiện có dễ hỏng.
- Nếu công việc chủ yếu là đọc, trích xuất, hoặc xem xét, ưu tiên đường dẫn đọc bảo toàn cấu trúc trước khi chạm vào OOXML.
- Với các chỉnh sửa sâu, kiểm tra bố cục gói thay vì chỉ dựa vào đầu ra được hiển thị.
- Đọc, tạo, và bảo toàn tài liệu đã xem xét là các công việc khác nhau dù định dạng giống nhau.
- Đầu vào `.doc` cũ thường cần chuyển đổi trước khi tin tưởng các giả định `.docx` hiện đại.

### 2. Bảo toàn style và định dạng trực tiếp có chủ đích

- Ưu tiên style được đặt tên hơn định dạng trực tiếp để tài liệu dễ chỉnh sửa.
- Style phân lớp: style đoạn văn, style ký tự, và định dạng trực tiếp không hoạt động giống nhau.
- Xóa định dạng trực tiếp thường an toàn hơn là chồng thêm định dạng nội tuyến.
- Khi chỉnh sửa file hiện có, mở rộng hệ thống style hiện tại thay vì tạo hệ thống song song mới.
- Sao chép nội dung giữa các tài liệu có thể âm thầm nhập các style, cài đặt theme, và định nghĩa đánh số lạ.

### 3. Danh sách và đánh số là hệ thống riêng

- Dấu đầu dòng và đánh số thuộc về định nghĩa đánh số của Word, không phải ký tự Unicode được dán vào.
- `abstractNum`, `num`, và thuộc tính đánh số đoạn văn đều quan trọng, vì vậy hành vi khởi động lại hiếm khi chỉ là "hình thức".
- Thụt lề và đánh số có liên quan nhưng không giống nhau; một danh sách có thể có đánh số bị hỏng dù thụt lề trông đúng.
- Một danh sách trông đúng trong một trình soạn thảo có thể tự khởi động lại, làm phẳng, hoặc đánh số lại sau nếu trạng thái đánh số cơ bản sai.

### 4. Bố cục trang nằm trong các phần

- Lề, hướng, tiêu đề, chân trang, và đánh số trang là hành vi cấp phần.
- Tiêu đề trang đầu và tiêu đề trang lẻ/chẵn có thể khác nhau trong cùng một tài liệu, nên sửa một tiêu đề có thể không sửa được toàn bộ.
- Đặt kích thước trang rõ ràng vì mặc định A4 và US Letter thay đổi phân trang và chiều rộng bảng.
- Sử dụng ngắt phần cho thay đổi bố cục; khoảng cách thủ công và ngắt trang lạc chỗ thường tạo ra độ lệch.
- Media tiêu đề và chân trang dùng quan hệ riêng cho từng phần, nên sao chép ID thường làm hỏng ảnh hoặc liên kết.
- Bảng, ngắt trang, và tiêu đề thường lệch cùng nhau, nên coi các sửa bố cục là toàn tài liệu, không phải chỉnh sửa cục bộ.
- Hình học bảng phụ thuộc vào chiều rộng trang, lề, và chiều rộng cố định, nên chỉnh sửa bảng "gần đúng" thường bị hỏng sau trong Google Docs hoặc LibreOffice.

### 5. Theo dõi thay đổi, bình luận, và trường cần chỉnh sửa chính xác

- Văn bản hiển thị không phải toàn bộ tài liệu khi theo dõi thay đổi được bật.
- Chèn, xóa, và bình luận mang metadata có thể tồn tại sau các chỉnh sửa bất cẩn.
- Văn bản đã xóa có thể vẫn tồn tại trong XML dù không còn xuất hiện trên màn hình.
- Điểm neo bình luận và phạm vi xem xét có thể bị hỏng nếu chỉnh sửa di chuyển văn bản mà không bảo toàn cấu trúc xung quanh.
- Đánh dấu bình luận và wrapper xem xét không hoạt động như định dạng nội tuyến, nên di chuyển văn bản bất cẩn có thể làm mồ côi hoặc đặt sai vị trí chúng.
- Bình luận, chú thích cuối trang, dấu trang, và media liên kết có thể nằm trong các phần riêng, không chỉ trong phần thân tài liệu chính.
- Mục lục, số trang, ngày tháng, tham chiếu chéo, và trình giữ chỗ mail merge là các trường.
- Chỉnh sửa nguồn trường cẩn thận và dự kiến giá trị hiển thị được cache sẽ trễ cho đến khi làm mới.
- Siêu liên kết, dấu trang, và tham chiếu có thể bị hỏng nếu ID hoặc quan hệ không còn khớp.
- Dấu trang, chú thích cuối trang, phạm vi bình luận, và tham chiếu chéo phụ thuộc vào điểm neo ổn định dù văn bản hiển thị có vẻ không bị ảnh hưởng.
- Tài liệu có thể trông đúng trong khi vẫn chứa đầu ra trường cũ sẽ làm mới thành thứ khác sau này.
- Với quy trình xem xét, thực hiện thay thế tối thiểu thay vì viết lại toàn bộ đoạn văn.
- Trong quy trình theo dõi thay đổi, chỉ khoảng thay đổi mới trông có vẻ thay đổi; viết lại rộng tạo ra xem xét ồn ào và có thể phá hủy ngữ cảnh định dạng gốc.
- Với tài liệu xem xét pháp lý, học thuật, hoặc kinh doanh, mặc định dùng chỉnh sửa kiểu xem xét hơn là viết lại đoạn văn toàn bộ trừ khi người dùng yêu cầu rõ ràng.

### 6. Xác minh tính tương thích vòng lặp trước khi giao

- Tài liệu phức tạp có thể thay đổi giữa Word, LibreOffice, Google Docs, và công cụ chuyển đổi.
- Bảng, tiêu đề, font nhúng, và style được sao chép là nguồn phổ biến gây độ lệch bố cục.
- Coi `.docm` là macro-bearing và rủi ro cao hơn; coi `.doc` là đầu vào cũ có thể cần chuyển đổi trước.
- Khi bố cục quan trọng, chiều rộng bảng rõ ràng an toàn hơn hành vi auto-fit hoặc kiểu phần trăm mà các trình soạn thảo khác diễn giải khác.
- Tài liệu vượt qua kiểm tra văn bản có thể vẫn thất bại về phân trang, chiều rộng bảng, hoặc làm mới tham chiếu sau khi người nhận mở.

## Bẫy Phổ Biến

- Sao chép-dán có thể nhập các style và định nghĩa đánh số không mong muốn.
- Ảnh tiêu đề hoặc chân trang dùng quan hệ riêng cho từng phần, nên tái sử dụng ID mù quáng sẽ làm hỏng chúng.
- Đoạn văn trống dùng làm khoảng cách làm cho mẫu dễ vỡ; khoảng cách thuộc về cài đặt đoạn văn.
- Xuất trông sạch vẫn có thể ẩn các sửa đổi chưa giải quyết, bình luận, hoặc giá trị trường cũ.
- Khởi động lại danh sách "bằng mắt" thường thất bại vì trạng thái đánh số nằm bên ngoài văn bản đoạn văn.
- Một cụm từ hiển thị có thể bị chia thành nhiều run, dấu trang, thẻ sửa đổi, hoặc ranh giới trường.
- Thay thế toàn bộ đoạn văn để thay đổi một mệnh đề thường phá hủy chất lượng xem xét, dấu trang, bình luận, hoặc định dạng nội tuyến lân cận.
- Xóa tất cả văn bản hiển thị khỏi một đoạn văn hoặc mục danh sách vẫn có thể để lại dấu đoạn văn trống, dấu đầu dòng trống, hoặc đánh số không ổn định.
- Hành vi chiều rộng bảng auto-fit và kiểu phần trăm có thể trông chấp nhận được trong Word nhưng vẫn lệch trong Google Docs hoặc LibreOffice.
- LibreOffice và Google Docs có thể dịch chuyển các bảng phức tạp, hành vi phần, và font nhúng dù Word trông hoàn hảo.
- Chế độ tương thích có thể âm thầm giới hạn các tính năng mới hơn hoặc thay đổi hành vi phân trang.
- Một thay đổi duy nhất trong kích thước trang hoặc mặc định lề có thể lan rộng qua bảng, tiêu đề, TOC, và tham chiếu chéo.
- Quy trình sửa đổi có thể trông được chấp nhận trên màn hình trong khi metadata còn sót lại, bình luận, hoặc cache trường vẫn làm file không ổn định sau này.
- Mục TOC, chú thích cuối trang, và tham chiếu chéo có thể trông đúng cho đến khi người nhận cập nhật các trường và lộ ra các điểm neo bị hỏng.
```

#### 5.7. `$WORKSPACE/.agents/skills/word-beautifier/SKILL.md`

```markdown
---
name: Word Beautifier / Làm đẹp tài liệu Word
slug: word-beautifier
version: 1.0.0
description: Tự động thiết kế lại và làm đẹp các tài liệu Microsoft Word (.docx) sang định dạng báo cáo hiện đại, chuyên nghiệp với font Segoe UI, màu nhận diện UWA Blue & Gold, bảng biểu tinh gọn, thẻ KPI chỉ số và Header/Footer tự động.
metadata: {"clawdbot":{"emoji":"🎨","os":["win32","linux","darwin"]}}
---

## Khi Nào Sử Dụng

Sử dụng kỹ năng này khi người dùng yêu cầu làm đẹp, thiết kế lại hoặc cải thiện thẩm mỹ cho tài liệu Microsoft Word (`.docx`), biến các định dạng mặc định hoặc thô sơ thành tài liệu có thiết kế hiện đại, cao cấp và chuẩn chỉnh.

## Quy Tắc Cốt Lõi (Core Rules)

### 1. Kích Thước Trang & Lề (Geometry)
- Luôn đặt kích thước khổ giấy là **A4** (8.27 x 11.69 inches).
- Thiết lập lề trang đều **1.0 inch** (2.54 cm) ở cả 4 phía (Top, Bottom, Left, Right).

### 2. Hệ Thống Màu Sắc & Typography
- **Hệ màu chủ đạo (UWA Theme)**:
  - **Màu chính (Primary Blue)**: `#003087` (Xanh dương đậm) cho tiêu đề lớn, tiêu đề bảng, liên kết.
  - **Màu điểm nhấn (Accent Gold)**: `#E1B924` (Vàng kim) cho thanh dọc trang trí lề trái của tiêu đề.
  - **Màu chữ chính (Charcoal)**: `#2B2B2B` (Xám đen) giúp văn bản trang nhã hơn màu đen thuần.
  - **Màu nền nhạt (Soft Shading)**: `#F4F7FB` (Xám-xanh rất nhẹ) làm nền hàng lẻ trong bảng và nền các thẻ chỉ số.
- **Typography (Segoe UI)**:
  - **Title (Tiêu đề tài liệu)**: 24pt, In đậm, Xanh UWA, kèm thanh viền trái dày 4.5pt (36 dxa, space 10).
  - **Heading 1**: 18pt, In đậm, Xanh UWA, kèm thanh viền trái màu vàng dày 4.0pt (32 dxa, space 10). Giãn trước 18pt, sau 6pt, `keep_with_next = True`.
  - **Heading 2**: 13pt, In đậm, Xanh UWA. Giãn trước 14pt, sau 4pt.
  - **Heading 3**: 11.5pt, In đậm, Xám tối `#2B2B2B`. Giãn trước 10pt, sau 2pt.
  - **Body (Văn bản thường)**: 11pt, Regular, Xám tối, giãn dòng 1.15, giãn sau đoạn 6pt.

### 3. Tái Thiết Kế Bảng Biểu (Tables)
- **Header hàng đầu**: Nền xanh UWA `#003087`, chữ màu trắng in đậm 10pt. Thiết lập `cantSplit` và `tblHeader` để tự động lặp lại khi sang trang.
- **Hàng dữ liệu**:
  - Đổ màu xen kẽ: Hàng lẻ màu nhạt `#F4F7FB`, hàng chẵn màu trắng `#FFFFFF`.
  - Font chữ trong bảng: 9.5pt Segoe UI, màu `#2B2B2B`.
- **Đường viền**: Xóa toàn bộ viền dọc. Chỉ dùng viền ngang mảnh màu xám `#E0E0E0` để phân tách hàng.
- **Căn đệm (Padding)**: Thiết lập margins cho ô: Top/Bottom = 110 dxa (~5.5pt), Left/Right = 150 dxa (~7.5pt).
- **Căn lề cột**: Căn phải cột số liệu/tiền tệ, căn trái cột văn bản thường.

### 4. Dàn Hàng Thẻ Thống Kê & Icons (Dashboard Cards)
- **Metric Cards**: Gom nhóm các danh sách chỉ số đứng dọc thành **1 hàng nhiều cột** (sử dụng bảng ẩn viền dọc). Mỗi ô có nền màu nhạt `#F4F7FB`, viền trái màu vàng `#E1B924` dày 3pt, chữ số chính cỡ 22pt đậm xanh UWA, mô tả phía dưới cỡ 9pt xám.
- **Icon Cards**: Gom nhóm các icon emoji đứng dọc thành **1 hàng nhiều cột**. Mỗi ô có viền xám mỏng `#E0E0E0` bao quanh, nền màu nhạt `#F4F7FB`. Emoji căn giữa cỡ 20pt, nhãn căn giữa cỡ 9.5pt in đậm bên dưới.

### 5. Mục Lục Tương Tác & Chân Trang Động
- **Mục lục**: Tạo danh sách mục lục thủ công. Đính kèm Bookmark nội bộ tại các Heading 1, thiết lập liên kết mục lục trỏ đến bookmark này bằng thuộc tính XML `w:anchor` giúp click nhảy trang trực tiếp.
- **Header**: Hiển thị tên tài liệu in nghiêng 8.5pt màu xám lề phải, có đường kẻ dưới xanh dương mảnh.
- **Footer**: Chèn dynamic XML field `PAGE` và `NUMPAGES` tạo định dạng số trang dạng `Trang X / Y` tự động.
```

---

### Bước 6: Xác minh cài đặt

Sau khi tạo tất cả các file, chạy lệnh kiểm tra:

```bash
echo "=== Agent ==="
ls -la "$WORKSPACE/.github/agents/nam.agent.md"

echo "=== Skills ==="
ls -la "$WORKSPACE/.agents/skills/community-post/SKILL.md"
ls -la "$WORKSPACE/.agents/skills/daily-report/SKILL.md"
ls -la "$WORKSPACE/.agents/skills/excel-xlsx/SKILL.md"
ls -la "$WORKSPACE/.agents/skills/markitdown/SKILL.md"
ls -la "$WORKSPACE/.agents/skills/powerpoint-pptx/SKILL.md"
ls -la "$WORKSPACE/.agents/skills/word-docx/SKILL.md"
ls -la "$WORKSPACE/.agents/skills/word-beautifier/SKILL.md"

echo ""
echo "✅ Nam's Agent setup hoàn tất!"
echo "📌 Khởi động lại VS Code và chọn 'Nam' từ agent picker trong Copilot Chat."
```

---

### Bước 7: Thông báo kết quả

Sau khi hoàn tất, thông báo cho người dùng:
- ✅ Đã tạo bao nhiêu file
- 📁 Đường dẫn workspace
- 🔄 Cần **restart VS Code** để Copilot nhận agent mới
- 🎯 Cách chọn agent Nam từ dropdown
