---
name: buyer-criteria-skill
description: Extracts a buyer's real evaluation criteria from sales-call transcripts — in the buyer's own words, with speaker attribution — and produces a MEDDIC-style qualification summary built only from transcript evidence. Keeps stated requirements strictly separate from labeled inferences, marks qualification gaps as "not established" instead of guessing, and flags an unidentified competitor as the deal's most expensive open question. Hands its output directly to positioning-table-skill for deal-specific competitive positioning.
---

# Buyer Criteria Skill

## What This Skill Does

Turns call transcripts into the specification a competitive deal should be run against: what the buyer actually said they need, who else is in the deal, and how qualified the opportunity really is — with the gaps admitted rather than papered over.

**Key capabilities:**
- Extracts stated criteria near-verbatim, with speaker attribution and type tags
- Quarantines inferences: anything not literally stated is labeled `[inferred]` and listed separately
- Builds a MEDDIC-style qualification summary from transcript evidence only, with honest "not established" entries
- Detects and reports competitor status — named (who, by whom, in what context) or the unknown-competitor flag
- Hands off cleanly to `positioning-table-skill` once criteria and competitor are established

## When to Use This Skill

Use after any substantive buyer conversation — discovery, demo, technical review — and before positioning work. Typical requests:

- "Extract the buyer's criteria from this transcript"
- "What does this buyer actually need"
- "MEDDIC summary from these calls"
- "What did they say matters in the eval"

## Required Inputs

1. **One or more raw call transcripts** — expect real conversation-intelligence exports (Gong, Chorus, Zoom, Teams): speaker labels, timestamps, filler words, crosstalk, tangents, seller pitching. That mess is the normal input; do not ask the user to clean it. (Detailed call notes are acceptable, but say so in the output — notes are already someone's interpretation.)
2. Optional: **previously extracted criteria** for the same deal, to merge and update rather than start over.

## The Hard Rules

1. **The buyer's words are the data.** Criteria are captured near-verbatim — trimmed for length, never rewritten into vendor language. The phrasing is what the demo and collateral must echo back.
2. **Seller speech is context, never data.** Ignore everything seller-side speakers say as a source of criteria — no matter how the buyer nods along. Use seller turns for exactly one purpose: interpreting the buyer's statements (a buyer's answer means little without the question that prompted it; note that context in the attribution). What the seller pitched and the buyer merely didn't object to is not a stated criterion — polite agreement ("sure, that's nice") is not a requirement.
3. **Stated and inferred never blend.** Inference is allowed and useful ("their SSO questions suggest a security review is coming") but every inference carries an `[inferred]` label and lives in its own list. A requirement nobody stated must never look like one they did.
4. **Qualification from evidence only.** Every MEDDIC field is filled from the transcript or marked **"not established."** A qualification summary that admits its gaps is a work plan; one that looks complete is a liability.

## Procedure

1. **Identify the speakers.** Classify every speaker as buyer-side or seller-side, from labels where present or from context (who asks discovery questions, who represents the vendor). State the classification at the top of the output; if any speaker is ambiguous, say so and mark their extractions.
2. **Extract stated criteria — from buyer-side turns only.** For each: the near-verbatim statement, who said it (with timestamp when available), which call/segment, and a type tag — `technical` / `commercial` / `compliance` / `rollout` / `integration` / `support`. Where a criterion was stated in response to a seller question, note the prompting question as context. Merge duplicates across calls, keeping the strongest phrasing.
3. **Collect inferences separately.** Signals worth acting on that fall short of stated requirements — each labeled `[inferred]` with the evidence that suggests it.
4. **Build the MEDDIC-style summary** (adapt headers to the team's framework if asked):
   - **Metrics** — the numbers the buyer said would define success
   - **Economic buyer** — who owns the budget, if identified
   - **Decision criteria** — the stated criteria list, cross-referenced
   - **Decision process** — steps, dates, and approvals mentioned
   - **Identified pain** — the problem in the buyer's words
   - **Champion** — who is selling internally, if evidenced
   Each field: transcript evidence or "not established."
5. **Report competitor status.** If a competitor is named: who named it, in what context, and every mention. If none is named: lead the output with the flag — **"Unknown competitor — resolve before positioning."** An unknown competitor is the most expensive gap in a competitive deal; note any indirect hints (e.g. "we're comparing options") as `[inferred]`, but do not guess a name.
6. **Hand off.** Close by offering to feed the stated criteria and competitor into `positioning-table-skill` for the deal-specific positioning table.

## Output Format

1. **Speaker classification** — who was treated as buyer-side vs. seller-side (one line each).
2. **Competitor status** (named, or the unknown-competitor flag).
3. **Stated criteria** — numbered, each with quote, attribution (speaker + timestamp), call reference, and type tag; prompting seller question noted as context where relevant.
4. **Inferred signals** — separate list, each labeled `[inferred]` with its evidence.
5. **MEDDIC-style summary** — the six fields, evidence or "not established."
6. **Hand-off line** offering the positioning table.

Plain voice throughout: short sentences, concrete verbs, no superlatives. The output is a working document for a deal team, not a report.
