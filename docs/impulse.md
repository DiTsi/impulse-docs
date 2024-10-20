# IMPulse

You should set the environment variables and configure `impulse.yml`:

## environment variables

Environment variables are installed in `.env` file for python installation or in `docker-compose.yml` for docker installation. 

To run IMPulse you should set `SLACK_BOT_USER_OAUTH_TOKEN`, `SLACK_VERIFICATION_TOKEN` for Slack installation and `MATTERMOST_ACCESS_TOKEN` for Mattermost.

| Variable | Description | Default | Required |
|-|-|-|-|
| DATA_PATH | path to data directory | ./data | - |
| CONFIG_PATH | path to `impulse.yml` directory | ./ | - |
| LOG_LEVEL | Log level | INFO | - |
| MATTERMOST_ACCESS_TOKEN | [Mattermost 'Access Token'](mattermost.md) | ./ | for Mattermost |
| SLACK_BOT_USER_OAUTH_TOKEN | [Slack 'Bot User OAuth Token'](slack.md) | | for Slack |
| SLACK_VERIFICATION_TOKEN | [Slack 'Verification Token'](slack.md) | | for Slack |

## impulse.yml

`impulse.slack.yml` (or `impulse.mattermost.yml` for Mattermost) contains all available configuration options. Minimal required configuration is uncommented. 

Configuration has these blocks:

- incident
- timeouts
- route
- application
- webhooks
- experimental (don't use it)

### incident

Name | Description | Values
-|-|-
`alerts_firing_notifications` | Notification about new firing instances | `True` / `False` (default)
`alerts_resolved_notifications` | Nofitication about old resolved instances | `True` / `False` (default)

### timeouts

`timeouts` block has 3 options: `firing`, `unknown`, `resolved`. For information see comments in [impulse.slack.yml](https://github.com/DiTsi/impulse/blob/main/impulse.slack.yml) or [Concepts](concepts.md).

### route

Route for Incidents routing is based on alert's fields. It is made very similar to Alertmanager's [route](https://prometheus.io/docs/alerting/latest/configuration/#route).

### application

Instant messaging app configuration. See comments in impulse.yml examples for [Slack](https://github.com/DiTsi/impulse/blob/main/impulse.slack.yml) and [Mattermost](https://github.com/DiTsi/impulse/blob/main/impulse.mattermost.yml) to understand


### webhooks

See [Webhooks](webhooks.md) to 
understand how to work with it.

### experimental

WE HIGHLY RECOMMEND DO NOT USE IT

Name | Description | Values
-|-|-
`recreate_chain` | This option will <!-- release incident --> enable chain and start it again <br> when new alerts added to incident | `True` / `False` (default)
