# verify-before-ship

**Make your coding agent prove a change works — drive the real behaviour and observe it — before it's
allowed to say "done."**

A tiny, zero-telemetry Claude Code plugin. It adds one discipline: green tests and a clean typecheck
are necessary, not sufficient — verification means the agent drove the actual change through the
actual system and watched it do the thing. "Done" comes to mean **observed**, not **hoped**.

## Why

The most expensive bug is the one your agent confidently reported as fixed. A slow "not yet" costs
less trust than a fast "done" that turns out to be untrue. This plugin trades a few seconds of driving
the real thing for never shipping a hollow claim.

## What you get

- **A `verify` skill** that auto-invokes before the agent reports or commits any change with a runtime
  surface (an endpoint, a CLI, a UI state, a data transform, a build). It makes the agent name the
  surface, drive the smallest real end-to-end path, hit an edge case, and record the exact command +
  output as evidence.
- **A `/verify` command** you can run on demand against your current change — it drives each surface
  and hands back an evidence table plus a one-line **SHIP / NOT YET** verdict.

No network calls. No telemetry. No account. It reads and runs your code locally, nothing leaves your
machine.

## Install

From inside Claude Code:

```
/plugin marketplace add audhdmomentum/verify-before-ship
/plugin install verify-before-ship@axiom-open-core
```

Once installed, the `verify` skill is discovered automatically and `/verify` is available as a command.

## Use

- **Automatic** — just work. Before the agent calls a change "done," the skill kicks in and makes it
  drive the real behaviour first.
- **On demand** — run `/verify` after a chunk of work to get an evidence table and a SHIP / NOT YET
  verdict on what you've changed.

## What counts, and what doesn't

Verification is: you drove the new code end-to-end and read the real output. It is **not**: "the tests
pass," "it typechecks," "the file was written," "it should work," or re-reading your own diff. If the
diff is genuinely inert (pure tests/docs/comments/config with no runtime effect), the skill says so and
skips — it won't fabricate a run.

## The bigger picture

`verify-before-ship` is the free, MIT-licensed **open core** of [**Axiom Agent
OS**](https://axiom.momentumfocus.org) — a disciplined, zero-telemetry, bring-your-own-keys
engineering layer for Claude Code, Codex, and any LLM CLI. Axiom Agent OS extends this single-session
discipline into a full delivery gate across every deliverable (links, files, numbers, builds), a
self-improving brain, parallel/supercompute execution, and team-wide consistency.

This plugin stands alone and always will. If it earns a place in your workflow, the full engine is
there when you want more.

## License

MIT — see [LICENSE](./LICENSE). Built by [Momentum Focus](https://axiom.momentumfocus.org).
