---
description: Address PR review comments
agent: plan
---
Address all unresolved comments from the PR by making a todo list.
Either respond to them or mark them as resolved.
Don't stop until the todo items are all done.

Use the following command to get the unresolved comments:

```
gh api graphql -F owner='<REPO_OWNER>' -F name='<REPO_NAME>' -F number=<PR_NUMBER> -f query='query($owner: String!, $name: String!, $number: Int!) { repository(owner: $owner, name: $name) { pullRequest(number: $number) { reviewThreads(first: 100) { nodes { isResolved comments(first: 100) { nodes { diffHunk body startLine line isMinimized } } } } } } }' -q '[.data.repository.pullRequest.reviewThreads.nodes[] | select(.isResolved == false) | .comments.nodes[] | select(.isMinimized == false) | {diff_hunk: .diffHunk, line: .line, start_line: .startLine, body: .body}]'
```

You'll need to replace <REPO_OWNER>, <REPO_NAME>, and <PR_NUMBER> with relevant
values for the current repo and PR. (You can probably get them by running `gh pr status` or `gh pr view`)
