# Relay

> Plan once. Route intelligently. Integrate only verified work.

> **Release status:** the M6.2 candidate is not submission-ready. Its sole complete packaged live
> gate finished Sol, T001, and T002, then preserved a recoverable T003 controller-validation
> failure. No final RC4 release has been created; replay and deterministic local testing remain the
> verified free paths.

Long coding-agent tasks are expensive and difficult to trust: context grows, interrupted work is repeated, and workers can report success without evidence. Relay converts one complex request into durable bounded tasks, routes each task to the appropriate GPT-5.6 tier, and integrates only independently validated results.

## The problem

Developers need long-running coding work to survive interruption, keep contexts bounded, use frontier intelligence selectively, and produce proof stronger than a worker’s success message.

## What Relay does

Relay keeps `PLAN.md` durable while active task packets remain temporary and recoverable. Workers edit isolated Git worktrees but cannot approve, commit, merge, compact, or clean their own work. The controller validates scope, dependencies, tests, Ruff, behavioral contracts, snapshots, and integration before creating a commit.

## Three-minute overview

1. Sol produces one semantic plan; Relay freezes controller-owned contracts.
2. Terra implements the core task. Luna handles bounded tests and documentation concurrently.
3. Relay independently validates, commits, and integrates in deterministic order.
4. Verified evidence is compacted into `PLAN.md`; temporary packets disappear only after durable integration.

## Core workflow

`request → Sol plan → temporary contracts → isolated workers → controller validation → controller commits → deterministic integration → evidence export → PLAN.md-only cleanup`

## Why PLAN.md persists and task files disappear

Active packets preserve exact recovery context. After verified integration their useful outcome and evidence digest are compacted into the durable plan, preventing completed operational context from accumulating.

## GPT-5.6 model roles

- Sol: semantic planning and difficult coordination.
- Terra: bounded implementation and the single validation-triggered repair.
- Luna: clear behavioral-test and documentation tasks.
- Relay controller: exact scope, validation, commits, integration, evidence, and cleanup.

The controller—not a worker—determines acceptance.

## Verified integration model

Workers leave ordinary unstaged files. Relay derives stable snapshots, rejects scope or policy violations, runs the complete acceptance contract, and creates one attributable controller commit. Only the integration controller touches the integration branch.

## Parallel execution

The accepted graph is fixed at `T001 → {T002, T003}`. T002 and T003 use separate worktrees and bounded contexts with concurrency two. Completion order never controls Git history: T002 integrates before T003.

## Validation-triggered escalation

A controlled fault-injection drill exercised one Luna-to-Terra repair path. Luna’s natural candidate passed; Relay injected a bounded behavioral fault so the escalation path could be tested deterministically. This is not evidence that Luna naturally failed.

## Controlled benchmark result

In the controlled M5 benchmark, both the mixed-tier and all-Sol strategies passed the same acceptance suite. Under the documented Codex credit rate card, the mixed-tier worker strategy used an estimated 14.66 credits versus 36.03 credits for all-Sol, a 59.31% difference. This is a benchmark-specific estimate, not actual billing or a universal model ranking.

## Product modes

- Replay: accepted sanitized evidence; free, offline after installation, no Git mutation or credentials.
- Local: disposable deterministic lifecycle; no Codex client or model turn.
- Live: the installed package exposes the complete controlled `python-task-service` lifecycle with explicit confirmation. It runs Sol/medium planning, Terra/medium T001, parallel Luna/medium T002 and Luna/low T003, controller validation/commits, fixed integration, external evidence export, and PLAN-only cleanup. API-key mode is supported but remains offline-tested.

## Quick start

```bash
npm install --global ./relay-0.1.0-build-week.tgz
relay --help
relay demo --replay
```

## Judge test — no credentials

```bash
relay demo --replay --no-open
relay demo --local --json
```

See [docs/submission/JUDGE_TESTING.md](docs/submission/JUDGE_TESTING.md).

## Optional live test

```bash
codex login
relay demo --live --auth codex-login --confirm-live
# or, for a compatible controlled fixture:
relay run --profile python-task-service --repo /path/to/project --task-file DEMO_TASK.md --auth codex-login --confirm-live
```

