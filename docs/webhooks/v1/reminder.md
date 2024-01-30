# Reminders

## Push reminder

The REMINDER_CREATED event is triggered when a reminder is sent (or pushed) to an external system. The request body (of reminder schema) is sent to the webhook URL configured for the tenant. Once the reminder is sent, the messageId can be used to track the status of the reminder.


```json
{
  "eventId" : "45645666aff54497ba804e6f1ea09929",
  "eventType" : "REMINDER_CREATED",
  "eventCreatedAt" : "2021-04-05T14:48:00.000Z",
  "reminders" : [{
    "customerExternalId" : "45645666aff54497ba804e6f1ea09929",
    "messageId" : "45645666aff54497ba804e6f1ea09929",
    "payload": {
      "title": "Please check this reminder!",
      "description": "This reminder is a sample reminder",
      "portalUrl": "https://stage-portal.peakflo.co/?token=sampletoken"
    }
  }]
}
```

Property | type | description
---------|----------|---------
 customer-id | string | The ID of the customer associated with the reminder.
 message-id | string | The unique identifier for the reminder message.
 payload | object | The payload containing details of the reminder.