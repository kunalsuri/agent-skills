# agent-skills

Personal collection of [Agent Skills](https://agentskills.io/specification)
— self-contained `SKILL.md` folders that work across Claude Code, OpenAI Codex,
GitHub Copilot, Cursor, and Google Antigravity (formerly Gemini CLI). One skill,
one folder, no per-tool forks: every tool in the install table reads the same
file.

## Skills

| Skill | What it does |
|---|---|
| [`resumable-sdd`](./resumable-sdd/SKILL.md) | A **lightweight, resumable take on spec-driven development (SDD)**: spec doc → checklist → implement/test/commit/check-off, one item at a time, with the plan *and* the progress committed to git. Survives the agent stopping mid-task — session death, context overflow, or running out of budget — so no work is lost. |

## Where this fits

`resumable-sdd` is deliberately the **light end** of the SDD spectrum. It is not
trying to be a full methodology — it's for small-to-medium tasks where the full
ceremony is overkill but losing an hour of uncommitted work would still hurt.

- **Full pipeline →** [GitHub Spec Kit](https://github.com/github/spec-kit), the
  de-facto reference (7 phases, 30+ agents, a `speckit-*` skills mode).
- **Full SDD, in-house →** *AI-Fication-Kit* (a separate, larger project with a
  development loop built for complete SDD).
- **Lightweight + resumable →** this skill.

The reasoning, recon, and decisions behind this positioning live in
[`docs/lessons-learnt/`](./docs/lessons-learnt/README.md).

## What's new *(last retrieved 2026-07-08)*

- **Agent Skills is an open standard.** Anthropic published the
  [Agent Skills spec](https://agentskills.io/specification) on **18 Dec 2025**;
  it's now stewarded by the Linux Foundation's **Agentic AI Foundation**. The
  spec is still **draft**, with **v1.0 targeted for 2H 2026**, so the frontmatter
  surface may still shift. Supported across Claude Code, OpenAI Codex CLI, Google
  Antigravity/Gemini CLI, GitHub Copilot, Cursor, and ~40 other clients; the most
  active registry is [skills.sh](https://skills.sh) (Vercel).
- **Spec detail authors should know:** the `name` field must now **match the
  parent directory name**, may not contain consecutive hyphens, and the spec
  recommends keeping `SKILL.md` **under ~500 lines / 5k tokens**, moving detail
  into `references/`.
- **`AGENTS.md` is the sibling standard**, under the same foundation —
  **60,000+ projects, 20+ tools** as of Dec 2025. It's the *project-context* file
  (build/test/style/architecture) to Skills' *portable-capability* folder;
  they're complementary, not competing.
- **Spec-Driven Development landscape:** no vendor ships a standalone installable
  SDD *skill* today. [GitHub Spec Kit](https://github.com/github/spec-kit) is the
  reference (and has a skills mode); **Google Antigravity** has native SDD plus an
  [official codelab](https://codelabs.developers.google.com/codelabs/getting-started-with-spec-driven-development-in-antigravity);
  **IBM Bob** ships an official SDD *mode* ([IBM/iac-spec-kit](https://github.com/IBM/iac-spec-kit)
  covers infrastructure-as-code). That's the gap `resumable-sdd` fills at the
  lightweight end.
- **Tooling note:** Google folded **Gemini CLI into Antigravity CLI** (May 2026);
  it keeps Agent Skills, hooks, and subagents.

## Install

Pick whichever matches your tool. All of them just need the skill's folder
placed somewhere your tool looks for skills.

**Any tool, via the `npx skills` installer** (installs to `~/.agents/skills`,
picked up by Gemini CLI and others):
```bash
npx skills install github.com/kunalsuri/agent-skills
```

**Claude Code:**
```bash
# project-local
cp -r resumable-sdd .claude/skills/
# or personal, available in every project
cp -r resumable-sdd ~/.claude/skills/
```

**GitHub Copilot (VS Code):**
```bash
cp -r resumable-sdd .github/skills/
```

**Cursor:**
```bash
cp -r resumable-sdd .cursor/skills/
```

**Antigravity:**
```bash
cp -r resumable-sdd ~/.gemini/config/skills/
```

**Gemini CLI:**
```bash
cp -r resumable-sdd ~/.gemini/skills/
```

**GitHub CLI** (public preview as of `gh` v2.90, April 2026 — installs,
pins to a tag/commit, and tracks provenance in the frontmatter):
```bash
gh skill install kunalsuri/agent-skills/resumable-sdd
```

Skills aren't verified by any of these tools — read a `SKILL.md` before
installing it, same as you would a shell script from the internet.

## Format

Every skill here follows the current open [Agent Skills specification](https://agentskills.io/specification):
YAML frontmatter (`name`, `description` required; `license`, `metadata`,
`compatibility`, `allowed-tools` optional) followed by Markdown instructions.
`name` is lowercase-hyphen, ≤64 chars, must **match the folder name**, and must
not contain leading/trailing/consecutive hyphens. `description` is ≤1024 chars
and must say both *what* the skill does and *when* to use it, since that's what
drives a tool's automatic skill selection. Keep the body under ~500 lines and
push detail into `references/`.

## License

[Apache License 2.0](./LICENSE) — Copyright © 2026 Kunal Suri. Covers the skill
content in this repo, not any upstream tooling.
