# Public file whitelist — the exact contents of this repository

This is the authoritative list. Any file NOT listed here must not be published.

| # | Path | Purpose | Sensitive? |
|---|---|---|---|
| 1 | `.gitignore` | Excludes local build/audit tooling and the E2E signing key directory | No |
| 2 | `LICENSE` | MIT license text | No |
| 3 | `PUBLIC-FILES.md` | This whitelist — the authoritative published-file list | No |
| 4 | `README.md` | What this repository is / is not, trust boundary, immutability policy | No |
| 5 | `trust/e2e-public-key.json` | **Ed25519 PUBLIC key only** — required so acceptance runs can build an isolated trust store | No (public key is public by definition) |
| 6 | `skills/review-helper/manifest.json` | Signed `external-skill-manifest-v1` manifest | No |
| 7 | `skills/review-helper/SKILL.md` | Inert prompt-only Skill body (Markdown guidance text) | No |
| 8 | `skills/report-helper/manifest.json` | Signed `external-skill-manifest-v1` manifest | No |
| 9 | `skills/report-helper/SKILL.md` | Inert prompt-only Skill body (Markdown guidance text) | No |

**9 files total.**

## Never published

| Path | Why |
|---|---|
| `.e2e-signing-key/**` | The Ed25519 **private** key. Generated locally, used once to sign, then evacuated out of this working tree and destroyed. `.gitignore` is a convenience, not the control — the key is not kept here at all. |
| `_build_fixture.py` | Local generator that produced the signed manifests. |
| `_audit_fixture.py` | Local audit harness that runs the product's real verification chain. |
| `_evacuate_key.py` | Local one-shot key evacuation utility. |
| `_check_whitelist.py` | Local gate that proves this document and the repository agree. |
| `PUSH-INSTRUCTIONS.md` | Local operator runbook for creating and publishing the remote. Not part of the published fixture content. |

## Invariants a reviewer can re-check

1. `git ls-files` returns **exactly** the 9 paths above — no more, no fewer.
2. No tracked file carries a PEM private-key block, and no `.pem` file is
   tracked. (This document deliberately contains no such block, so the check
   below is clean.)
3. `trust/e2e-public-key.json` contains a raw 32-byte **public** key and the
   base64 of that same key; both must equal the key derived from the signing
   key that produced the manifests.
4. Every `manifest.json` has `dependencies: []` and `declared_capabilities: []`,
   `entrypoint` ending in `.md`, and no path pointing outside its own directory.
5. The archive contains no `.py` / `.sh` / `.exe` / `.js` / `.ps1` / `.bat` /
   `.pem` entry.
