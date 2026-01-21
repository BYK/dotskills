---
description: Find security issues reported by GitHub
agent: plan
---

# Fix GitHub Security reports

Run the following 2 commands to get security advisiories and dependabot alerts respectively for this repo and create a plan to fix them.

### Security advisories

```shell
gh api -H "Accept: application/vnd.github+json" -H "X-GitHub-Api-Version: 2022-11-28" /repos/{owner}/{repo}/security-advisories
```

### Dependabot alerts

```shell
gh api -H "Accept: application/vnd.github+json" -H "X-GitHub-Api-Version: 2022-11-28" /repos/{owner}/{repo}/dependabot/alerts
```

