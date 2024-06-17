# Webhooks

Webhooks used to send POST HTTP requests in

## Examples

### Example for Twilio calls

You can configure webhook to call using Twilio service

Configure `impulse.yml` like:
```yaml
webhooks:
  Oleg:
    url: "https://api.twilio.com/2010-04-01/Accounts/{{ env['TWILIO_ACCOUNT_SID'] }}/Calls.json"
    data:
      To: '+998xxxxxxxxx'
      From: "{{ env['TWILIO_NUMBER'] }}"
      Url: http://example.com/twiml.xml
    user: "{{ env['TWILIO_ACCOUNT_SID'] }}:{{ env['TWILIO_AUTH_TOKEN'] }}"
```

and set environment variables:
```
TWILIO_ACCOUNT_SID=<xxxxxxxxxxxxx>
TWILIO_AUTH_TOKEN=<xxxxxxxxxxxxx>
TWILIO_NUMBER=+<xxxxxxxxxxxxx>
```
