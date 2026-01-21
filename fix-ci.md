---
description: Fix CI issues
agent: build
---
Keep running

```
gh run view --log-failed --job $(gh pr checks $PR_NO --json  state,link  -q '.[] | select(.state == "FAILURE").link | split("/")[-1]')'
```

to get  all failing jobs after you push and do not stop until there are no more failures.
