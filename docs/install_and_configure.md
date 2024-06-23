# Installation and Configuration

## 1 create Slack bot

Instuction [here](apps.md#slack)

## 2 configure Alertmanager

All code examples about [`alertmanager.yml`](https://prometheus.io/docs/alerting/latest/configuration/)

### 2.1 set repeat_interval

Set `repeat_interval` option less than [`timeouts.firing`](https://github.com/DiTsi/impulse/blob/main/impulse.yml.default) (default `6h`). Explanation [here](concepts.md#unknown)

```yaml
route:
  repeat_interval: 4h
```

### 2.2 move routing

IMPulse's `route` is similar to Alertmanager's, but simpler. Unlike of Alertmanager it has only four instructions: `routes`, `matchers`, `channel`, `chain`.

When using IMPulse as the only one incident manager, you can move full your Alertmaanger's [`route`](https://prometheus.io/docs/alerting/latest/configuration/#route) block from `alertmanager.yml` to `impulse.yml`. Don't forget to remove all unused instructions and change all `receiver` instrustions to `chain` and `channel`. Fill it correctly.

### 2.3 modify receiver

Set IMPulse as default recever

```yaml
receivers:
- name: 'impulse'
  webhook_configs:
  - url: 'http://<impulse_host>:<impulse_port>/'

route:
  receiver: 'impulse'
```

## 3 get

There are two ways to run IMPulse: python or docker. Select one of these

### 3.1 python

```bash
git clone git@github.com:DiTsi/impulse.git impulse
cd impulse
cp impulse.yml.default impulse.yml
```

### 3.2 docker

```bash
mkdir impulse impulse/config impulse/data
cd impulse
wget https://github.com/DiTsi/impulse/blob/develop/docker-compose.yml
wget https://github.com/DiTsi/impulse/blob/develop/impulse.yml.default config/impulse.yml
```

## 4 configure

You should set two ENVs `SLACK_BOT_USER_OAUTH_TOKEN`, `SLACK_VERIFICATION_TOKEN` (ref. 4.1) and modify `impulse.yml` (ref. 4.2)

### 4.1 environment variables

| Variable | Description | Default |
|-|-|-|
| DATA_PATH | path to data directory | ./data |
| CONFIG_PATH | path to `impulse.yml` directory | ./ |
| SLACK_BOT_USER_OAUTH_TOKEN | [Slack 'Bot User OAuth Token'](apps.md#configure-bot) | |
| SLACK_VERIFICATION_TOKEN | [Slack 'Verification Token'](apps.md#configure-bot) | |

### 4.2 impulse.yml

`impulse.yml.default` has minimal configuration IMPulse can start with. All additional settings commented out.

On the root level configuration has these blocks:

- timeouts
- route
- application
- webhooks

#### 4.2.1 timeouts

`timeouts` block have 3 options: `firing`, `unknown`, `resolved`. For information see comments in [impulse.yml.default](https://github.com/DiTsi/impulse/blob/main/impulse.yml.default) or [Concepts](concepts.md).

#### 4.2.2 route

Route for Incidents routing based on alert's fields. It made very similar to Alertmanager's [route](https://prometheus.io/docs/alerting/latest/configuration/#route).

### 4.3 webhooks

Webhooks used to send POST HTTP requests

#### 4.3.1 examples

##### 4.3.1.1 Twilio calls

Configure `webhooks` in `impulse.yml` that way:
```yaml
webhooks:
  Oleg:
    url: "https://api.twilio.com/2010-04-01/Accounts/{{ env['TWILIO_ACCOUNT_SID'] }}/Calls.json"
    data:
      To: '+998xxxxxxxxx'
      From: "{{ env['TWILIO_NUMBER'] }}"
      Url: http://example.com/twiml.xml
    user: "{{ env['TWILIO_ACCOUNT_SID'] }}:{{ env['TWILIO_AUTH_TOKEN'] }}"
```

Don't forget to set custom environment variables in `.env` or `docker-compose.yml`:
```ini
TWILIO_ACCOUNT_SID=<xxxxxxxxxxxxx>
TWILIO_AUTH_TOKEN=<xxxxxxxxxxxxx>
TWILIO_NUMBER=+<xxxxxxxxxxxxx>
```

### 4.4 secrets

[Webhook](webhook.md) config allows you to declare custom ENVs for secrets or duplicates (see [Twilio](webhook.md#twilio) example).

## 5 run

Use 

### 5.1 python

```bash
# use 'SLACK_BOT_USER_OAUTH_TOKEN' and
# 'SLACK_VERIFICATION_TOKEN' from 1 step
echo 'SLACK_BOT_USER_OAUTH_TOKEN=<your_oauth_token>' > .env #!
echo 'SLACK_VERIFICATION_TOKEN=<your_verif_token>' >> .env #!
```

### 5.2 docker

```bash
# set `SLACK_BOT_USER_OAUTH_TOKEN` and
# `SLACK_VERIFICATION_TOKEN` in `docker-compose.yml`
docker-compose up -d
```
