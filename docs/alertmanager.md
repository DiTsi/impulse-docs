# Alertmanager



## Configuration

You should set `repeat_interval` option in **Alertmanager's** config less than `firing_timeout` (see [example](https://github.com/DiTsi/impulse/blob/develop/impulse.yml.default) file). Explanation [here](theory.md#unknown).

## Migrate from Alertmanager

1. Routes
You can use block `route:` from `alertmanager.yml` to configure **IMPulse** routes the similar way.

Just copy full `route:` block from `alertmanager.yml` to `impulse.yml` and change all `receiver` to `chain` and `channel`.

`IMPulse` will ignore all `continue` and `group_interval` instructions. You can remove them all.
