# Codex Working Rules

## GitHub Actions Budget

- Treat private GitHub Actions minutes as scarce. Run local verification before pushing whenever the relevant toolchain is available.
- Batch related changes into fewer pushes. Do not push repeatedly just to test syntax or quick failures.
- Prefer draft PRs while work is still exploratory. Mark ready only after local checks pass.
- Do not trigger deployment workflows unless a production deploy is intended.
- Use `[skip ci]` only for documentation-only or repository-administration commits where checks are not needed. Do not use it to bypass required validation for application code.
- Keep heavy checks such as e2e suites, Docker image builds, mobile builds, coverage uploads, and OS matrix tests behind `workflow_dispatch`, main-branch merges, or an explicit user request.
- When editing workflows, include stale-run cancellation, path filters, job timeouts, Linux runners, dependency caching, and shallow checkout where compatible with the job.

## Local Verification First

- For Node repositories, prefer `npm ci` plus the repo's existing `typecheck`, `test`, `lint`, and `build` scripts.
- For Python repositories, run the project test/lint commands locally before opening or updating a PR.
- For deploy-only repositories, inspect the changed paths carefully and avoid pushing deploy-triggering changes unless the deployment should happen.
