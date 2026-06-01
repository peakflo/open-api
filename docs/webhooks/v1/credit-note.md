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
      "vendorExternalId": "VEND001",
      "vendorName": "Acme Trading LLC",
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
      "items": [
        {
          "externalId": "ITEM001",
          "unit": "ea",
          "sourceInventoryId": "ITEM001",
          "name": "Returned Goods",
          "description": "Returned Goods",
          "quantity": 2,
          "unitPrice": 300,
          "account": "Sales Returns",
          "accountId": "acc_001",
          "type": "Service",
          "taxes": [
            {
              "name": "GST",
              "amount": 54,
              "priceIncludesTax": false,
              "status": "active",
              "externalId": "tax_001",
              "amountType": "Percentage",
              "category": "GST",
              "perc": 9
            }
          ],
          "discounts": [
            {
              "name": "Promo Discount",
              "amount": 12.5,
              "status": "active",
              "issuerId": "test-issuer"
            }
          ],
          "customFields": [
            {
              "sourceId": "LocationCode",
              "value": "WH-001",
              "customFieldNumber": "1",
              "name": "Location Code",
              "type": "Input"
            }
          ],
          "purchaseOrderExternalId": "",
          "poItemExternalId": "",
          "PONumber": ""
        }
      ],
      "appliedItems": [
        {
          "billExternalId": "35b97bee-2f05-4c09-9f74-0916d7554de5",
          "billSourceId": "bill_01J9VJ0J9Q8R7S6T5U4V3W2X1Y",
          "billNumber": "BILL-2026-0004",
          "amount": 600
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
| vendorExternalId | string | The external ID of the vendor associated with the credit note. |
| vendorName | string | The name of the vendor. |
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
| items | array | An array containing item level details on the credit note. |
| appliedItems | array | An array containing bill application details for the credit note. |
| attachments | array | An array containing details of attachments related to the credit note. |
| status | string | The status of the credit note. [Possible Values](#possible-credit-note-status-values) |
| submittedAt | string | The datetime when the credit note was submitted. |
| approvedOn | string | The datetime when the credit note was approved. |
| createdByName | string | The name of the user who created the credit note. |
| createdAt | string | The datetime when the credit note was created. |
| updatedAt | string | The datetime when the credit note was last updated. |

### Item Object

| Property | Type | Description |
|----------|------|-------------|
| externalId | string | The external ID of the item line. |
| unit | string | The unit for the item. |
| sourceInventoryId | string | The inventory item identifier from the source system. |
| name | string | The item name. |
| description | string | The item description. |
| quantity | number | The item quantity. |
| unitPrice | number | The item unit price. |
| account | string | The account name for the item line. |
| accountId | string | The account identifier for the item line. |
| type | string | The item type. |
| taxes | array | Taxes applied to the item line. |
| discounts | array | Discounts applied to the item line. |
| customFields | array | Custom fields attached to the item line. |
| purchaseOrderExternalId | string | The related purchase order external ID. |
| poItemExternalId | string | The related purchase order item external ID. |
| PONumber | string | The related purchase order number. |

### Applied Item Object

| Property | Type | Description |
|----------|------|-------------|
| billExternalId | string | The external ID of the applied bill. |
| billSourceId | string | The source ID of the applied bill. |
| billNumber | string | The bill number of the applied bill. |
| amount | number | The applied amount in source currency. |

### Possible Credit Note Status Values

```json
[
  "processing",
  "active"
  "cancelled",
]
```
