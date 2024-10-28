# Examples

**minimal Slack configuration**

```yaml
route:
  channel: space

application:
  type: slack
  admin_users:
  - Dmitry_Tsybus
  users:
    Dmitry_Tsybus: {full_name: "Dmitry Tsybus"}
```

**minimal Mattermost configuration**

```yaml
url: https://impulse.yourdomain.com # IMPulse URL where Mattermost will send buttons events (we'll move it in v2.0.0)

route:
  channel: space

application:
  url: https://mattermost.yourdomain.com # your Mattermost URL (we'll move it in v2.0.0)
  type: slack
  admin_users:
  - Dmitry_Tsybus
  users:
    Dmitry_Tsybus: {username: "ditsi"}
```
