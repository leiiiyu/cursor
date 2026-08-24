# AGENTS.md

This file is the shared instruction set for coding agents working in this repository (Cursor, GitHub Copilot coding agent, Codex, and others). Humans should still start from `README.md`.

## Project overview

This repository is a **Chinese Computer Science postgraduate entrance exam (408) study log**, hosted at [leiiiyu/cursor](https://github.com/leiiiyu/cursor). It is primarily Markdown notes plus C solutions for LeetCode-style practice. It is not an application codebase: there is no package manager, test runner, or production service.

Subjects currently in tree:

- `01-数据结构/` — data-structure notes and LeetCode practice in C
- `03-操作系统/` — operating-system round-1 notes and OSTEP reading notes

Other 408 subjects (computer networks, computer organization) may be added later using the same numbering and naming style.

## Working language

- Notes, headings, and explanations are written in **Simplified Chinese**.
- Code identifiers, LeetCode titles, and command names stay in their original form (C, English problem names, file names).
- Agent replies to the owner should prefer Chinese unless they ask for another language.

## Directory and naming conventions

Keep new files next to related existing material. Do not invent a parallel tree.

| Area | Pattern | Example |
| --- | --- | --- |
| Subject folders | `NN-中文名/` | `01-数据结构/`, `03-操作系统/` |
| OS round-1 notes | `OS-NN 主题.md` | `03-操作系统/一轮笔记/OS-01 概论.md` |
| LeetCode C notes | `题号-中文标题.md` | `01-数据结构/leetcode刷题C语言/数组/1-两数之和.md` |
| LeetCode heading | `# lc-<id> <中文标题>` | `# lc-1 两数之和` |
| Image assets | sibling `*.assets/` folder | `OS-01 概论.assets/` |

Do not rename existing files or asset folders just to “clean up” encoding. Several asset paths already use URL-encoded Chinese names; changing them breaks Markdown image links.

## Markdown style for notes

Match nearby files rather than introducing a new template.

For **concept notes** (OS / textbook):

1. One H1 title matching the file topic.
2. Numbered H2/H3 sections (`## 1 ...`, `### 1.1 ...`).
3. Short paragraphs. Prefer precise CS terms (进程, 地址空间, 系统调用) over metaphor.
4. Keep screenshots/diagrams in the local `*.assets/` directory and reference them with relative paths.
5. Call out exam-relevant conclusions explicitly when they are the point of a section.

For **LeetCode C write-ups**:

```markdown
# lc-<id> <中文标题>

## 1 题目描述

...

## 2 题解

### 2.1 <解法名>

```C
...
```
```

C solutions should stay close to LeetCode’s C ABI:

- Use `malloc` / caller-`free` when the problem requires a returned buffer.
- Prefer `int*`, `int numsSize`, and out-params such as `returnSize` over inventing a different API.
- Keep comments sparse and in Chinese when they explain an idea, not when they narrate the code.
- Show the brute-force approach first when that is how the existing notes are structured, then add a better solution as `### 2.2`.

## What agents should and should not do

Do:

- Add or edit only the notes, solutions, or agent-config files requested.
- Preserve existing wording unless the task is to correct an error.
- When adding a problem, put it in the right topic folder (`数组/`, etc.) and update a local `readme.md` only if that folder already tracks coverage.
- Keep commits focused: notes separately from agent-config, unless the user asked for a single dump.

Do not:

- Refactor the whole tree, reformat every Markdown file, or convert notes into a blog/docs site.
- Delete or recommit large binaries such as `03-操作系统/OSTEP/OSTEP完全版.pdf` unless the user explicitly asks.
- Add Node/Python toolchains, linters, or CI “because every repo should have them” unless asked.
- Print, log, or commit secrets. GitHub access uses the `GITHUB_TOKEN` environment variable.

## GitHub and git

- Canonical remote for this copy: `https://github.com/leiiiyu/cursor.git`
- Default branch: `main`
- Prefer small, descriptive commit messages. Existing history is informal (`update`, `update OS`); new work should still be readable, e.g. `docs: add OS memory-management notes`.
- Do not force-push `main` unless the owner asked to rewrite history.
- Never copy `GITHUB_TOKEN` into files, commit messages, or command output.

For GitHub-specific procedures (issues, pull requests, `gh`, REST), load the project skill `.github/skills/github-workflow/SKILL.md`.

## Checks before finishing

There is no test suite. Before finishing a notes change:

1. Open the edited Markdown and confirm headings, fenced code, and image links still render as intended.
2. If C code was added, it should compile conceptually as a LeetCode C snippet (correct signatures, no undeclared identifiers).
3. Do not leave generated junk (`.DS_Store`, editor swap files) in the commit.
