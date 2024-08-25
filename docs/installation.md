# Installation

## get

There are two ways to run IMPulse: python or docker. Select one of these

### python

use `<release_tag>` from [here](https://github.com/DiTsi/impulse/releases)

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

don't forget to replace `<release_tag>` in `docker-compose.yml` to one of [release tags](https://github.com/DiTsi/impulse/releases)

## configure

Follow instructions in [Configuration](configuration.md#impulse)

## run

### python

```bash
gunicorn -w 1 -b 127.0.0.1:5000 'wsgi:app'
```

### docker

```bash
docker-compose up -d
```
