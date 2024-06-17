# Configuration

## Config file
The only one configuration file of IMPulse is `impulse.yml`.
Path to this file by `CONFIG_PATH` (see [Environment](configuration.md#environment))

Just copy `impulse.yml.default` to `impulse.yml` and modify it to configure IMPulse. By default it has minimal configuration IMPulse start with. And all additional possible settings commented out.

On the root level configuration has these blocks:
```
timeouts:
route:
application:
webhooks:
```

### Timeouts
`timeouts` have 3 options: `firing`, `unknown`, `resolved`. See  [unknown](theory.md#unknown) and [closed](theory.md#closed) Incident status documentation to understand.

### Route

Used for Incidents routing based on alert's fields. It made very similar to Alertmanager's [route](https://prometheus.io/docs/alerting/latest/configuration/#route).

## Environment variables

| Variable | Description | Default |
|-|-|-|
| DATA_PATH | Path to DATA directory | ./data |
| CONFIG_PATH | Path to CONFIG directory | ./ |
| SLACK_BOT_USER_OAUTH_TOKEN | Slack Bot | |
| SLACK_VERIFICATION_TOKEN | Slack Bot | |

### Secrets

[Webhook](webhook.md) config allows you to declare custom ENVs for secrets or duplicates (see [Twilio](webhook.md#twilio) example).
