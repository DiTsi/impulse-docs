# Run

Use your installation option

## python

Environment variables created [here](apps.md)

```bash
# for Slack
echo 'SLACK_BOT_USER_OAUTH_TOKEN=<your_oauth_token>' >> .env
echo 'SLACK_VERIFICATION_TOKEN=<your_verif_token>' >> .env

# for Mattermost
echo 'MATTERMOST_ACCESS_TOKEN=<your_access_token>' >> .env

gunicorn -w 1 -b 0.0.0.0:5000 wsgi:app
```

## docker

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
