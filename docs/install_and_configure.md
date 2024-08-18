# Installation and Configuration

## configure Slack

[See](apps.md#slack) important notes, add and configure bot

## configure Alertmanager

All code examples about [`alertmanager.yml`](https://prometheus.io/docs/alerting/latest/configuration/)

### set repeat_interval

Set `repeat_interval` option less than [`timeouts.firing`](https://github.com/DiTsi/impulse/blob/main/impulse.slack.yml) (default `6h`). Explanation [here](concepts.md#unknown)

```yaml
route:
  repeat_interval: 4h
```

### move routing

IMPulse's `route` is similar to Alertmanager's, but simpler. Unlike of Alertmanager it has only four instructions: `routes`, `matchers`, `channel`, `chain`.

When using IMPulse as the only one incident manager, you can move full your Alertmaanger's [`route`](https://prometheus.io/docs/alerting/latest/configuration/#route) block from `alertmanager.yml` to `impulse.yml`. Don't forget to remove all unused instructions and change all `receiver` instrustions to `chain` and `channel`. Fill it correctly.

### modify receiver

Set IMPulse as default recever

```yaml
receivers:
- name: 'impulse'
  webhook_configs:
  - url: 'http://<impulse_host>:<impulse_port>/'

route:
  receiver: 'impulse'
```

## get

There are two ways to run IMPulse: python or docker. Select one of these

### python

```bash
git clone git@github.com:DiTsi/impulse.git impulse
cd impulse
# for Slack
cp impulse.slack.yml impulse.yml
cp .env.slack .env
# for Mattermost
cp impulse.mattermost.yml impulse.yml
cp .env.mattermost .env
```

### docker

```bash
mkdir impulse impulse/config impulse/data
cd impulse
wget -O docker-compose.yml https://raw.githubusercontent.com/DiTsi/impulse/master/docker-compose.yml
# for Slack
wget -O config/impulse.yml https://raw.githubusercontent.com/DiTsi/impulse/master/impulse.slack.yml
# for Mattermost
wget -O config/impulse.yml https://raw.githubusercontent.com/DiTsi/impulse/master/impulse.mattermost.yml
```

## configure

You should set two ENVs `SLACK_BOT_USER_OAUTH_TOKEN`, `SLACK_VERIFICATION_TOKEN` for Slack or `MATTERMOST_ACCESS_TOKEN` for Mattermost (see [apps](apps.md) to get it).

Modify `impulse.yml`

### environment variables

| Variable | Description | Default |
|-|-|-|
| DATA_PATH | path to data directory | ./data |
| CONFIG_PATH | path to `impulse.yml` directory | ./ |
| LOG_LEVEL | Log level | INFO |
| MATTERMOST_ACCESS_TOKEN | [Mattermost 'Access Token'](apps.md#mattermost) | ./ |
| SLACK_BOT_USER_OAUTH_TOKEN | [Slack 'Bot User OAuth Token'](apps.md#slack) | |
| SLACK_VERIFICATION_TOKEN | [Slack 'Verification Token'](apps.md#slack) | |

### impulse.yml

`impulse.slack.yml` (or `impulse.mattermost.yml` for Mattermost) has all available configuration options. By default enabled (without `#`) minimal configuration IMPulse can start with. For additional settings commented out.

On the root level configuration has these blocks:

- timeouts
- route
- application
- webhooks

#### timeouts

`timeouts` block have 3 options: `firing`, `unknown`, `resolved`. For information see comments in [impulse.slack.yml](https://github.com/DiTsi/impulse/blob/main/impulse.slack.yml) or [Concepts](concepts.md).

#### route

Route for Incidents routing based on alert's fields. It made very similar to Alertmanager's [route](https://prometheus.io/docs/alerting/latest/configuration/#route).

#### webhooks

Webhooks used to send POST HTTP requests

##### examples

###### Twilio calls

1. Configure `webhooks` in `impulse.yml` that way:
        
        webhooks:
          Dmitry_call:
            url: "https://api.twilio.com/2010-04-01/Accounts/{{ env['TWILIO_ACCOUNT_SID'] }}/Calls.json"
            data:
              To: '+998xxxxxxxxx'
              From: "{{ env['TWILIO_NUMBER'] }}"
              Url: http://example.com/twiml.xml
            auth: "{{ env['TWILIO_ACCOUNT_SID'] }}:{{ env['TWILIO_AUTH_TOKEN'] }}"

2. Add custom environment variables in `.env` or `docker-compose.yml`:

        TWILIO_ACCOUNT_SID
        TWILIO_AUTH_TOKEN
        TWILIO_NUMBER

###### Zvonok.com calls

1. Configure `webhooks` in `impulse.yml` that way:

        webhooks:
          Dmitry_call:
            url: "https://zvonok.com/manager/cabapi_external/api/v1/phones/call/"
            data:
              campaign_id: '{{ env["ZVONOK_CAMPAIGN_ID"] }}'
              phone: '+998xxxxxxxxx'
              public_key: '{{ env["ZVONOK_PUBLIC_KEY"] }}'

2. Add custom environment variables in `.env` or `docker-compose.yml`:

        ZVONOK_CAMPAIGN_ID
        ZVONOK_PUBLIC_KEY

## run

Use your installation option

### python

```bash
# use 'SLACK_BOT_USER_OAUTH_TOKEN' and
# 'SLACK_VERIFICATION_TOKEN' from 1 step
echo 'SLACK_BOT_USER_OAUTH_TOKEN=<your_oauth_token>' > .env #!
echo 'SLACK_VERIFICATION_TOKEN=<your_verif_token>' >> .env #!
```

### docker

Set environment variables

```yaml
SLACK_BOT_USER_OAUTH_TOKEN
SLACK_VERIFICATION_TOKEN
```

in `docker-compose.yml` and run IMPulse:

```bash
docker-compose up -d
```
