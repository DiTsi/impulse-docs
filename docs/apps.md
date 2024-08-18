# Instant Messaging Apps

## Notes

Now only public channels are supported.

All [application.admin_users](https://github.com/DiTsi/impulse/blob/main/impulse.slack.yml) should be added to all incident channels.

## Slack

### Add bot

1. Go to [Slack Apps](https://api.slack.com/apps) and click button **Create New App**
2. Select **From scratch**
3. Set **App Name** to "IMPulse" and select your workspace

### Configure bot

1. In **Interactivity & Shortcuts** section
    - enable "Interactivity"
    - add **Request URL** in format `https://<your_domain>/app`
    - add shortcuts **Chain** and **Status**:
        - press the button **Create New Shortcut**
        - select "Global", press the button **Next**
        - set **Name** to "Chain", **Callback ID** to "chain" and **Short Description** to "."
        - press the button **Create**
        - press the button **Create New Shortcut**
        - select "Global", press the button **Next**
        - set **Name** to "Status", **Callback ID** to "status" and **Short Description** to "."
        - press the button **Create**
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
    - click the button **Install to Workspace**
    - we highly recommend add IP address of your IMPulse server in white list in **Restrict API Token Usage** subsection
    - use "Bot User OAuth Token" as ENV `SLACK_BOT_USER_OAUTH_TOKEN` (see [configure](install_and_configure.md#configure))
3. In **Basic Information** section
    - use "Verification Token" as ENV `SLACK_VERIFICATION_TOKEN` (see [configure](install_and_configure.md#configure))

### Configure channels

1. `application.admin_users` **should** be in all `route` channels
2. Add users from `application.chains` to their channels. 

   To make it simpler you can add all `application.users` to all channels from `route`. If users do next recommendation, no extra notifications will appear
3. Highly recommend to set "Just @mentions" notifications for every of `application.users` for their `route` channels. Users on their channels should:
    - press **right mouse button** on channel and select "Change notifications"
    - select "Mentions" and check "Also include @channel and @here
    - press **Save Changes**

## Mattermost

### Add bot

1. Go to Menu (dots 3x3) > System Console > Integrations > Bot Accounts
    - set `True` for "Enable Bot Account Creation", press "Save"
2. Go to Menu (dots 3x3) > Integarations > Bot Accounts
    - press the button "Add Bot Account"
    - type "IMPulse" to **Username**
    <!-- - select icon  -->
    - set **Role** to "System Admin"
    - press the button "Create Bot Account"
    - use "Token" as ENV `MATTERMOST_ACCESS_TOKEN` (see [configure](install_and_configure.md#configure))
    - press the button **Done**

### Configure bot

1. Go to Menu (dots 3x3) > System Console > User Management > Teams
- press on your Team
- press the button **Add Members**
- type "impulse" in search, select it and press the button **Add**
- press the button **Save**

### Configure channels

See [instruction for Slack](apps.md#configure-channels)
