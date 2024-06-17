# Getting started

## Create Slack bot
Instuction [here](apps.md#slack)

## Run IMPulse

There are two ways to run: Python and Docker

### Python

```bash
git clone git@github.com:DiTsi/impulse.git impulse
cd impulse
cp impulse.yml.default impulse.yml
# modify impulse.yml

# use 'SLACK_BOT_USER_OAUTH_TOKEN' and
# 'SLACK_VERIFICATION_TOKEN' from 1 step
echo 'SLACK_BOT_USER_OAUTH_TOKEN=<your_oauth_token>' > .env #!
echo 'SLACK_VERIFICATION_TOKEN=<your_verif_token>' >> .env #!
```

### Docker

```bash
mkdir impulse
mkdir impulse/config
mkdir impulse/data
cd impulse
wget https://github.com/DiTsi/impulse/blob/develop/docker-compose.yml
wget https://github.com/DiTsi/impulse/blob/develop/impulse.yml.default config/impulse.yml
# set `SLACK_BOT_USER_OAUTH_TOKEN` and
# `SLACK_VERIFICATION_TOKEN` in `docker-compose.yml`
docker-compose up -d
```
