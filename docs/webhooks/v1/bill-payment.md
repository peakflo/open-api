# Bill Payment

## Bill Payment Created

The BILL_PAYMENT_CREATED event is triggered when bill payment created in peakflo. The request body looks like this

```json
{
  "eventId" : "45645666aff54497ba804e6f1ea09929",
  "eventType" : "BILL_PAYMENT_CREATED",
  "eventCreatedAt" : "2021-04-05T14:48:00.000Z",
  "dataType": "BILL_PAYMENT",
  "data": [
    {
      "externalId": "80d6616d-4c5c-4634-9937-2c2aba1fe5eb",
      "billExternalId": "bill-external-id-1",
      "vendorExternalId": "VENDOR001",
      "date": "2024-01-01T00:00:00Z",
      "amount": 550,
      "currency": "SGD",
      "status": "draft"
    },
  ]
}
```

| Property       | Type    | Description                                                  |
|----------------|---------|--------------------------------------------------------------|
| externalId | string  | An external ID associated with the bill payment.                       |
| billExternalId | string  | An external ID associated with the bill.                       |
| vendorExternalId | string  | The external ID of the vendor associated with the bill.                 |
| date     | string  | the date which payment record created.                                       |
| amount       | number  | The total amount of bill payment.              |
| currency       | string  | currency of bill payment.              |
| status         | string  | The status of the bill. [Possible Values](#possible-bill-payment-status-values)      |


### Possible Bill Payment Status Values

```json
[
 "draft",
 "paid",
]
```