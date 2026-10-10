# Inspecting GitHub checks

Use these as examples, not as commands to run without identifying the target and understanding scope. Prefer an existing connector when it exposes the needed run/job/log data. Do not install or authenticate tools automatically.

With an already available GitHub CLI:

```sh
gh auth status
gh pr view <pr> --repo <owner/repo> --json number,url,headRefOid,statusCheckRollup
gh pr checks <pr> --repo <owner/repo> --json name,state,bucket,link
gh run view <run-id> --repo <owner/repo> --json headSha,attempt,status,conclusion,jobs,url
gh run view <run-id> --repo <owner/repo> --attempt <attempt> --log-failed
```

Validate supported flags/fields with the installed command's help when needed. Check JSON output for the head and attempt before associating a failure with the current checkout. A pending job may not have complete logs; report that instead of fabricating a failure. The `gh pr checks` command may exit nonzero because checks failed or remain pending; inspect its output before diagnosing CLI malfunction.

Use the observed attempt for log retrieval so a concurrent rerun does not silently change the evidence. Current CLI documentation lists exit code 8 for pending checks; confirm behavior against the installed version when classifying a nonzero exit.

A whole run's final error can hide the first failure. Inspect the specific failed job/step and its log context. When logs are unavailable due to access or retention, request the relevant supplied excerpt or authenticated read capability. Do not recommend broad token scopes by default.

Keep three distinct evidence records when relevant:

| Evidence | What it can establish |
| --- | --- |
| Supplied logs | What the provided run/transcript reports; provenance may be incomplete |
| Local reproduction | Behavior in the inspected checkout/environment |
| Remote completed check | Result for the verified head, run, and attempt |

For workflow reruns, inspect all reachable jobs for deployment, publishing, secrets, and external mutations first. A fix request is not blanket authorization for those effects. Never upload private source or logs to a new service to debug a check.

Official references:

- [gh pr checks](https://cli.github.com/manual/gh_pr_checks)
- [gh run view](https://cli.github.com/manual/gh_run_view)
- [GitHub Actions logs](https://docs.github.com/en/actions/monitoring-and-troubleshooting-workflows/using-workflow-run-logs)

Design reference: [OpenAI gh-fix-ci](https://github.com/openai/skills/blob/main/skills/.curated/gh-fix-ci/SKILL.md). This adaptation supports source-bounded offline diagnosis and respects already granted authorization rather than requiring redundant confirmations.
