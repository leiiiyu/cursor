@AGENTS.md

# Claude Code instructions

Claude Code reads this file at the start of every session. Shared project rules live in `AGENTS.md`; keep this file limited to Claude-specific behavior.

## Imports

- Treat `@AGENTS.md` as the source of truth for repository layout, note style, C solution format, and git hygiene.
- Do not duplicate those rules here.

## Session behavior

- This is a Markdown + C notes repo, not an app. Do not spend the session scaffolding a build system.
- Prefer editing the specific note the user named. Use a focused search (single path or glob) before a repo-wide explore.
- When the user asks to “整理笔记”, restructure only the file or section they pointed at; do not rewrite sibling notes.
- When adding LeetCode solutions, keep the C snippet inside the Markdown file unless the user asks for a `.c` source file.

## Tools

- GitHub and Aliyun keys are already in local environment variables (`GITHUB_TOKEN`, `ALIBABACLOUD_ACCESS_KEY_ID`, `ALIBABACLOUD_ACCESS_KEY_SECRET`). Never echo them; do not write CLI profile files.
- For GitHub issue, pull request, release, or Actions work, follow `.cursor/skills/github-workflow/SKILL.md`.
- For Aliyun CLI / OpenAPI, follow `.cursor/skills/aliyun-cli-manage/SKILL.md`.
- Do not run package installs or start servers; there are none to start.

## Memory

- Project facts that apply to every session belong in `AGENTS.md`.
- Do not write personal Claude-only preferences into `AGENTS.md`.
