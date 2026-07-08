---
name: verify
description: Prove a change works by driving the real behaviour end-to-end and observing it, before calling anything "done". Auto-invoke before reporting or committing any nontrivial code change that has a runtime surface — an endpoint, a CLI, a UI state, a data transform, a build, a script. Skip only for pure test/docs/comment/inert-config diffs with no behaviour to observe.
---

# verify-before-ship

Green tests and a clean typecheck are necessary, not sufficient. Verification means you drove the
actual change through the actual system and watched it do the thing. This skill makes "done" mean
**observed**, not **hoped**.

## The one rule

Before you say "done" on any change with a runtime surface, exercise that surface **this turn** and
observe the result — the behaviour, not the code.

| You changed… | So drive… | And observe… |
|---|---|---|
| an API handler | a real request to the endpoint | status + body |
| a CLI flag | the CLI with that flag | stdout / stderr + exit code |
| a UI state | the page, into that state | the rendered result |
| a data transform | a real input through it | output, diffed vs expected |
| a build step | the build | the artifact exists + is well-formed |

## Procedure

1. **Name the surface.** The observable behaviour this change should alter — a response, an exit
   code, a rendered element, a file on disk. If you can't name one, you don't yet understand the change.
2. **Establish before-state** when you can, so the delta is provable, not assumed.
3. **Drive it.** The smallest end-to-end path that exercises the *new* code. A real invocation beats a
   mock every time.
4. **Observe.** Read the actual output and compare it to the claim you're about to make.
5. **Hit an edge.** At least one boundary or failure input — not only the happy path.
6. **Record the evidence.** The exact command and the exact output. That evidence is what makes
   "done" true. If you didn't capture it, you didn't verify.

## What does NOT count as verification

- **"The tests pass."** Tests can be absent, wrong, or miss this exact path.
- **"It typechecks."** Types don't run.
- **"The file was written."** A written file is not an observed behaviour.
- **"It should work."** *Should* is a prediction, not an observation.
- **Re-reading your own diff.** Reading is not driving.

## When there is genuinely nothing to drive

If the diff is only tests, docs, comments, or inert config with no runtime effect, say so plainly and
skip — don't fabricate a run. But be honest with yourself: product source almost always has a surface.
If you think this change has none, look harder before you claim it.

## Why this exists

The most expensive bug is the one an agent confidently reported as fixed. "Done" that turns out to be
untrue costs more trust than a slow "not yet." This discipline trades a few seconds of driving the
real thing for never shipping a hollow claim.

---

*`verify-before-ship` is the free, MIT-licensed open core of **Axiom Agent OS** — the disciplined,
zero-telemetry, bring-your-own-keys engineering layer for Claude Code, Codex, and any LLM CLI. The
full engine extends this single-session discipline into a delivery gate across every deliverable
(links, files, numbers, builds), a self-improving brain, parallel/supercompute execution, and
team-wide consistency. → https://axiom.momentumfocus.org*
