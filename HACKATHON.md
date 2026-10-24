# FR_OS AI-Perimeter — hackathon workspace rules

This private repository is the workspace for the Meta Global AI Developer
Hackathon (2026-10-26 to 2026-11-04). It starts from FR_OS Community `main`
and keeps its history, so the work can be merged into the public repository
after the hackathon. These rules apply to every agent and person working
here, on top of [AGENTS.md](AGENTS.md). Where the two differ, this file wins
for the duration of the hackathon.

## How work is handed out
- The coordinator (Claude Code) opens one issue per work package. Work only
  on an issue that is assigned to you in its description.
- Branch: `hack/<package>-<slug>`, for example `hack/a4-conntrack-bytes`.
- One pull request per issue, based on `main`, title `<package>: <what it does>`.
- `main` is protected. Nobody pushes to it directly; the coordinator reviews
  every pull request and merges it only after the owner's "Mehet".
- The pause notice in AGENTS.md ("External contributions are paused") does
  not apply in this repository.

## What may be in this repository
- **Community code only.** No FR_OS Enterprise code, no licensing logic, no
  keys, tokens, `.env` files or real configuration. Some agents here run on
  hosted models whose providers may keep the input.
- **No compliance reporting** (NIS2, NIST, audit-trail export). That is an
  Enterprise feature (AGENTS.md, LEGAL.md section 3). The anomaly explanation
  says what happened and why; it does not map to a framework.
- Everything committed is in English.

## Design rules for the AI features
- **Local first (security-lessons G11).** The default model backend is a
  local, OpenAI-compatible endpoint. The Meta Model API is opt-in, off by
  default, and documented as a network call.
- **The model never acts.** Model output is untrusted input. It is a
  proposal that goes through `config_store.validate`, `rule_lint`, a diff the
  admin reads, `actions.try_save` and `apply_confirm`. The model service has
  no access to the apply-helper socket (security-lessons A1, I1).
- **No secrets to the model.** The model sees configuration only through
  `frfw.config.export.redacted`. It never generates passwords, ZTNA hashes or
  WireGuard private keys.
- Prefer the standard library; a new dependency follows AGENTS.md.

## Definition of done
As in AGENTS.md: tests (real sockets and processes over mocks), both test
runs green, docs updated, and a pull request description that says what was
tested and what was not.
