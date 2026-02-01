# Contributing

Thanks for helping improve PivotStream!

## Setup
```bash
python3 -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
```

## Release tooling (git-cliff)
Install the optional release dependencies:
```bash
pip install -e ".[release]"
```

Generate the changelog:
```bash
git cliff -o CHANGELOG.md
```

## Pre-commit
```bash
pip install pre-commit
pre-commit install
pre-commit run --all-files
```

## Release Process
Releases are fully automated via GitHub Actions.

### Manual initiation
- Run the **Release Automation** workflow (workflow_dispatch).
- The workflow determines the bump type, calculates the next version, generates the changelog, and opens a PR from `bot/release/vX.Y.Z` with label `release`.

### PR updates
- Any push to `bot/release/*` regenerates the changelog and updates the PR automatically.

### Release creation
- When the release PR is merged into `main`, the workflow tags the merge commit, creates the GitHub release, and marks it as the latest.

### Local checks (optional)
```bash
scripts/test_bump_type.sh
```

### Branch protection
Branch protection rules (e.g., required PR reviews) must be configured in GitHub repository settings.

## First-Time Release Setup
- [ ] Install git-cliff locally: `pip install -e ".[release]"`
- [ ] Configure bot access (see `docs/internal/bot-setup.md`) and add `RELEASE_BOT_TOKEN` as a GitHub secret (SECRET)
- [ ] Run the Release Automation workflow on a feature branch to verify it opens a PR
- [ ] Set up branch protection rules for `main` (require PR reviews, prevent direct pushes)

## Troubleshooting
- **Bot token authentication failures**: verify `RELEASE_BOT_TOKEN` exists in repo secrets and the bot has Contents/PR write access.
- **Changelog generation errors**: ensure `git-cliff` installs successfully and `cliff.toml` is valid.
- **PR creation conflicts**: check for an existing open PR from `bot/release/vX.Y.Z`, or delete the stale branch.
- **Tag already exists**: delete the tag if it was created accidentally, or bump the version and rerun.