The live profile consumes the tester’s selected allowance, starts at most four turns, and makes no new benchmark claim. Relay rejects unsupported repositories before authentication or model work. The sole M6.2 release gate did not reach PLAN-only completion, so live mode is not a verified judge path in the current candidate. Never place an API key in a command or file.

## Codex plugin installation

```bash
relay plugin install --yes
relay plugin status
```

Start a new Codex thread and invoke `$relay`. Uninstall with `relay plugin uninstall`.

## CLI reference

`relay --help`, `--version`, `auth status`, `doctor`, `demo --replay`, `demo --local`, `dashboard`, `run`, `status`, `evidence`, `plugin install|status|uninstall`, and `completion` form the stable product surface.

## Dashboard

The local server binds `127.0.0.1`, chooses a free port, validates state/events/PLAN/evidence against packaged schemas, exposes read-only JSON/SSE endpoints, sets a restrictive content security policy, and never uses analytics. Filesystem watching has a polling fallback; incomplete JSONL tails are ignored until complete. Replay, local, live, and recovery modes are visibly distinct. The accepted replay includes external T002/T003 evidence, escalation, benchmark, and PLAN views.

## Supported platforms

Tested: Linux x86_64, Node.js 22.23.1, Git, Python 3.11.15, pytest 9.1.1, Ruff 0.15.22, and Codex runtime 0.144.4. Replay needs only Linux x86_64 and Node.js 22. Windows, macOS, and ARM are not yet verified.

## Architecture

The TypeScript runtime owns versioned file-backed state and deterministic policies. A digest-verified packaged resource resolver locates the bundled engine, schemas, templates, sample, dashboard data, plugin, and accepted evidence without searching for a source checkout. JSON/JSONL are temporary during active work; `PLAN.md` is the successful product state. Detailed sanitized evidence lives outside the run directory.

## Security model

Relay uses bounded contexts and scopes, isolated worktrees, controller-only Git authority, explicit authentication resolution, redacted errors, loopback dashboard binding, schema-validated evidence, no telemetry, and digest-verified release artifacts. Repository and worker output are untrusted inputs.

## Evidence and reproducibility

Accepted public evidence is under `benchmarks/evidence/m4.1/`, `benchmarks/results/m5/`, `docs/evidence/`, and `examples/completed-run/`. `npm run build:replay` deterministically regenerates the judge replay from those files.

## How Codex was used to build Relay

One primary Codex thread performed most architecture, runtime, validation, Git integration, scheduler, escalation, benchmark, CLI, plugin, dashboard, packaging, tests, and release documentation work. Real GPT-5.6 Sol, Terra, and Luna turns are evidenced without publishing raw transcripts or private reasoning.

## Decisions made by the entrant

The entrant defined the product concept, durable `PLAN.md`, disposable packets, tier strategy, controller authority, evidence-before-trust principle, product positioning, benchmark boundaries, and milestone acceptance.

## Build Week development history

M0 stabilized contracts; M1 proved durability; M2 added real Sol/Terra and authentication; M3 added routed multi-task execution; M4 added bounded parallelism and evidence export; M5 added one repair escalation and the frozen comparison; M6 productized the frozen engine; M6.1 packaged the engine and production dashboard adapters; M6.2 corrected duplicate observational commands but its one live gate stopped at T003 controller validation.

## Testing

```bash
npm ci
npm run build:workspaces
npm test
npm run test:release
```

All M1–M5 regression commands remain available in `package.json`. Release tests create zero model turns.

## Current limitations

The live profile is intentionally limited to the controlled Python task-service case. Relay does not claim arbitrary repositories, learned routing, general graphs, provider retries, universal savings, production billing accuracy, Windows/macOS/ARM support, or hosted multi-user operation.

## Licence

MIT. See [LICENSE](LICENSE), [THIRD_PARTY_NOTICES.md](THIRD_PARTY_NOTICES.md), and [ASSET_PROVENANCE.md](ASSET_PROVENANCE.md).
