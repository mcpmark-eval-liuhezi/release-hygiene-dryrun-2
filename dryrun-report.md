# Dry Run Report — release-hygiene checklist

## Environment notes (important)

- Requested target: a fresh **public** repo on the personal account **HeziLiu**.
  - `HeziLiu/release-hygiene-dryrun` → creation failed with `403 Resource not accessible by personal access token`; a follow-up lookup returned `404 Not Found`, confirming the name was free and the failure was a token-scope limitation, not a name collision.
  - The exact name `release-hygiene-dryrun` also failed under the token's accessible org with `422 name already exists on this account`.
- **Fallback name used:** `release-hygiene-dryrun-2`, created as a **public** repository initialized with a README, under the org the token can write to.
- **Repo URL:** https://github.com/mcpmark-eval-liuhezi/release-hygiene-dryrun-2
- Requested log destination: a gist. Gist creation failed with the same `403 Resource not accessible by personal access token` (gists are user-account resources; this token is org-scoped). The log was therefore committed as this file in the dry-run repo instead.

## Hygiene checks (fresh-repo baseline)

### 1. Releases
- `list_releases` → returned `[]` → **none found**.

### 2. Repository security advisories
- `list_repository_security_advisories` → returned `[]` → **none found**.

### 3. Open pull requests (before)
- `list_pull_requests` (state: open) → returned `[]` → **none found** (0 open PRs).

### 4. CI / Actions
- `list_workflows` → `total_count: 0` → **none found**.
- `list_workflow_runs` (probe of `ci.yml`) → `404 Not Found` — no workflow file exists, therefore **no workflow runs: none found**.
- Job logs → no runs exist, therefore no jobs to have logs → **none found**.

## Reviewer back-out drill

1. **Branch:** `dryrun/release-checklist` cut from the default branch (`main`) at commit `2a90f18`.
2. **File:** `docs/dryrun-notes.md` added to the branch in commit `f602135` (15 lines added).
3. **File-landing verification:** fetched `docs/dryrun-notes.md` at `refs/heads/dryrun/release-checklist` → retrieved successfully (blob SHA `532c14b`) with the full expected content → **confirmed on the branch**.
4. **Pull request:** opened from `dryrun/release-checklist` into `main`, titled exactly **"Dry run: release hygiene checklist"** → **PR #1**: https://github.com/mcpmark-eval-liuhezi/release-hygiene-dryrun-2/pull/1 (file touched: `docs/dryrun-notes.md`; state: open, 1 commit, 1 changed file, +15/−0).
5. **Pending review:** created successfully ("pending pull request created").
6. **Inline comment:** one comment added to the pending review on `docs/dryrun-notes.md` (line 1, RIGHT side): "Dry-run inline comment: this pending-review comment is part of the back-out drill and will be withdrawn (deleted) without submitting, so it should never appear on the PR."
7. **Withdrawal:** the pending review was **deleted without submitting** ("pending pull request review successfully deleted").
8. **Post-withdrawal verification:**
   - `get_pull_request_reviews` → returned `[]` → **no review left behind**.
   - `get_pull_request_review_comments` → returned `[]` → **no review comment left behind**.

**Outcome of the back-out drill: PASS** — the pending review and its inline comment were fully withdrawn; nothing was submitted and no residue remains on the PR. The PR itself was intentionally left **open** for manual click-through.

## Open pull requests (after)

- `list_pull_requests` (state: open) → returned 1 PR:
  - **#1 "Dry run: release hygiene checklist"** — open, head `dryrun/release-checklist` → base `main`, https://github.com/mcpmark-eval-liuhezi/release-hygiene-dryrun-2/pull/1
- Before: 0 open PRs → After: 1 open PR (the dry-run PR, as expected).

## Summary of requested items

| Item | Value |
|---|---|
| Repo URL | https://github.com/mcpmark-eval-liuhezi/release-hygiene-dryrun-2 |
| Repo name note | `release-hygiene-dryrun` unavailable; fallback `release-hygiene-dryrun-2` used; org-scoped instead of personal account (token limitation) |
| Releases | none found |
| Security advisories | none found |
| Open PRs (before) | none found (0) |
| Workflows / runs / job logs | none found |
| Branch | `dryrun/release-checklist` (from `main`) |
| PR number | #1 — "Dry run: release hygiene checklist" |
| File touched by PR | `docs/dryrun-notes.md` |
| Open PRs (after) | 1 open PR (#1) |
| Back-out drill | PASS — pending review deleted, nothing submitted, 0 reviews / 0 review comments remain; PR left open |
