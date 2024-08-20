# Webhooks

## Examples

### Twilio calls example

1. Configure `webhooks` in `impulse.yml` that way:
        
        webhooks:
          Dmitry_call:
            url: "https://api.twilio.com/2010-04-01/Accounts/{{ env['TWILIO_ACCOUNT_SID'] }}/Calls.json"
            data:
              To: '+998xxxxxxxxx'
              From: "{{ env['TWILIO_NUMBER'] }}"
              Url: http://example.com/twiml.xml
            auth: "{{ env['TWILIO_ACCOUNT_SID'] }}:{{ env['TWILIO_AUTH_TOKEN'] }}"

2. Add custom environment variables in `.env` or `docker-compose.yml`:

        TWILIO_ACCOUNT_SID
        TWILIO_AUTH_TOKEN
        TWILIO_NUMBER

### Zvonok.com calls example

1. Configure `webhooks` in `impulse.yml` that way:

        webhooks:
          Dmitry_call:
            url: "https://zvonok.com/manager/cabapi_external/api/v1/phones/call/"
            data:
              campaign_id: '{{ env["ZVONOK_CAMPAIGN_ID"] }}'
              phone: '+998xxxxxxxxx'
              public_key: '{{ env["ZVONOK_PUBLIC_KEY"] }}'

2. Add custom environment variables in `.env` or `docker-compose.yml`:

        ZVONOK_CAMPAIGN_ID
        ZVONOK_PUBLIC_KEY
