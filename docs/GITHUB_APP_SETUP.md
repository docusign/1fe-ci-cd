# GitHub App Authentication Setup

This document describes how to set up GitHub App authentication for automated widget builds and deployments.

## Overview

The `1fe-admin` GitHub App is used to authenticate automated commits and cross-repository operations in the widget build process. This provides better security, audit trails, and permissions management compared to using personal access tokens.

## Required Configuration

### 1. Repository Variables

Set the following repository variable in your GitHub repository settings:

- **Name**: `FE_ADMIN_APP_ID`  
- **Value**: The App ID of your `1fe-admin` GitHub App
- **Location**: Repository → Settings → Secrets and Variables → Actions → Variables tab

### 2. Repository Secrets  

Set the following repository secret:

- **Name**: `FE_ADMIN_PRIVATE_KEY`
- **Value**: The complete private key for your `1fe-admin` GitHub App (including `-----BEGIN RSA PRIVATE KEY-----` and `-----END RSA PRIVATE KEY-----` lines)
- **Location**: Repository → Settings → Secrets and Variables → Actions → Secrets tab

## GitHub App Configuration

Your `1fe-admin` GitHub App should have the following permissions:

### Repository Permissions:
- **Contents**: Write (for pushing commits and tags)
- **Metadata**: Read (for repository information)
- **Pull requests**: Write (if needed for PR operations)

### Installation:
- Install the `1fe-admin` app on the organization/repositories where widget builds will run
- Grant access to repositories that need automated commits

## How It Works

1. **Token Generation**: The workflow uses `actions/create-github-app-token@v2` to generate an installation access token
2. **Bot User Configuration**: Git is configured to use the GitHub App's bot user for commits
3. **Authenticated Operations**: All git operations (commits, pushes, tagging) use the app token
4. **Automatic Cleanup**: Tokens are automatically revoked after the job completes

## Benefits

- ✅ **Cross-repository access**: Can access multiple repositories in the organization
- ✅ **Better audit trail**: Commits appear from `1fe-admin[bot]` user
- ✅ **Enhanced security**: Tokens are short-lived and scoped to specific permissions
- ✅ **No personal tokens**: Doesn't rely on individual user credentials
- ✅ **Centralized management**: All automation uses the same app identity

## Troubleshooting

### Common Issues:

1. **"Invalid app-id" error**: Verify `FE_ADMIN_APP_ID` is set correctly
2. **"Invalid private key" error**: Ensure `FE_ADMIN_PRIVATE_KEY` includes the full key with headers
3. **"Installation not found" error**: Verify the app is installed on the target repository
4. **Permission denied**: Check the app has required permissions (Contents: Write)

### Verification:

You can verify the setup by checking that commits from automated builds show as `1fe-admin[bot]` in the git history.

## Related Documentation

- [GitHub Apps Documentation](https://docs.github.com/en/apps/creating-github-apps/authenticating-with-a-github-app/making-authenticated-api-requests-with-a-github-app-in-a-github-actions-workflow)
- [actions/create-github-app-token](https://github.com/actions/create-github-app-token)