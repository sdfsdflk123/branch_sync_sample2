hasdasdell
# branch sync sample 2

This repository demonstrates a GitHub Actions flow that versions `master` and syncs it to `develop` after a merged PR from `hotfix/*` or `release/*`.

## Workflows

- `.github/workflows/release-version-and-sync-develop.yml`: runs on merged PRs to `master`, bumps version, pushes `master`, then syncs to `develop` using the shared reusable workflow from `branch_sync_sample`.

## Release rules

- `hotfix/*` -> `standard-version --release-as patch`
- `release/*` -> `standard-version --release-as minor`

## Required secrets

- `SYNC_DEVELOP_APP_ID`
- `SYNC_DEVELOP_APP_PRIVATE_KEY`

## GitHub App setup

1. Create a GitHub App.
2. Grant repository permissions:
   - `Contents`: Read and write
   - `Metadata`: Read-only
3. Install the app on this repository.
4. Add the app to bypass rules for `master` and `develop` if branch protection blocks direct pushes.

## Notes

- `standard-version` is invoked with `npx --yes`, so no local install step is required for this demo.
- The workflow uses `actions/create-github-app-token@v2` and `actions/checkout@v5`.
- The sync step uses the shared reusable workflow at `sdfsdflk123/branch_sync_sample/.github/workflows/sync-base-to-develop.reusable.yml@develop`.
