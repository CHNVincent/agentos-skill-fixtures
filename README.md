# agentos-skill-fixtures

Public acceptance fixtures for AgentOS Feature 15 / ALIJ-S2F-B2.

## What this repository is

It contains **inert, prompt-only AgentOS Skill candidates** used to verify the
real GitHub intake path end to end: intent routing, the GitHub network approval,
fixed-commit resolution, archive download, candidate discovery, explicit user
selection, the external Skill content audit, and asynchronous installation.

## What this repository is NOT

- No executable or tool-type Skill.
- No scripts, binaries, or generated artifacts.
- No dependency installation (`dependencies` is empty on every manifest).
- No declared capabilities (`declared_capabilities` is empty on every manifest).
- No secrets, tokens, or credentials of any kind.
- No network access of any kind.

Each candidate is a `SKILL.md` file plus a signed `manifest.json`. The Skill
body is plain Markdown guidance text; loading it grants no capability.

## Trust boundary

Manifests are signed with a **dedicated E2E Ed25519 key**
(`key_id: agentos-b2-e2e-fixture-key-v1`). Only the public key is published
here — in [`trust/e2e-public-key.json`](trust/e2e-public-key.json).

The private key was generated locally, used once to sign these two manifests,
and then **removed from this working tree**. It is not kept in this repository,
and it will be destroyed once the signed commit is public and verified.
`.gitignore` is a convenience, not the control — the key is simply not here.

If these fixtures ever need to change, that is a **new key id with a new key**,
committed as a new commit. The key that signed this commit is never reused and
never resurrected.

The public key is injected into an isolated acceptance Trust Store
(`AGENT_OS_SCANNER_TRUST_STORE`) and **must not** enter the production trust
root. A signature that verifies here proves the signing and verification path
works; it carries no production trust.

## Repository contents

The exact published file list is [`PUBLIC-FILES.md`](PUBLIC-FILES.md). Anything
not listed there is not part of this repository.

## Immutability

Acceptance runs pin an exact 40-character commit SHA. **Published commits are
never rewritten.** Fixture changes are always a new commit, so a previously
accepted SHA keeps verifying forever.

## Layout

```
.gitignore
LICENSE
PUBLIC-FILES.md
README.md
skills/review-helper/{manifest.json,SKILL.md}
skills/report-helper/{manifest.json,SKILL.md}
trust/e2e-public-key.json
```
