---
name: github-workflow
description: Operate on the leiiiyu/cursor GitHub repository—create and update issues, pull requests, releases, and remote git history using GITHUB_TOKEN. Use when the user asks to push, open a PR, manage issues, inspect Actions, or otherwise talk to GitHub.
license: MIT
metadata:
  author: leiiiyu
  version: "1.0"
  repo: leiiiyu/cursor
---

# GitHub workflow for leiiiyu/cursor

Use this skill whenever the task touches GitHub itself rather than only local Markdown/C notes.

## Auth

- Read credentials from the `GITHUB_TOKEN` environment variable. Do not read tokens out of shell history, screenshots, or committed files.
- Prefer the GitHub REST/GraphQL API or `gh` with that token. Example (never print the token):

  ```bash
  curl -sS \
    -H "Authorization: Bearer ${GITHUB_TOKEN}" \
    -H "Accept: application/vnd.github+json" \
    -H "X-GitHub-Api-Version: 2022-11-28" \
    https://api.github.com/repos/leiiiyu/cursor
  ```

- If `gh` is available, `gh auth status` should show the token’s account. Use `GH_TOKEN`/`GITHUB_TOKEN` as already provided; do not run `gh auth login`.
- Redact tokens in logs, commit messages, git remotes written to disk, and chat replies. If a remote URL would embed the token, pass it only as a one-off push URL or via `http.extraheader`, then do not leave it in `.git/config`.

## Repository facts

| Item | Value |
| --- | --- |
| Owner/name | `leiiiyu/cursor` |
| URL | https://github.com/leiiiyu/cursor |
| Default branch | `main` |
| Visibility | public |
| Content | 408 CS exam Markdown notes (see `AGENTS.md`) |

This GitHub copy may exist alongside other clones (for example `leiiiyu/408`). Unless the user names another remote, **push and open PRs against `leiiiyu/cursor`**.

## Push

1. Confirm `git status` and that the commit is only the files the user asked for.
2. Push `main` to `https://github.com/leiiiyu/cursor.git` when they asked to publish to this repo.
3. Do not force-push `main` unless they explicitly asked to rewrite history.
4. Do not push these notes to a different repository just because `origin` still points somewhere else. Add or use a `cursor` remote, or push by URL.

## Issues

Open issues only when the user wants tracking (missing subjects, wrong solutions, scanning TODOs). Title in Chinese, body with:

- What is wrong or missing
- Path to the note (`03-操作系统/一轮笔记/...`)
- Suggested next step

Labels are optional; do not invent a label taxonomy unless one already exists on the repo.

## Pull requests

This repo often receives direct commits to `main`. Open a pull request when the user wants review, or when changing agent config (`AGENTS.md`, `CLAUDE.md`, `.cursor/skills/**`) together with a large notes edit.

PR title: short, imperative, Chinese or English is fine (`docs: add github workflow skill`).

PR body:

- What changed
- Which notes or skills to review
- Confirmation that `GITHUB_TOKEN` was not committed

## Actions and releases

There is no required CI. Do not add workflows “for completeness.” If a workflow later exists and fails, inspect the run with the GitHub API (`/repos/leiiiyu/cursor/actions/runs`) and summarize the failed job, then fix the YAML or the notes script it ran.

Create a GitHub Release only when the user asks (for example a 408 review milestone). Tag `vYYYY.MM` or a milestone name they choose; do not tag every notes commit.

## Safety

- Never grant the token to untrusted scripts from the web.
- Never commit `.env`, `gh` host configs, or files that contain `ghp_` / `gho_` / `github_pat_` prefixes.
- After a successful API call, report the human URL (`https://github.com/leiiiyu/cursor/...`) rather than raw JSON dumps, unless the user asked for the payload.
