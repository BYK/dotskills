---
description: Iterate on PR
agent: build
---

Keep running

```
gh run view --log-failed --job $(gh pr checks $PR_NO --json  state,link  -q '.[] | select(.state == "FAILURE").link | split("/")[-1]')'
```

to get  all failing jobs after you push.
Make sure to wait for "Sentry Seer" and "Cursor BugBot" jobs to finish.
Fix any failing jobs.
Address all unresolved comments (both from bots and humans) from the PR by making a todo list.
When you address each PR, either respond to them or mark them as resolved.
Don't stop until the todo items are all done.
Keep repeating this cycle until there are no more CI failures nor unresolved comments from humans or bots.

Use the following command to get the unresolved comments:

```
gh api graphql -F owner='<REPO_OWNER>' -F name='<REPO_NAME>' -F number=<PR_NUMBER> -f query='query($owner: String!, $name: String!, $number: Int!) { repository(owner: $owner, name: $name) { pullRequest(number: $number) { reviewThreads(first: 100) { nodes { isResolved comments(first: 100) { nodes { diffHunk body startLine line isMinimized } } } } } } }' -q '[.data.repository.pullRequest.reviewThreads.nodes[] | select(.isResolved == false) | .comments.nodes[] | select(.isMinimized == false) | {diff_hunk: .diffHunk, line: .line, start_line: .startLine, body: .body}]'
```

You'll need to replace <REPO_OWNER>, <REPO_NAME>, and <PR_NUMBER> with relevant
values for the current repo and PR. (You can probably get them by running `gh pr status` or `gh pr view`)
