# Alertmanager

## Configuration

You should set `repeat_interval` option in Alertmanager's config less than `firing_timeout` (see [example](https://github.com/DiTsi/impulse/blob/develop/impulse.yml.default) file). Explanation [here](theory.md#unknown).

## Routing

You can use block [`route:`](https://prometheus.io/docs/alerting/latest/configuration/#route) from `alertmanager.yml` to configure IMPulse [route](configuration.md#route) similar way.

Just cut full `route:` block from `alertmanager.yml`, paste to `impulse.yml` and change all `receiver` to `chain` and `channel`.

IMPulse `route` simpler than Alertmanager's. See [config example](configuration.md#config_file) will ignore all `continue` and `group_interval` instructions. You can remove them all.
