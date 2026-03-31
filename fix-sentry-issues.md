---
description: Fix top-5 Sentry issues affecting the most users
agent: build
---

# Fix Sentry issues

Use `sentry` CLI to find the issues affecting most users from the latest release and keep fixing them. You can use `sentry issue list sentry/cli --sort user` to get this list (also mind there is a `--json` and accompanying `--fields` flags to get filtered JSON output). For each issue, make a plan first, execute the plan, submit a PR (not a draft), wait for CI to finish, get all unresolved comments (especially Seer and Cursor Bugbot comments), address all of them and repeat until there are no more review comments. Once you reach this state, merge the PR and move on to the next issue.

Once you fix 5 issues, you can stop. Otherwise, keep going.

Also check open PRs and recently merged commits to avoid working on errors that are already resolved or in the process of being resolved.
