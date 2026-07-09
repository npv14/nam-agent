# Nam — VS Code Copilot Custom Agent

**Senior Software Engineer & Certified Scrum Master** with 10+ years of experience. A custom agent for VS Code Copilot, bilingual in Vietnamese & English.

## 🎯 Capabilities

- 🛠 **Full-stack Development** — architecture, code review, debugging, CI/CD, DevOps
- 🏃 **Scrum Master** — sprint planning, standups, retrospectives, burndown charts, user stories
- 👨‍🏫 **Technical Leadership** — mentoring, ADR/RFC, trade-off analysis, stakeholder communication

## 📦 Included Skills (7 Local Skills)

| Skill | Description |
|-------|-------------|
| 📰 **daily-report** | Generate HTML daily reports on AI developments with history deduplication |
| 📢 **community-post** | Convert daily HTML reports into bilingual (VI/EN) social media posts |
| 📗 **excel-xlsx** | Create/edit Excel workbooks, formulas, formatting, CSV/TSV, dashboards |
| 📝 **markitdown** | Convert PDF/Word/Excel documents to well-formatted Markdown |
| 📊 **powerpoint-pptx** | Create/edit PowerPoint decks with layouts, placeholders, charts, notes |
| 📘 **word-docx** | Create/edit Word documents with styles, tracked changes, tables, sections |
| 🎨 **word-beautifier** | Redesign Word documents into modern UWA Blue & Gold professional reports (VI) |

## 🚀 Installation

1. Copy this repo to your VS Code workspace: `.github/agents/` and `.agents/skills/`
2. The agent **Nam** will appear in the agent picker dropdown in Copilot Chat
3. Or type `/` to see Nam in the available agents list

## 📁 Structure

```
nam-agent/
├── .github/
│   └── agents/
│       └── nam.agent.md          # Agent definition
├── .agents/
│   └── skills/
│       ├── community-post/       # Social media post generator
│       ├── daily-report/         # AI daily report generator
│       ├── excel-xlsx/           # Excel workbook tools
│       ├── markitdown/           # Document → Markdown converter
│       ├── powerpoint-pptx/      # PowerPoint deck tools
│       ├── word-beautifier/      # Word document beautifier (VI)
│       └── word-docx/            # Word document tools
└── README.md
```

## 🌐 Languages

- **Vietnamese** (primary) — mặc định giao tiếp bằng tiếng Việt
- **English** (fluent) — automatically switches when user uses English
