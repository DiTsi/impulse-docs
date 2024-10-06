## Mattermost

### Create bot

1. Go to Menu (dots 3x3) > System Console > Integrations > Bot Accounts:
    - set `True` for "Enable Bot Account Creation", press "Save"
2. Go to Menu (dots 3x3) > Integarations > Bot Accounts:
    - press the button "Add Bot Account"
    - type "IMPulse" to **Username**
    - you can set [our icon](media/logo.png) as **Bot Icon**
    - set **Role** to "System Admin"
    - press the button "Create Bot Account"
    - use "Token" as ENV `MATTERMOST_ACCESS_TOKEN` (using [here](impulse.md))
    - press the button **Done**

### Configure bot

1. Go to Menu (dots 3x3) > System Console > User Management > Teams:
    - press on your Team
    - press the button **Add Members**
    - type "impulse" in search, select it and press the button **Add**
    - press the button **Save**

### Configure channels

Do the same [instruction for Slack](slack.md#configure-channels)

<!-- 4. To use IMPulse bot in private channels you should add it manually. Run command in all necessary private channels:
    ```
    /invite @impulse 
    ``` -->
