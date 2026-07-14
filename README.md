# Buyer Criteria Skill

A Claude skill that extracts a buyer's **real evaluation criteria** from raw sales-call transcripts — Gong, Chorus, or Zoom exports, mess included — in the buyer's own words, with speaker and timestamp attribution, plus a MEDDIC-style qualification summary built only from transcript evidence. Seller speech is **context, never data**: it is used only to interpret the buyer's statements, so vendor pitching can't leak into the requirements. Stated requirements stay strictly separate from labeled inferences, qualification gaps are admitted as "not established," and an unidentified competitor is flagged as the deal's most expensive open question.

Distilled from the account-intelligence and MEDDIC-analysis agents [Daniel Glickman](https://www.cmoconfessions.com) built and ran in production.

## What it does

- Works on **raw conversation-intelligence exports** (Gong, Chorus, Zoom, Teams) — timestamps, filler, crosstalk, and all; no cleanup needed
- **Ignores seller-side speech as data** — vendor claims and pitches never become "requirements," even when the buyer politely nods along; seller questions are kept only as context for the buyer's answers
- Extracts **stated criteria** near-verbatim, attributed with speaker and timestamp, tagged by type (technical, commercial, compliance, rollout, integration, support)
- Quarantines **inferences** — anything not literally stated is labeled `[inferred]`, in its own list
- Builds a **MEDDIC-style summary** from evidence only, with honest "not established" entries (adapt the headers if you run MEDDPICC or another framework)
- Reports **competitor status** — named (who, by whom, in what context) or the **unknown-competitor flag**
- Hands off to [`positioning-table-skill`](https://github.com/msdanyg/positioning-table-skill) for the deal-specific positioning table

## Why the separation matters

The gap between what the customer said matters and what your company wants to pitch is where deals are lost. This skill exists to keep that line hard: the buyer's phrasing is the specification, inferences are labeled speculation, and a qualification doc that admits its gaps is a work plan — one that looks complete is a liability.

## When it triggers

Phrases like:

- "Extract the buyer's criteria from this transcript"
- "What does this buyer actually need"
- "MEDDIC summary from these calls"
- "What did they say matters in the eval"

## Installation

### Option A — Install the skill folder (Claude Code)

Copy the skill folder into your Claude skills directory:

```bash
# Personal (all projects)
cp -r buyer-criteria-skill ~/.claude/skills/

# Or project-scoped
cp -r buyer-criteria-skill /path/to/project/.claude/skills/
```

Restart Claude Code (or start a new session) and the skill will be available.

### Option B — Use the packaged `.skill` file

Download [`buyer-criteria-skill.skill`](./buyer-criteria-skill.skill) and upload it wherever packaged skills are accepted (e.g. Claude.ai skill upload).

## Usage

Paste one or more transcripts and ask:

> Extract the buyer's criteria from these calls and give me the MEDDIC summary.

See [`examples/`](./examples) for a worked input and output (invented, illustrative data) — the example chains into the [`positioning-table-skill`](https://github.com/msdanyg/positioning-table-skill) example, so you can follow one invented deal through both skills.

## Repository contents

- [`buyer-criteria-skill/SKILL.md`](./buyer-criteria-skill/SKILL.md) — the skill
- [`examples/`](./examples) — worked example (illustrative, invented data)
- [`buyer-criteria-skill.skill`](./buyer-criteria-skill.skill) — packaged for upload

## Part of the PMM Skill Stack

One of four free Claude Skills for product marketers: [cmoconfessions.com/skills](https://www.cmoconfessions.com/skills). The method behind the stack: [Kill the Battle Card](https://www.cmoconfessions.com/method).
