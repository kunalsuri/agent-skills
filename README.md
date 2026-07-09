<div align="center">

# 🧩 agent-skills

**Portable, cross-tool Agent Skills — one folder, every agent.**

Self-contained [`SKILL.md`](https://agentskills.io/specification) packages that
run unchanged across Claude Code, OpenAI Codex, GitHub Copilot, Cursor, and Google
Antigravity. No per-tool forks. Write once, run in every agent.

[![License: Apache 2.0](https://img.shields.io/badge/license-Apache--2.0-blue.svg)](./LICENSE)
[![Spec: Agent Skills](https://img.shields.io/badge/spec-Agent%20Skills-8A2BE2.svg)](https://agentskills.io/specification)
[![Skills: 1](https://img.shields.io/badge/skills-1-brightgreen.svg)](#-skills)
[![Works with](https://img.shields.io/badge/works%20with-Claude%20Code%20·%20Codex%20·%20Copilot%20·%20Cursor%20·%20Antigravity-111.svg)](#-install)

</div>

> **One skill, one folder, no forks.** Every tool in the install table reads the
> exact same file — because Agent Skills is now an [open standard](https://agentskills.io/specification),
> not a vendor feature.

<br>

---

## 📐 More Info: Agent Skill - Format & Specifications

<br>

> [!TIP]
> **Agent Skills** is an open format maintained by **Anthropic** and open to contributions from the community.

<br>

Every skill follows the open [Agent Skills specification](https://agentskills.io/specification):
YAML frontmatter (`name`, `description` required; `license`, `metadata`,
`compatibility`, `allowed-tools` optional) followed by Markdown instructions.

- `name` — lowercase-hyphen, ≤64 chars, must **match the folder name**, no
  leading/trailing/consecutive hyphens.
- `description` — ≤1024 chars; must say both *what* the skill does and *when* to
  use it (that's what drives an agent's automatic skill selection).
- Keep the body under ~500 lines; move detail into `references/`.

<br>

---

## 🎯 Goal

Agents are only as good as the procedural knowledge you can hand them — and today
that knowledge is trapped in tool-specific formats, copied and re-pasted per
project, and lost the moment a session ends. This repo takes the opposite bet:

**Package capability once, as a portable `SKILL.md`, and make it durable.**

Concretely, that means each skill here is:

- 🔌 **Portable** — the same folder drops into Claude Code, Codex, Copilot,
  Cursor, or Antigravity. No rewrites, no adapters.
- 🧠 **Progressive** — an agent loads only the skill's name + description at
  startup (~100 tokens), then pulls in the full instructions *only when your task
  matches*. Cheap to have installed, powerful when triggered.

<br>

> [!TIP]
> **Example: How [`resumable-sdd`](#-skills) Skill Will Helps You?** Click the Button Below to View Details:

<details>
<summary><b>💾 Durable Execution using 'resumable-sdd' </b> 🔽</summary>

<br>

[`resumable-sdd`](#-skills), commits the *plan and the progress* to git, so an interrupted task (e.g. due to an event such as LLM Token Quota Over) resumes by reading two files instead of a lost transcript. 
It's deliberately the **light end** of the SDD spectrum — for small-to-medium tasks where the full ceremony is overkill but losing an hour of uncommitted work would still hurt.

<br>

| Without a skill | With these skills |
|---|---|
| Re-explaining the same workflow to your agent every session | The agent already knows it — it's installed |
| A long task dies at 90% and you start over | Resume from the last committed step |
| A different tool means a different config | One folder works everywhere |
| "It ran out of credits mid-task and lost everything" | The plan + progress are on disk, in git |

<br>

### 🧭 Things related to `resumable-sdd`?

```
1. Heavier Skill File                              ┃  GitHub Spec Kit      full 7-phase pipeline, 30+ agents, skills mode        |  [Developed by 3rd Party]

2. Methodology & underlying Infa to support SDD    ┃  AI-Fication-Kit      my own full-SDD project + dev loop                    |  [Developed by Kunal Suri (CEA LIST)]

3. Lighter Skill File                              ┃  resumable-sdd  ◀──    this repo: one spec, one checklist, commit-per-step  | [Developed in this Repo by Kunal Suri (CEA LIST)]
```

<br>

- **Full pipeline →** [GitHub Spec Kit](https://github.com/github/spec-kit)
- **Full SDD, in-house →** *AI-Fication-Kit* (a larger project with a dev loop
  built for complete SDD)
- **Lightweight + resumable →** this skill

<br>

The reasoning, recon, and decisions behind this positioning live in
[`docs/lessons-learnt/`](./docs/lessons-learnt/README.md).

</details>

<br>

---


## 📦 List of Skills in this Repo

| Skill | What it does |
|---|---|
| [`resumable-sdd`](./resumable-sdd/SKILL.md) | A **lightweight, resumable take on spec-driven development (SDD)**: spec doc → checklist → implement/test/commit/check-off, one item at a time, with the plan *and* the progress committed to git. Survives the agent stopping mid-task — session death, context overflow, or running out of budget — so no work is lost. |

<br>

---

## ⚡ Install

Pick whichever matches your tool — each just needs the skill's folder placed where
your tool looks for skills.

**Any tool, via the `npx skills` installer** (installs to `~/.agents/skills`):
```bash
npx skills install github.com/kunalsuri/agent-skills
```

<details>
<summary><b>Per-tool copy commands</b> (Claude Code, Copilot, Cursor, Antigravity, Gemini CLI)</summary>

```bash
# Claude Code — project-local, or ~/.claude/skills for every project
cp -r resumable-sdd .claude/skills/
cp -r resumable-sdd ~/.claude/skills/

# GitHub Copilot (VS Code)
cp -r resumable-sdd .github/skills/

# Cursor
cp -r resumable-sdd .cursor/skills/

# Antigravity
cp -r resumable-sdd ~/.gemini/config/skills/

# Gemini CLI
cp -r resumable-sdd ~/.gemini/skills/
```

</details>

<br>

**GitHub CLI** (public preview as of `gh` v2.90, April 2026 — installs, pins to a
tag/commit, and tracks provenance in the frontmatter):

```bash
gh skill install kunalsuri/agent-skills/resumable-sdd
```

<br>

> ⚠️ Skills aren't verified by any of these tools — read a `SKILL.md` before
> installing it, same as you would a shell script from the internet.

<br>

---

## NOTE: 🗂️ This Work is Part of another Effort — SkillDeck

This repo is a set of *hand-crafted* / *human-verified* skills. It feeds into a broader project:

### [**SkillDeck**](https://github.com/kunalsuri/SkillDeck) — a cross-company knowledge-base for AI agent skills

<br>

> A modern directory and knowledge base designed to **catalog, cluster, and
> verify** AI agent skills, workflows, and tools.

<br>

If `agent-skills` is the workbench, **SkillDeck is the library** — the place all of
this cross-company skill knowledge is gathered, quality-checked, and made
executable. → **[Explore SkillDeck](https://github.com/kunalsuri/SkillDeck)**

<br>

---

## 📰 What's new? Latest on Agent Skills · *last retrieved 2026-07-08*

- **Agent Skills is an open standard.** Anthropic published the
  [spec](https://agentskills.io/specification) on **18 Dec 2025**; it's now
  stewarded by the Linux Foundation's **Agentic AI Foundation**. Still **draft**,
  with **v1.0 targeted for 2H 2026**, so the frontmatter surface may shift.
  Supported across Claude Code, OpenAI Codex CLI, Google Antigravity/Gemini CLI,
  GitHub Copilot, Cursor, and ~40 other clients; busiest registry is
  [skills.sh](https://skills.sh) (Vercel).
  
- **Authoring rule to know:** `name` must now **match the parent directory name**,
  can't contain consecutive hyphens, and the spec recommends keeping `SKILL.md`
  **under ~500 lines / 5k tokens** (push detail into `references/`).
- **`AGENTS.md` is the sibling standard** — same foundation, **60,000+ projects,
  20+ tools** (Dec 2025). It's the *project-context* file (build/test/style) to
  Skills' *portable-capability* folder; complementary, not competing.
  
- **SDD landscape:** no vendor ships a standalone installable SDD *skill* today.
  [Spec Kit](https://github.com/github/spec-kit) is the reference (with a skills
  mode); **Google Antigravity** has native SDD + an
  [official codelab](https://codelabs.developers.google.com/codelabs/getting-started-with-spec-driven-development-in-antigravity);
  **IBM Bob** ships an SDD *mode* ([IBM/iac-spec-kit](https://github.com/IBM/iac-spec-kit)
  covers infrastructure-as-code). `resumable-sdd` fills the lightweight gap.
  
- **Tooling:** Google folded **Gemini CLI into Antigravity CLI** (May 2026); it
  keeps Agent Skills, hooks, and subagents.

<br>

---

## 📄 Acknowledgments & License

**Author**: Kunal Suri ([@kunalsuri](https://github.com/kunalsuri)) (CEA LIST)

The **Agent-Skills** project is open source and licensed under the [Apache License 2.0](LICENSE) — Copyright © 2026 Kunal Suri (CEA LIST). See the LICENSE file for the full license text.

**Warranty & Liability Notice**: This software is provided under the Apache License 2.0 on an "AS IS" basis, without warranties or conditions of any kind, either express or implied. To the extent permitted by the license and applicable law, the authors and contributors disclaim warranties and limit liability. Please refer to the LICENSE file for the complete terms, including Sections 7 (Disclaimer of Warranty) and 8 (Limitation of Liability).
