# Bot Setup for Automated Releases

This document describes how to configure a bot identity for automated releases in PivotStream.

## Option A: GitHub App (recommended)
1. Create a GitHub App:
   - Go to **Settings → Developer settings → GitHub Apps → New GitHub App**.
   - App name: `PivotStream Release Bot` (example).
   - Homepage URL: your repo URL.
   - Webhook: disable or leave blank if not needed.
2. Permissions:
   - **Contents: Read & write**
   - **Pull requests: Read & write**
3. Install the app on the PivotStream repository.
4. Generate a private key for the app and download it.
5. Create a bot token:
   - Use the GitHub App credentials to generate an installation access token.
   - Store this token securely (SECRET).

## Option B: Bot user (simple)
1. Create a dedicated GitHub user (e.g., `pivotstream-bot`).
2. Add the user to the PivotStream repo with **Write** access.
3. Create a Personal Access Token (classic) with:
   - **repo** (full control of private repositories)
4. Store the token securely (SECRET).

## Store the token in GitHub Secrets
1. Go to **Repo → Settings → Secrets and variables → Actions**.
2. Create a new secret:
   - Name: `RELEASE_BOT_TOKEN`
   - Value: the bot token (SECRET)

## Security Notes
- Treat all tokens as **SECRET**. Never commit them to the repo.
- Rotate tokens if they are exposed.
- Prefer GitHub App tokens for tighter scope and auditability.
