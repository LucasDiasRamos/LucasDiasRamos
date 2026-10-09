# Visual GitHub metrics — setup guide

This profile uses [lowlighter/metrics](https://github.com/lowlighter/metrics) to generate visual cards from public GitHub activity.

## Security and privacy

- The workflow reads GitHub information using a **personal access token** (PAT). Create one with **no additional scopes** for these public-only metrics. The upstream project documents this requirement: a repository-scoped `GITHUB_TOKEN` cannot replace it for all user metrics.
- Never paste a PAT into the README, GitHub issue, pull request, source code or chat. Use a GitHub Actions repository secret named `METRICS_TOKEN`.
- Private repository access is **not** needed and should not be granted for this public portfolio.
- The workflow uses `plugin_activity_visibility: public` to limit the activity feed to publicly visible events.
- GitHub's automatically supplied `github.token` is used by the action to commit generated images. The workflow grants `contents: write` for those commits.
- Review third-party GitHub Actions before use. The workflow currently follows upstream's `@latest` stable tag; for stronger supply-chain controls, pin to a reviewed commit SHA and update deliberately.

## Activate

1. In GitHub, open `LucasDiasRamos/LucasDiasRamos` → **Settings** → **Secrets and variables** → **Actions**.
2. Create a **new repository secret** named `METRICS_TOKEN` with your least-privilege personal access token. For classic tokens, upstream recommends no additional scopes when showing public information only.
3. Merge the pull request that adds this workflow.
4. Open **Actions** → **Visual GitHub Metrics** → **Run workflow**.
5. Confirm the job succeeded and produced:
   - `assets/metrics-languages.svg`
   - `assets/metrics-isocalendar.svg`
   - `assets/metrics-activity.svg`
6. Check the profile README. Images won't render until the first successful workflow run creates these files.

## Maintenance

- The workflow runs every Monday at **11:17 UTC**, which corresponds to **07:17 in Campo Grande** when UTC−4 applies.
- You can also rerun it on demand using **workflow_dispatch**.
- If generated images remain missing, inspect the GitHub Actions logs, confirm the repository has Actions enabled, verify the `METRICS_TOKEN` secret is available, and check that the default-branch workflow has permission to write repository contents.
- Language statistics can be influenced by vendored files, generated code, and repository size. They are not a measure of professional skill.
- Generated SVG files may be public even when source data is private; do not expand token permissions or enable private activity unless you intend those details to be visible.
