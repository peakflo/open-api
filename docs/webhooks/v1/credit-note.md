# Credit Notes

## Credit Note Status Changed

The CREDIT_NOTE_STATUS_CHANGED event is triggered when the status of a credit note changes. The request body looks like this

```json
{
  "eventId": "45645666aff54497ba804e6f1ea09929",
  "eventType": "CREDIT_NOTE_STATUS_CHANGED",
  "eventCreatedAt": "2026-02-06T14:48:00.000Z",
  "dataType": "CREDIT_NOTE",
  "data": [
    {
      "externalId": "cn_01J9VJ4N8Q7T2Y6R3X5A9B1C2D",
      "creditNoteNumber": "CN-2026-0001",
      "customerExternalId": "CUS001",
      "customerName": "Acme Trading LLC",
      "issueDate": "2026-01-15T00:00:00.000Z",
      "note": "Credit issued for returned goods",
      "totalAmount": 963,
      "totalAmountConv": 1300.05,
      "subTotal": 1000,
      "subTotalConv": 1350,
      "remainingCredit": 363,
      "remainingCreditConv": 490.05,
      "currency": "USD",
      "currencyRate": 1.35,
      "destinationCurrency": "SGD",
      "lineItems": [
        {
          "externalId": "ITEM001",
          "invoiceExternalId": "inv_01J9VJ0J9Q8R7S6T5U4V3W2X1Y",
          "amount": 600,
          "amountConv": 810,
          "currencyRate": 1.35,
          "wht": {
            "referenceId": "REF001",
            "code": "WHT_CODE",
            "displayName": "Withholding Tax",
            "amount": 12
          }
        }
      ],
      "attachments": [
        {
          "name": "credit-note-support.pdf",
          "contentType": "application/pdf"
        }
      ],
      "status": "active",
      "submittedAt": "2026-01-21T08:40:00.000Z",
      "approvedOn": "2026-01-21T09:00:00.000Z",
      "createdByName": "Nora AR",
      "createdAt": "2026-01-15T10:00:00.000Z",
      "updatedAt": "2026-01-21T09:01:00.000Z"
    }
  ]
}
```

| Property | Type | Description |
|----------|------|-------------|
| externalId | string | An external ID associated with the credit note. |
| creditNoteNumber | string | The unique identifier for the credit note. |
| customerExternalId | string | The external ID of the customer associated with the credit note. |
| customerName | string | The name of the customer. |
| issueDate | string | The issue date of the credit note. |
| note | string | Additional note for the credit note. |
| totalAmount | number | The total amount for the credit note. |
| totalAmountConv | number | The total amount converted to destination currency. |
| subTotal | number | The subtotal amount for the credit note. |
| subTotalConv | number | The subtotal converted to destination currency. |
| remainingCredit | number | The remaining unutilized credit amount. |
| remainingCreditConv | number | The remaining credit converted to destination currency. |
| currency | string | The source currency of the credit note. |
| currencyRate | number | The exchange rate used for conversion. |
| destinationCurrency | string | The destination currency for converted amounts. |
| lineItems | array | An array containing line item level details. |
| attachments | array | An array containing details of attachments related to the credit note. |
| status | string | The status of the credit note. [Possible Values](#possible-credit-note-status-values) |
| submittedAt | string | The datetime when the credit note was submitted. |
| approvedOn | string | The datetime when the credit note was approved. |
| createdByName | string | The name of the user who created the credit note. |
| createdAt | string | The datetime when the credit note was created. |
| updatedAt | string | The datetime when the credit note was last updated. |

### Possible Credit Note Status Values

```json
[
  "processing",
  "active"
  "cancelled",
]
```
