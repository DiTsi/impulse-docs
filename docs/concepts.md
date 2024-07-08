# Concepts

IMPulse installed between Alertmanager and one of [instant messaging apps](apps.md).

![None](media/impulse.excalidraw.svg)

It get's alerts from Alertmanager and send it to [instant messaging app](apps.md) channel based on `application` and `route` [configuration](install_and_configure.md#42-impulseyml).

Alertmanager sends alerts with one of two statuses: **firing** and **resolved**. Of course, first status always **firing** when problem occurs. Based on these statuses IMPulse create Incidents.

<img src="../media/slack_firing.png" alt="" width="400"/>

## Incident

Incident is a message representation of alert with actual status.

and user notifications in message thread based on [application.chains](https://github.com/DiTsi/impulse/blob/main/impulse.yml.slack). You can modify Incident format using [application.message_template](https://github.com/DiTsi/impulse/blob/main/impulse.yml.slack).

Unlike of Alertmanager alerts, IMPulse Incidents may have 4 statuses: **firing**, **resolved**, **unknown**, **closed**.

### Statuses and their colors

#### firing and resolved

<img src="../media/slack_firing.png" alt="" width="400"/> <img src="../media/slack_resolved.png" alt="" width="400"/>

Incident change status to **firing** and **resolved** based on Alertmanager's alerts statuses sent to IMPulse.

#### unknown

<img src="../media/slack_unknown.png" alt="" width="400"/>

What is **unknown**. Alertmanager has `repeat_interval` value which force Alertmanager to sent actual alert status even if it didn't changed. IMPulse has [`timeouts.firing`](https://github.com/DiTsi/impulse/blob/main/impulse.yml.slack) value during which alert status should updates. And if `repeat_interval` more than [`timeouts.firing`](https://github.com/DiTsi/impulse/blob/main/impulse.yml.slack) Incident switch to non-actual status which named **unknown**.

There are two reasons for this. First, IMPulse was down when Alertmanager sends actual alert status. Second, Alertmanager don't send status during `timeouts.firing`.

When Incident become **unknown** IMPulse send warning message to admin_channel.

If reason for problem was first - admins should know it. It reason was second, you should check that Alertmanager's `repeat_interval` is less than IMPulse's `timeouts.firing`. I recommend set it 1.5 times lower.

#### closed

<img src="../media/slack_closed.png" alt="" width="400"/>

What is **closed** Incident. As it sounds it is Incident which already didn\`t tracks by IMPulse. There are two ways how it can be closed. First, **resolved** Incident stays in this status for `timeouts.resolved` time. Second, **unknown** Incidents stays in this status for `timeouts.unknown` time.


### Lifecycle

![None](media/incident_behavior.excalidraw.svg)

Incident is created with status **firing** and stop tracing after status **closed**. You can see all the options for each status and notification

![None](media/incident_firing.excalidraw.svg)

![None](media/incident_unknown.excalidraw.svg)

![None](media/incident_resolved.excalidraw.svg)
