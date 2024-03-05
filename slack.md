# Slack

Basically `bot` has write access to all `public` channels. But if you want to send messages to `private` channels you should add `bot` to them.

## OAuth & Permissions

### Scopes

#### Bot Token Scopes

Minimal required scope list:
  - chat:write
  - chat:write.customize
  - chat:write.public
  - commands
  - im:write

### Restrict API Token Usage

We recommend use `white list` for your servers
