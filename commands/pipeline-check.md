---
name: pipeline-check
description: Validates NATS/n8n pipeline configurations and message flows
---

Analyze and validate event-driven pipeline configurations.

## Checks to Perform

1. **NATS Configuration**
   - Stream definitions exist and are valid
   - Consumer configs have appropriate ack policies
   - Subject naming follows conventions
   - Retention policies are set correctly

2. **n8n Workflows**
   - Webhook endpoints are secured
   - Error handling nodes are present
   - Credentials are not hardcoded
   - Retry logic is configured

3. **Message Flow**
   - Trace message path from producer to consumer
   - Identify potential bottlenecks
   - Check for message loss scenarios
   - Verify ordering guarantees if required

4. **Integration Points**
   - API endpoints are documented
   - Schema contracts are defined
   - Version compatibility is maintained

Start by identifying pipeline configuration files in the project.
