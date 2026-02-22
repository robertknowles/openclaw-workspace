---
name: sheet-tracker
description: Read and write to the OpenClaw PropPath Tracker Google Sheet for task management, research pipeline, and lead generation tracking.
metadata: {"openclaw":{"emoji":"📊","requires":{"bins":["gog"]}}}
---

# sheet-tracker

Use `gog` to read and write the PropPath Tracker Google Sheet.

## Config
- Spreadsheet ID: `1Kx2ft1rMZQ0KgncQUtWv2R2cRtdQAO4JmQnea-3FUk4`
- Account: `robert.knowles2884@gmail.com`
- Sheets: TaskManager, ResearchPipeline, LeadGeneration

Always use `--account robert.knowles2884@gmail.com` or ensure GOG_ACCOUNT is set.

## TaskManager sheet
Columns: Task | Agent | Status | Started | Last Update | Next Step

Read all tasks:
`gog sheets get 1Kx2ft1rMZQ0KgncQUtWv2R2cRtdQAO4JmQnea-3FUk4 "TaskManager!A:F" --json`

Add a new task row:
`gog sheets append 1Kx2ft1rMZQ0KgncQUtWv2R2cRtdQAO4JmQnea-3FUk4 "TaskManager!A:F" --values-json '[["<task>","<agent>","<status>","<started>","<updated>","<next>"]]' --insert INSERT_ROWS`

## ResearchPipeline sheet
Columns: Company | Location | Status | Research Date | Notes | Priority

Add a company:
`gog sheets append 1Kx2ft1rMZQ0KgncQUtWv2R2cRtdQAO4JmQnea-3FUk4 "ResearchPipeline!A:F" --values-json '[["<company>","<location>","<status>","<date>","<notes>","<priority>"]]' --insert INSERT_ROWS`

## LeadGeneration sheet
Columns: Name | Company | Location | Status | Contact Info | Source | Notes

Add a lead:
`gog sheets append 1Kx2ft1rMZQ0KgncQUtWv2R2cRtdQAO4JmQnea-3FUk4 "LeadGeneration!A:G" --values-json '[["<name>","<company>","<location>","<status>","<contact>","<source>","<notes>"]]' --insert INSERT_ROWS`

## Notes
- Always use `--input USER_ENTERED` for update commands
- Use `--json` flag for all read commands
- Use `--insert INSERT_ROWS` when appending to avoid overwriting data
- zsh users: run `setopt NO_BANG_HIST` before commands with `!` in cell ranges
- Confirm with Rob before clearing any sheet data

