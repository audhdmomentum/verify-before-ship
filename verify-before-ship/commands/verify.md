---
description: Run the verify-before-ship delivery gate on your current change — drive the real behaviour and report the evidence.
allowed-tools: Bash, Read, Grep, Glob
---

You are running the **verify-before-ship** gate on the work in progress. Do not trust "it looks right."

1. Identify what changed this session — recent edits, or `git diff` / `git status` if this is a repo —
   and for each change name the observable surface it affects (an endpoint, a CLI, a UI state, a data
   transform, a build artifact, a file on disk).
2. For each surface, drive the smallest real end-to-end path and observe the actual output: call the
   endpoint, run the CLI, load the page, run the build. Prefer a real invocation over a mock.
3. Hit at least one edge or failure input, not only the happy path.
4. Report a short evidence table — one row per surface: `change → exact command run → observed output
   → matches the claim? (yes/no)`.
5. If a surface genuinely cannot be driven here, say exactly why and mark it **UNVERIFIED**. Never
   imply verification you did not perform.

End with a one-line verdict:
- **SHIP** — every surface was driven and observed to match, or
- **NOT YET** — name the failing or unverified surface and what's needed to close it.
