---
name: nats-patterns
description: NATS and JetStream best practices. Auto-invoked when working with NATS, JetStream, messaging, or queue-related code.
---

## NATS Development Standards

### Subject Naming Convention

```
{domain}.{entity}.{action}[.{qualifier}]

Examples:
  alarms.equipment.triggered
  alarms.equipment.acknowledged
  events.sensor.reading.temperature
  commands.hvac.setpoint.update
```

### JetStream Consumer Configuration

```javascript
// Durable consumer for reliable processing
const consumerConfig = {
  durable_name: "processor-v1",
  ack_policy: "explicit",
  ack_wait: 30_000_000_000,  // 30 seconds in nanoseconds
  max_deliver: 3,
  filter_subject: "alarms.>",
  deliver_policy: "all"
};
```

### Message Handling Pattern

```go
// Always process then ack
func handleMessage(msg *nats.Msg) error {
    // 1. Parse message
    var event Event
    if err := json.Unmarshal(msg.Data, &event); err != nil {
        // Permanent failure - nak with no redelivery
        msg.Term()
        return err
    }
    
    // 2. Process with idempotency check
    if processed, _ := cache.Get(event.ID); processed {
        msg.Ack()
        return nil
    }
    
    // 3. Do work
    if err := processEvent(event); err != nil {
        // Transient failure - will be redelivered
        msg.Nak()
        return err
    }
    
    // 4. Mark complete
    cache.Set(event.ID, true, 24*time.Hour)
    msg.Ack()
    return nil
}
```

### Dead Letter Queue Pattern

```javascript
// Configure DLQ stream
const dlqStream = {
  name: "DLQ",
  subjects: ["$JS.EVENT.ADVISORY.CONSUMER.MAX_DELIVERIES.>"],
  retention: "limits",
  max_msgs: 10000
};
```

### Common Anti-Patterns to Avoid

❌ Acknowledging before processing
❌ Using request-reply for high-volume async work  
❌ Not setting ack_wait appropriately
❌ Ignoring consumer lag metrics
❌ Hardcoding subject names
