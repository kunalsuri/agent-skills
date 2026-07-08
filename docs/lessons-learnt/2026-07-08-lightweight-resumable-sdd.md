# A lightweight, resumable take on SDD

**Date:** 2026-07-08
**Applies to:** the spec → checklist → commit-per-step skill in this repo
(`resumable-sdd`, renamed from `resumable-implementation` on 2026-07-08).
**Status:** accepted.

## One-line positioning

> A lightweight, resumable take on Spec-Driven Development — for the full
> pipeline, use [GitHub Spec Kit](https://github.com/github/spec-kit).

## The problem this actually solves

The point of this skill is **not** to be a complete SDD methodology. It's to stop
work from being lost when an agent stops mid-task — because the session died, the
context window filled up, or **the agent ran out of budget/credits partway
through**. Classic SDD guarantees the spec is the source of truth. This skill adds
a second guarantee on top: *the plan and the progress are themselves committed to
git*, so any next session — a different agent, or a human — resumes from two
files, not from a transcript that may be gone.

That "don't lose an hour of work when the money runs out" property is the reason
the skill exists, and it's precisely the thing the heavyweight SDD pipelines don't
emphasise.

## Where it sits in the landscape

Three tiers, from heaviest to lightest:

1. **Full pipeline — [GitHub Spec Kit](https://github.com/github/spec-kit).**
   The de-facto reference. Seven phases
   (`constitution → specify → clarify → plan → tasks → analyze → implement`),
   30+ agents, and a real *skills mode* that installs `speckit-*` skills. IBM Bob
   and Google Antigravity both orbit it.
2. **Full SDD, our own — AI-Fication-Kit.** A separate, larger project with a
   development loop and a file/infrastructure layout built to support *full* SDD.
   That's where the complete pipeline lives.
3. **Lightweight + resumable — this skill.** One spec doc, one checklist, a
   commit after every step. Meant for **small-to-medium tasks** where the full
   Spec Kit / AI-Fication-Kit ceremony is overkill, but losing uncommitted work
   would still hurt.

So this repo is deliberately the *light* end of the spectrum. It should point
users up to Spec Kit / AI-Fication-Kit when they outgrow it, not try to become
them.

## What the recon turned up (last retrieved 2026-07-08)

Checked whether Anthropic, Google, or IBM ship a standalone, installable "SDD
skill". None do:

- **Anthropic** — no SDD skill in [anthropics/skills](https://github.com/anthropics/skills)
  (~17 skills: documents, creative/design, `skill-creator`, MCP, web-app-testing,
  enterprise comms). The repo hosts the *spec for skills*, not a *skill for specs*.
- **Google** — no downloadable skill, but **Antigravity** (Gemini CLI's successor,
  May 2026) has native SDD plus an
  [official codelab](https://codelabs.developers.google.com/codelabs/getting-started-with-spec-driven-development-in-antigravity).
- **IBM** — **Bob** has an official SDD *mode* and Skills docs; the only official
  spec-kit-style repo is [IBM/iac-spec-kit](https://github.com/IBM/iac-spec-kit)
  (infrastructure-as-code only). IBM's recommended path is Bob **+** Spec Kit.

**Conclusion:** a small, resumable SDD skill fills a real, unoccupied niche.

## What this skill deliberately does *not* do

Honest trade-offs, so nobody mistakes the light take for the full thing:

- **No separate Plan phase.** Design is folded into the spec doc; Spec Kit splits
  Specification (what) from Technical Plan (how/stack).
- **No clarification / "grill-me" step.** Spec Kit and IBM Bob interrogate you to
  harden the spec before coding; this skill just says "write the spec."
- **No constitution.** No project-wide non-negotiables artifact.
- **No spec-as-regeneration.** Spec Kit's signature move is: edit the spec →
  *regenerate* the tasks → rerun. Here, deviations are appended to the checklist,
  not regenerated from the spec.

What it adds that the heavy tools don't foreground: **resumability via
commit-per-step**, and a hard rule that a test gate's *actual evidence* (exit
code, pass count) goes in the checklist — not just the word "tested".

## Naming decision

**Do not name it `spec-driven-development`.** Reasons:

- It collides with an existing, well-known community skill of the exact same name
  ([addyosmani/agent-skills](https://github.com/addyosmani/agent-skills/blob/main/skills/spec-driven-development/SKILL.md)).
- It's generic Spec Kit territory and **overpromises** — this is the light variant,
  not the full pipeline.

Lean into the differentiator instead. Candidates that signal "SDD, but crash-safe":
`checkpointed-sdd`, `resumable-sdd`, `spec-driven-delivery`.

**Decided: `resumable-sdd`.** It maps one-to-one to the approved tagline
("a lightweight, *resumable* take on *SDD*"), keeps the differentiator up front,
stays discoverable via the SDD keyword, and avoids both the name collision and the
overpromise. Per the Agent Skills spec the `name:` frontmatter must **match the
folder name** — so the folder was renamed to `resumable-sdd` to match.

## License hygiene note

Caught during recon: the repo's `LICENSE` file was Apache-2.0 while the README and
`SKILL.md` frontmatter both declared MIT. **Resolved 2026-07-08: standardised on
Apache-2.0** — kept the existing `LICENSE` file, and fixed the README and the
`SKILL.md` frontmatter `license:` field to match. Lesson: whatever the license,
keep all three in sync — the `LICENSE` file, the README section, and the skill
frontmatter `license:` field. A skill is distributed standalone, so its frontmatter
license travels with it and must be correct on its own.
