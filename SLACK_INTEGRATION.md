# Slack Integration for Homework PRs

This repository now includes automatic Slack notifications for homework pull request status updates.

## Features

The Slack integration provides real-time notifications for:

- **📝 New PRs Opened**: When students submit new homework
- **✅ PRs Merged**: When homework passes all checks and is accepted  
- **⚠️ PRs Flagged**: When homework needs changes or has issues
- **🔒 PRs Closed**: When stale PRs are automatically closed
- **⏰ Stale PRs**: When PRs have been open for extended periods

## Quick Setup

1. **Enable the feature**: Set `SLACK_ENABLED=true` in GitHub Secrets
2. **Configure Slack**: Follow the [Slack Setup Guide](.github/SLACK_SETUP.md)
3. **Add secrets**: Configure either webhook URL or bot token
4. **Test it**: Open a test PR to verify notifications work

## Notification Examples

### New PR Opened
```
📝 *New Homework PR Opened*
👤 johndoe opened PR #42
📚 Week 3 Exercise Submission
🔗 https://github.com/...
📅 Week: 3
```

### PR Merged
```
✅ *Homework PR Merged*
👤 johndoe's homework passed all checks!
📚 PR #42: Week 3 Exercise Submission
🔗 https://github.com/...
🎉 Great work!
```

### PR Flagged
```
⚠️ *Homework PR Needs Changes*
👤 johndoe's PR needs attention
📚 PR #42: Week 3 Exercise Submission
🔗 https://github.com/...
❓ Issue: Invalid file(s)
```

## Configuration

### GitHub Secrets Required

- `SLACK_ENABLED`: Set to `true` to enable notifications
- `SLACK_WEBHOOK_URL`: Your Slack webhook URL (recommended method)
- `SLACK_CHANNEL`: Target channel (defaults to `#homework-notifications`)

### Optional Features

- **Personalized notifications**: Map GitHub usernames to Slack user IDs
- **Instructor alerts**: Separate notifications for instructors
- **Custom channels**: Different channels for different types of notifications

## Troubleshooting

### Notifications not appearing
1. Check that `SLACK_ENABLED=true` in GitHub Secrets
2. Verify the webhook URL is correct
3. Ensure the Slack app has proper permissions
4. Check GitHub Actions logs for errors

### Messages going to wrong channel
- Verify `SLACK_CHANNEL` secret value
- Check webhook is configured for correct channel
- Ensure channel exists in your workspace

### Too many notifications
- Set `SLACK_ENABLED=false` to disable temporarily
- Consider using separate channels for different notification types
- Adjust notification frequency in workflow settings

## Advanced Configuration

### Custom Notification Templates
The notification templates can be customized in the GitHub workflow file:
- File: `.github/workflows/Review-HW-PRs.yml`
- Section: `SLACK_TEMPLATES` object
- Modify the message format and content as needed

### Multi-Channel Support
To send different notifications to different channels:
1. Create multiple webhooks for different channels
2. Modify the workflow to use specific webhooks per notification type
3. Update secret names accordingly

### User-Specific Notifications
For direct messages to students:
1. Create a user mapping file: `.github/slack_user_mapping.json`
2. Map GitHub usernames to Slack user IDs
3. Modify the notification function to use direct messages

## Security Best Practices

- Never commit Slack tokens to the repository
- Use GitHub Secrets for all sensitive information
- Regularly rotate webhook URLs and tokens
- Limit Slack app permissions to minimum required
- Monitor Slack app usage and access logs

## Future Enhancements

Potential improvements for the Slack integration:

- **Deadline reminders**: Automated reminders before homework due dates
- **Progress tracking**: Weekly summaries of student progress
- **Instructor dashboard**: Slack command to check overall PR status
- **Peer review notifications**: Alerts for peer review assignments
- **Grade announcements**: Automated grade posting to Slack

## Support

For issues or questions about the Slack integration:

1. Check the [Slack Setup Guide](.github/SLACK_SETUP.md) for detailed setup instructions
2. Review GitHub Actions logs for error messages
3. Verify Slack app permissions and configuration
4. Contact repository maintainers for additional help

## Contributing

To improve the Slack integration:

1. Test changes in a fork first
2. Use `SLACK_ENABLED=false` for development
3. Add comprehensive tests for notification logic
4. Update documentation for any new features
5. Submit a PR with clear description of changes