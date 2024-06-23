# Installation and Configuration

## 1 Create Slack bot

Instuction [here](apps.md#slack)

## 2 Configure Alertmanager

### 2.1 set repeat_interval

In Alertmanager's config file `alertmanager.yml` you should set `repeat_interval` option less than `timeouts.firing` (default `6h`). Explanation [here](concepts.md#unknown).

Example:

```yaml
route:
  repeat_interval: 4h
  ...
```

### 2.2 modify receiver

Set IMPulse as default recever

```yaml
receivers:
- name: 'impulse'
  webhook_configs:
  - url: 'http://<impulse_host>:<impulse_port>/'

route:
  receiver: 'impulse'
  ...
```

### 2.3 routing

IMPulse `route` very similar to Alertmanager's but simpler. Instead of Alertmanager's it has only four instructions: `routes`, `matchers`, `channel`, `chain`.

When using IMPulse as the only one incident manager, you can move all your [`route`](https://prometheus.io/docs/alerting/latest/configuration/#route) block from `alertmanager.yml` to `impulse.yml`. Don't forget to remove all unused instructions and change all `receiver` instrustions to `chain` and `channel`. Fill it right.

## 3 Get

There are two ways to run IMPulse: Python and Docker.

### 3.1 Python

```bash
git clone git@github.com:DiTsi/impulse.git impulse
cd impulse
cp impulse.yml.default impulse.yml
```

### 3.2 Docker

```bash
mkdir impulse
mkdir impulse/config
mkdir impulse/data
cd impulse
wget https://github.com/DiTsi/impulse/blob/develop/docker-compose.yml
wget https://github.com/DiTsi/impulse/blob/develop/impulse.yml.default config/impulse.yml
```

## 4 Configure

You should set two ENVs `SLACK_BOT_USER_OAUTH_TOKEN`, `SLACK_VERIFICATION_TOKEN` (pt. 4.1) and modify `impulse.yml` (pt. 4.2)

### 4.1 Environment variables

| Variable | Description | Default |
|-|-|-|
| DATA_PATH | Path to data directory | ./data |
| CONFIG_PATH | Path to `impulse.yml` directory | ./ |
| SLACK_BOT_USER_OAUTH_TOKEN | Slack Bot User OAuth Token | |
| SLACK_VERIFICATION_TOKEN | Slack Verification Token | |

### 4.2 impulse.yml

`impulse.yml.default` has minimal configuration IMPulse can start with. All additional settings commented out.

On the root level configuration has these blocks:
```
timeouts:
route:
application:
webhooks:
```

#### 4.2.1 Timeouts

`timeouts` have 3 options: `firing`, `unknown`, `resolved`. See  [unknown](concepts.md#unknown) and [closed](concepts.md#closed) Incident status documentation to understand.

#### 4.2.2 Route

Used for Incidents routing based on alert's fields. It made very similar to Alertmanager's [route](https://prometheus.io/docs/alerting/latest/configuration/#route).

### 4.3 Webhooks

Webhooks used to send POST HTTP requests

#### 4.3.1 Examples

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

### 4.4 Secrets

[Webhook](webhook.md) config allows you to declare custom ENVs for secrets or duplicates (see [Twilio](webhook.md#twilio) example).

## 5 Run

Use 

### 5.1 Python

```bash
# use 'SLACK_BOT_USER_OAUTH_TOKEN' and
# 'SLACK_VERIFICATION_TOKEN' from 1 step
echo 'SLACK_BOT_USER_OAUTH_TOKEN=<your_oauth_token>' > .env #!
echo 'SLACK_VERIFICATION_TOKEN=<your_verif_token>' >> .env #!
```

### 5.2 Docker

```bash
# set `SLACK_BOT_USER_OAUTH_TOKEN` and
# `SLACK_VERIFICATION_TOKEN` in `docker-compose.yml`
docker-compose up -d
```
