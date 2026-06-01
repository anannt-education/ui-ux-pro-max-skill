# GitHub Actions Minute Budget

This repository is configured to reduce accidental GitHub Actions usage on private repositories.

## Operating Rules

- Local checks come first. GitHub Actions should confirm work, not be the first place syntax and dependency errors are discovered.
- Push fewer times. Batch related changes before pushing to a PR branch.
- Keep PRs as draft while iterating.
- Use `workflow_dispatch` for heavy or unusual checks.
- Do not use macOS or Windows runners unless the behavior is platform-specific.
- Keep production deploy workflows limited to the default branch or manual dispatch.

## Workflow Controls To Keep

- `concurrency.cancel-in-progress: true` for CI and deploy workflows so stale branch runs are cancelled.
- `timeout-minutes` on every job.
- `permissions: contents: read` unless the workflow truly needs more access.
- `actions/setup-node` or equivalent dependency caching based on lockfiles.
- `actions/checkout` with `fetch-depth: 1` unless full history is required.
- `paths-ignore` for docs-only changes on expensive CI/deploy workflows.
- Separate fast validation from e2e, Docker, mobile, or deployment work.

## Safe Skip Usage

GitHub supports commit-message skip tokens such as `[skip ci]` for `push` and `pull_request` workflows. Use this only for documentation or repository administration changes where validation is unnecessary. Do not use it for application code that needs checks before merge.

## Monitoring

Review usage regularly in GitHub billing and Actions run history. If usage climbs again, look first for branch push triggers, matrix jobs, long deploys, missing caches, and workflows running on docs-only changes.
