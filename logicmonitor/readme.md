# Cisco Meraki Webhook Payload Template for LogicMonitor

This template enables Cisco Meraki webhooks to integrate with [LogicMonitor](https://www.logicmonitor.com) by forwarding events in a format LogicMonitor can ingest.

## Files
- `body.liquid` – Defines the JSON body of the webhook payload.
- `headers.liquid` – Defines any custom headers required by the LogicMonitor ingest endpoint.

## Usage
1. Import the template into the Meraki Dashboard:
   - Go to **Organization → Settings → Webhooks → Payload Templates**.
   - Click **New Template** and paste the contents of `body.liquid` and `headers.liquid`.
2. Assign the webhook template to your alert destinations.


## Example Body
```json

{
"Cisco Meraki": "{{ alertType }} alert in {{ networkName }} ({{ organizationName }}) for device {{ deviceName }}",
"alert_data": {{ alertData | jsonify }},
  "log_level": "{{ alertLevel }}",
  "timestamp": "{{ occurredAt }}",
  "sentAt": "{{ sentAt }}",
  "organizationName": "{{ organizationName }}",
  "organizationId": "{{ organizationId }}",
  "organizationUrl": "{{ organizationUrl }}",
  "networkName": "{{ networkName }}",
  "networkId": "{{ networkId }}",
  "networkUrl": "{{ networkUrl }}",
  "networkTags": {{ networkTags | jsonify }},
  "deviceName": "{{ deviceName }}",
  "deviceModel": "{{ deviceModel }}",
  "deviceSerial": "{{ deviceSerial }}",
  "deviceMac": "{{ deviceMac }}",
  "deviceUrl": "{{ deviceUrl }}",
  "deviceTags": {{ deviceTags | jsonify }},
  "alertId": "{{ alertId }}",
  "alertType": "{{ alertType }}",
  "alertTypeId": "{{ alertTypeId }}",
  "alertData": {{ alertData | jsonify }}
}
