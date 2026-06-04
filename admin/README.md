# Studio Admin panel

Private operations dashboard for the AI Automation Studio.

**URL:** https://antonsemenovser.github.io/ai-automation-studio-site/admin/

Single static page (no server). It talks to the GitHub API **from your browser**, under
a personal token you paste once — the token is stored only in this browser's localStorage
and is sent only to `github.com`. The page is `noindex` and useless without the token.

## What it shows
- **Процессы** — last run status (success / fail / running) + next scheduled run for each of
  the three automations (channel poster, lead radar, site feed), with **▶ Run now** and a
  link to the run logs.
- **Лента сайта** — current `feed.json` (count, updated, latest items). Public, no token.
- **Активность** — the last ~12 workflow runs across all three, newest first.
- **Лиды** — placeholder until the bot publishes its CRM stats here (next step); full lead
  detail stays in the Telegram bot (`/panel`, `/leads`).

## Setup (one time, on Anton's phone/PC)
1. Create a **fine-grained PAT**: https://github.com/settings/personal-access-tokens/new
2. Resource owner `antonsemenovser`; Repositories → `ai-automation-studio` + `ai-automation-studio-site`.
3. Permissions → **Actions: Read and write**, **Contents: Read**.
4. Open the panel → 🔑 Токен → paste → Save.

## Control
The **▶ Run now** buttons fire each workflow's `workflow_dispatch` — i.e. post to the channel,
scan for leads, or refresh the site on demand, from anywhere, with the laptop off.
