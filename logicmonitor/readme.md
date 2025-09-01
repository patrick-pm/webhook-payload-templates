# Cisco Meraki Webhook Payload Template for LogicMonitor

This template enables Cisco Meraki webhooks to integrate with [LogicMonitor](https://www.logicmonitor.com) LM Logs.

## Files
- `body.liquid` – Defines the JSON body of the webhook payload.
- `headers.liquid` – Defines any custom headers required by the LogicMonitor ingest endpoint.

## Usage
1. Generate a Bearer Token from your LogicMonitor Portal
2. Import the template into the Meraki Dashboard:
   - Go to **Organization → Settings → Webhooks → Payload Templates**.
   - Click **New Template** and paste the contents of `body.liquid` and `headers.liquid`.
  
3. Add a new Receiver via
   - Go to **Organization → Settings → Webhooks → Receivers -> Add Receiver**.
   - Give your Receiver a name, like "My LogicMonitor Portal Name + Optional Tenant Name"
   - Enter your portal webhook reveiver URL, like "https://myportalname.logicmonitor.com/rest/api/v1/webhook/ingest/meraki:
   - Paste your LogicMonitor Bearer Token into the "Shared Secret Field"
   - Select your LogicMonitor Payload Template and Save.
  
4. Add this Receiver to the desired Meraki Networks via
 - Go to **Organization → Network Name → Network Wide → Alerts**.

## Example Header
```json
{
  "Authorization": "Bearer {{sharedSecret}}"
}
```

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
```
