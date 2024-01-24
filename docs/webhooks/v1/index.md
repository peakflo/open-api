# About Peakflo Webhooks

Peakflo supports secure webhooks implementation using which clients can receive events for objects of client's interest. Please read through below for information on webhooks

## Limits


Limit type | Count | Description
---------|----------|---------
 Maximum requests per minute	 | 100 | Maximum number of requests made per account
 Maximum retries	 | 5 | Maximum number of retries for single request if the request doesnt get a success response
 Retry delay in minutes	 |  10 | Number of minutes pause between each retry

 ## Request headers

 The Request sent will include the below headers (Peakflo will share the access token ahead)


Parameter | Type | Description
---------|----------|---------
 Content-Type	 | string | application/json
 x-callback-token | string | access token

## Supported Events

For webhook payload schema and more details please go to respective pages.

- [Payments](./payment.md)
    - [Created](./payment.md#payment-created)
    - [Updated](./payment.md#payment-updated)
    - [Deleted](./payment.md#payment-deleted)
- [Reminders](./reminders.md)
    - [Created](./reminder.md) - when a reminder is created and sent
- [Bills](./bill.md)
    - [Updated](./bill.md#bill-updated)
    - [Status changed](./bill.md#bill-status-changed)
- [Purchase Orders](./purchase-order.md)
    - [Updated](./purchase-order.md#purchase-order-updated)
- [Receipt Notes](./receipt-note.md)
    - [Updated](./receipt-note.md#receipt-note-updated)

