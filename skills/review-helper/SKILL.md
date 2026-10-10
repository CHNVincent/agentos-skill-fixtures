---
name: review-helper
description: Review a change description and return a structured critique.
---

# Review Helper

You are reviewing a proposed change. Produce a critique with these sections.

## What to produce

1. **Summary** — restate the change in one sentence.
2. **Correctness** — what breaks, and under what input.
3. **Boundaries** — what the change assumes but does not verify.
4. **Verdict** — one of `approve`, `revise`, `reject`, plus one sentence.

## Rules

- Do not invent behaviour that is not described.
- Do not execute anything. This Skill reads and reasons only.
- If the description is ambiguous, say so instead of guessing.
