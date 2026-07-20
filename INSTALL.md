# Judge testing

## Path 1 — Instant replay, no credentials

```bash
npm install -g ./relay-0.1.0-build-week.tgz
relay demo --replay
```

The dashboard identifies recorded accepted evidence, offers the Judge Tour, and shows the controlled benchmark. It makes zero model calls.

## Path 2 — Deterministic lifecycle, no credentials

```bash
relay demo --local
```

Relay creates a temporary Git project, executes deterministic task changes and controller commits, compacts the result, and leaves only `PLAN.md` in its run directory. This proves lifecycle wiring, not GPT-5.6 quality.

## Path 3 — Optional complete controlled GPT-5.6 lifecycle

Current release status: this path passed from the installed source-free package with Codex login.
It completed exactly one Sol/medium, Terra/medium, Luna/medium, and Luna/low turn with no retry,
then finalized to PLAN-only state. Judges do not need this paid path; replay and local remain the
recommended free tests.

```bash
codex login
relay demo --live --auth codex-login --confirm-live
```

This copies the bundled compatible TaskService fixture, verifies the packaged resource attestation,
and requests exactly Sol/medium → Terra/medium → parallel Luna/medium and Luna/low. The controller
validates, commits, integrates T002 before T003, exports three evidence bundles, and finishes
PLAN-only. It starts at most four turns and consumes the tester’s allowance.

The accepted release run recorded 33,947 ms of T002/T003 overlap, all seven T002 mutants, all seven
T003 documentation requirements, three controller commits/integrations/ledgers/markers, one
completion digest, final pytest and Ruff, dashboard completion, and exit 0.

API-key selection uses `--auth api-key` with `OPENAI_API_KEY` set in the environment. It is supported and offline-tested but was not live-tested for this release. Never paste a key into a command or file. Live mode is optional for judging.

Inspect an active, recovery, or completed run with:

```bash
relay dashboard --run <run-directory-or-PLAN.md> --evidence-root <evidence-directory>
```

The browser can select only validated evidence identifiers indexed by the server; it cannot request arbitrary paths.

Public dashboard payloads contain logical artifact references and deterministic path digests, not
private absolute source, worktree, validation, evidence, executable, package, or temporary paths.
CLI exit status is 0 on success, 1 on failure, 2 on a recoverable blocked run, 3 on interruption, and
64 on invalid usage.
