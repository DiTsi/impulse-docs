# Theory

IMPulse installed between [Alertmanager](alertmanager.md) and one of [Instant Messaging Apps](apps.md).

## Incident statuses

![None](media/incident_behavior.excalidraw.svg)

Alertmanager sends alerts with one of two statuses: **firing** and **resolved**. Of course, first status always **firing** when problem occurs. Based on these statuses IMPulse creates Incidents (message representation of alert with actual status).

Unlike of Alertmanager alerts, IMPulse Incidents may have 4 statuses: **firing**, **resolved**, **unknown**, **closed**.

### firing and resolved

Incident change status to **firing** and **resolved** based on Alertmanager's alerts statuses sent to IMPulse.

### unknown

What is **unknown**. Alertmanager has `repeat_interval` value which force Alertmanager to sent actual alert status even if it didn't changed. IMPulse has `timeouts.firing` value during which alert status should updates. And if `repeat_interval` more than `timeouts.firing` Incident switch to non-actual status which named **unknown**.

There are two reasons for this. First, IMPulse was down when Alertmanager sends actual alert status. Second, Alertmanager don't send status during `timeouts.firing`.

When Incident become **unknown** IMPulse send warning message to admin_channel.

If reason for problem was first - admins should know it. It reason was second, you should check that Alertmanager's `repeat_interval` is less than IMPulse's `timeouts.firing`. I recommend set it 1.5 times lower.

### closed

What is **closed** Incident. As it sounds it is Incident which already didn\`t handle by IMPulse. There are two ways how it can be closed. First, **resolved** Incident stays in this status for `timeouts.resolved` time. Second, **unknown** Incidents stays in this status for `timeouts.unknown` time.
