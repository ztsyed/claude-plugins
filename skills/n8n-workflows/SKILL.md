---
name: n8n-workflows
description: n8n workflow development patterns. Auto-invoked when working with n8n, workflow automation, or webhook integrations.
---

## n8n Development Standards

### Workflow Structure

```
[Trigger] → [Validate] → [Process] → [Route] → [Output]
                ↓
            [Error Handler]
```

### Webhook Security

```javascript
// Always validate incoming webhooks
{
  "nodes": [
    {
      "name": "Webhook",
      "type": "n8n-nodes-base.webhook",
      "parameters": {
        "authentication": "headerAuth",
        "path": "incoming-events",
        "responseMode": "onReceived"
      }
    },
    {
      "name": "Validate Signature",
      "type": "n8n-nodes-base.code",
      "parameters": {
        "jsCode": "const crypto = require('crypto');\nconst signature = $input.first().headers['x-signature'];\nconst computed = crypto.createHmac('sha256', $env.WEBHOOK_SECRET).update(JSON.stringify($input.first().body)).digest('hex');\nif (signature !== computed) throw new Error('Invalid signature');\nreturn $input.all();"
      }
    }
  ]
}
```

### Error Handling Pattern

Every workflow should have:
1. Try/catch around main logic
2. Error workflow trigger for alerting
3. Dead letter storage for failed items
4. Retry configuration for transient failures

### Workflow Versioning

```
workflows/
├── active/
│   └── process-alarms.json       # Currently deployed
├── versions/
│   ├── process-alarms.v1.json    # Previous versions
│   └── process-alarms.v2.json
└── templates/
    └── base-webhook-flow.json    # Reusable templates
```

### Environment Configuration

```javascript
// Never hardcode credentials or endpoints
{
  "parameters": {
    "url": "={{ $env.API_ENDPOINT }}/v1/alarms",
    "authentication": "predefinedCredentialType",
    "nodeCredentialType": "httpHeaderAuth"
  }
}
```
