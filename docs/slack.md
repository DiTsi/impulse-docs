## Slack

### Create bot

1. Go to [Slack Apps](https://api.slack.com/apps) and click button **Create New App**.
2. Select **From scratch**.
3. Set **App Name** to "IMPulse" and select your workspace.

### Configure bot

1. In **Interactivity & Shortcuts** section:
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
2. In **OAuth & Permissions** section:
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
    - we highly recommend to add the IP address of your IMPulse server in white list in **Restrict API Token Usage** subsection
    - use "Bot User OAuth Token" as ENV `SLACK_BOT_USER_OAUTH_TOKEN` (using [here](impulse.md))
3. In **Basic Information** section:
    - in **App Credentials** subsection:
        - use "Verification Token" as ENV `SLACK_VERIFICATION_TOKEN` (using [here](impulse.md))
    - in **Display Information** subsection:
        - you can set [our logo](media/logo.png) as **App icon**

### Configure channels

1. `application.admin_users` **should** be in all `route` channels.
2. Add users from `application.chains` to their channels.

    To make it simpler you can add all `application.users` to all channels from `route`. If users do next recommendation, no extra notifications will appear.

3. Highly recommend to set "Just @mentions" notifications for every of `application.users` for their `route` channels. Users on their channels should:
    - press **right mouse button** on channel and select "Change notifications"
    - select "Mentions" and check "Also include @channel and @here
    - press **Save Changes**