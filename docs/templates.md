# Templates

Incident message contains three parts ([picture](concepts.md/#structure)):

- status icons
- header
- body

They forms by [templates](https://github.com/DiTsi/impulse/tree/main/templates) for every messenger. And you can customize it in `impulse.yml` by `application.template_files` settings.

## Features

### Special words

In template files you can use special words `incident` and `payload` as variables to show additional info:

- `incident` contains [incident attributes](https://github.com/DiTsi/impulse/blob/release/v1.2.0/app/incident/incident.py#L20).
- `payload` is an Alertmanager alerts payload

### Source and runbook links

<p align="center"><img src="../media/links.png" alt="" width="400"/></p>

Our default templates have **source** for Prometheus expression <!--?--> link and **runbook** for alert runbook link.

To use **runbook** just add `runbook` to your alert `annotations`.
