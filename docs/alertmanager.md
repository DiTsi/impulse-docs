# Alertmanager

All code examples below is about [`alertmanager.yml`](https://prometheus.io/docs/alerting/latest/configuration/)

### set repeat_interval

Set sum of `repeat_interval` and `group_interval` options less than [`timeouts.firing`](https://github.com/DiTsi/impulse/blob/main/impulse.slack.yml) (default `6h`). Explanation [here](concepts.md#unknown)

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
