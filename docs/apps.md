# Apps

## Slack

### Add bot

1. Go to [Slack Apps](https://api.slack.com/apps) and click button **Create New App**
2. Select **From scratch**
3. Set **App Name** to "IMPulse" and select your workspace

### Configure bot

1. In **Basic Information** section copy "Verification Token" as ENV `SLACK_VERIFICATION_TOKEN`
2. In **OAuth & Permissions** section add these "Bot Token Scopes":
  - channels:read
  - chat:write
  - chat:write.customize
  - chat:write.public
  - groups:read
  - im:read
  - im:write
  - mpim:read
  - users:read
3. !!! Add REDIRECTURI
4. In **OAuth & Permissions** section click button "Install to Workspace"
5. !!! In **OAuth & Permissions** section **Restrict API Token Usage** subsection add IP address of your IMPulse server
5.  In **OAuth & Permissions** section copy "Bot User OAuth Token" as ENV `SLACK_BOT_USER_OAUTH_TOKEN`
6. In **Interactivity & Shortcuts** add "Request URL" in format `https://<your_domain>/slack`
7. In **Interactivity & Shortcuts** add two shortcuts
   - press the button "Create New Shortcut"
   - select "Global", press "Next"
   - type "Chain" to **Name**, "chain" to **Callback ID** and "." to **Short Description**
   - press **Create**
   - do the same for "Status" shortcut

We recommend use `white list` for your servers
