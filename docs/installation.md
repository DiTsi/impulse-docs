# Installation

## get

There are two ways to run IMPulse: python or docker. Select one of these:

### python

Use `<release_tag>` from [here](https://github.com/DiTsi/impulse/releases) and do:

```bash
git clone --branch <release_tag> --single-branch git@github.com:DiTsi/impulse.git impulse
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

don't forget to replace `<release_tag>` in `docker-compose.yml` to one of the [release tags](https://github.com/DiTsi/impulse/releases).

## configure

See [Configuration](configuration.md#impulse).

## run

Use your installation option

### python

Environment variables created [here](apps.md)

```bash
# for Slack
echo 'SLACK_BOT_USER_OAUTH_TOKEN=<your_oauth_token>' >> .env
echo 'SLACK_VERIFICATION_TOKEN=<your_verif_token>' >> .env

# for Mattermost
echo 'MATTERMOST_ACCESS_TOKEN=<your_access_token>' >> .env

gunicorn -w 1 -b 0.0.0.0:5000 wsgi:app
```

### docker

Set environment variables

```yaml
# for Slack
SLACK_BOT_USER_OAUTH_TOKEN
SLACK_VERIFICATION_TOKEN

# for Mattermost
MATTERMOST_ACCESS_TOKEN
```

in `docker-compose.yml` and run IMPulse:

```bash
docker-compose up -d
```
