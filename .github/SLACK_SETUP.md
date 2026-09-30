# Slack Integration Setup Guide

This guide explains how to set up Slack notifications for homework PR status updates.

## Overview

The Slack integration will automatically notify students when their homework PRs are:
- Opened (new submission)
- Reviewed and passed (merged)
- Reviewed and needs changes (flagged)
- Closed (stale or resolved)

## Prerequisites

- Admin access to your Slack workspace
- Admin access to the GitHub repository
- GitHub repository admin permissions for secrets

## Step 1: Create a Slack App

1. Go to [api.slack.com/apps](https://api.slack.com/apps)
2. Click **"Create New App"**
3. Choose **"From scratch"**
4. Name the app (e.g., "CTP Homework Bot")
5. Select your Slack workspace
6. Click **"Create App"**

## Step 2: Configure App Permissions

### Bot Permissions
1. Go to **"OAuth & Permissions"** in the left sidebar
2. Under **"Scopes"** → **"Bot Token Scopes"**, add:
   - `chat:write` - Send messages to channels
   - `chat:write.public` - Send messages to channels the bot isn't in
   - `users:read` - Read user information (optional, for personalized messages)

### Install App to Workspace
1. Scroll up to **"OAuth Tokens for Your Workspace"**
2. Click **"Install to Workspace"**
3. Review permissions and click **"Allow"**
4. **Copy the Bot User OAuth Token** (starts with `xoxb-`) - you'll need this for GitHub secrets

## Step 3: Configure Incoming Webhooks (Alternative Method)

If you prefer webhooks over bot tokens:

1. In your Slack app, go to **"Incoming Webhooks"**
2. Toggle **"Activate Incoming Webhooks"** to On
3. Click **"Add New Webhook to Workspace"**
4. Select the channel where notifications should be posted
5. **Copy the Webhook URL** - you'll need this for GitHub secrets

## Step 4: Create GitHub Secrets

Navigate to your GitHub repository:
1. Go to **Settings** → **Secrets and variables** → **Actions**
2. Click **"New repository secret"**

Add the following secrets:

### Required Secrets
- **Name**: `SLACK_ENABLED`
- **Value**: `true` (to enable Slack notifications) or `false` (to disable)

### Choose One Method

#### Using Webhook (Recommended - simpler setup)
- **Name**: `SLACK_WEBHOOK_URL`  
- **Value**: Your Incoming Webhook URL

#### Using Bot Token (Advanced - more features)
- **Name**: `SLACK_BOT_TOKEN`
- **Value**: Your Bot User OAuth Token (starts with `xoxb-`)

### Optional Configuration
- **Name**: `SLACK_CHANNEL`
- **Value**: Default Slack channel for notifications (e.g., `#homework-notifications`)
- **Default**: `#homework-notifications` if not specified

## Step 5: Configure Slack Channel Mapping (Optional)

For personalized notifications to individual students:

1. Create a mapping file in the repository: `.github/slack_user_mapping.json`
2. Map GitHub usernames to Slack user IDs:
```json
{
  "github-username-1": "U1234567890",
  "github-username-2": "U0987654321"
}
```

To find Slack user IDs:
- In Slack, right-click on a user → "Copy Link" 
- The ID is in the URL (e.g., `https://yourworkspace.slack.com/team/U1234567890`)

## Step 6: Test the Integration

Once configured, the GitHub workflow will automatically send Slack notifications when:
- Students open new homework PRs
- PRs pass all checks and are merged
- PRs are flagged for issues
- PRs are closed

## Troubleshooting

### Bot not sending messages
- Verify the bot token is correct
- Check that the bot has been invited to the target channel
- Ensure the GitHub Actions secret is properly set

### Messages going to wrong channel
- Check the `SLACK_CHANNEL` secret value
- Verify the channel exists in your workspace
- For webhooks, ensure the webhook is pointing to the correct channel

### Permission errors
- Verify the bot has the required scopes
- Check that the bot is installed to the correct workspace
- Ensure the bot has access to the target channel

## Security Notes

- Never commit Slack tokens to the repository
- Use GitHub Secrets for all sensitive information
- Regularly rotate tokens for security
- Limit bot permissions to only what's needed

## Next Steps

After setup, the GitHub workflow will automatically:
1. Send notifications when PRs are opened
2. Alert students when their homework passes/fails checks
3. Notify instructors of stuck or problematic PRs
4. Provide direct links to PRs for quick access

The integration is designed to be non-intrusive and helpful, keeping students informed without overwhelming them with notifications.