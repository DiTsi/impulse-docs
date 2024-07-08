# Instant Messaging Apps

## Slack

### Notes

Now only public channels are supported.

All [application.admin_users](https://github.com/DiTsi/impulse/blob/main/impulse.yml.slack) should be added to all incident channels.

### Add bot

1. Go to [Slack Apps](https://api.slack.com/apps) and click button **Create New App**
2. Select **From scratch**
3. Set **App Name** to "IMPulse" and select your workspace

### Configure bot

1. In **Interactivity & Shortcuts** section
    - enable "Interactivity"
    - add "Request URL" in format `https://<your_domain>/app`
    - add shortcuts "Chain" and "Status":
        - press the button "Create New Shortcut"
        - select "Global", press "Next"
        - type "Chain" to **Name**, "chain" to **Callback ID** and "." to **Short Description**
        - press **Create**
        - press the button "Create New Shortcut"
        - select "Global", press "Next"
        - type "Status" to **Name**, "status" to **Callback ID** and "." to **Short Description**
        - press **Create**
2. In **OAuth & Permissions** section
    - in **Scopes** subsection add these "Bot Token Scopes":
        - channels:read
        - chat:write
        - chat:write.customize
        - chat:write.public
        - groups:read
        - im:read
        - im:write
        - mpim:read
        - users:read
    - click button "Install to Workspace"
    - we highly recommend add IP address of your IMPulse server in white list in **Restrict API Token Usage** subsection
    - copy "Bot User OAuth Token" as ENV `SLACK_BOT_USER_OAUTH_TOKEN` (see [configure](install_and_configure.md#configure))
3. In **Basic Information** section
    - copy "Verification Token" as ENV `SLACK_VERIFICATION_TOKEN` (see [configure](install_and_configure.md#configure))

## Mattermost
    Role System Admin
    Go to System Console > User Management > Teams, add bot to Team