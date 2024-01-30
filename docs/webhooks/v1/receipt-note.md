# Receipt Notes

## Receipt note updated

The RN_UPDATED event is triggered when an existing receipt note is updated. The request body looks like this


```json
{
  "eventId" : "45645666aff54497ba804e6f1ea09929",
  "eventType" : "RN_UPDATED",
  "eventCreatedAt" : "2021-04-05T14:48:00.000Z",
  "receiptNotes": [{
    "externalId": "12345",
    "receiptNoteNumber": "RN2023",
    "deliveryDate": "2023-11-28",
    "attachments": [
      {
        "id": "att1",
        "name": "receipt_image.jpg",
        "contentType": "image/jpeg",
        "fileSize": 1024,
        "base64": "base64_encoded_string"
      },
      {
        "id": "att2",
        "name": "receipt_pdf.pdf",
        "contentType": "application/pdf",
        "fileSize": 2048,
        "base64": "base64_encoded_string"
      }
    ],
    "items": [
      {
        "itemId": "item1",
        "name": "Product A",
        "unit": "piece",
        "description": "Description of Product A",
        "quantity": 5,
        "unitPrice": 10.5,
        "accountId": "acc123",
        "wht": {
          "id": "wht1",
          "referenceId": "ref123",
          "code": "WHT_CODE",
          "displayName": "Withholding Tax",
          "amount": 5.25
        },
        "taxes": [
          {
            "externalId": "tax1",
            "name": "Sales Tax",
            "amount": 2.10,
            "priceIncludesTax": true,
            "amountType": "percentage",
            "perc": 10
          }
        ],
        "discounts": [
          {
            "externalId": "disc1",
            "name": "Discount A",
            "amount": 1.50,
            "amountType": "fixed"
          }
        ]
      },
      {
        "itemId": "item2",
        "name": "Product B",
        "unit": "box",
        "description": "Description of Product B",
        "quantity": 2,
        "unitPrice": 20.75,
        "accountId": "acc456",
        "wht": {
          "id": "wht2",
          "referenceId": "ref456",
          "code": "WHT_CODE",
          "displayName": "Withholding Tax",
          "amount": 6.22
        },
        "taxes": [
          {
            "externalId": "tax2",
            "name": "VAT",
            "amount": 5.25,
            "priceIncludesTax": true,
            "amountType": "percentage",
            "perc": 10
          }
        ],
        "discounts": []
      }
    ],
    "purchaseOrder": "PO123",
    "vendorId": "vendorXYZ",
    "receiptNoteAmount": 76.25,
    "totalAmount": 78.75,
    "totalTax": 7.35,
    "totalWHT": 11.47,
    "currency": "USD",
    "status": "completed",
    "notes": "This is a sample receipt note.",
    "fxRate": 1.25,
    "convertedAmount": 97.5,
    "customFields": [
      {
        "id": "d4lkrdgj34ojtwlekdfj",
        "customFieldNumber": "customfield2",
        "name": "Test field name",
        "type": "string",
        "sourceId": "asg4sgs4g",
        "value": "Test Value",
      }
    ]
  }]
}
```

| Property             | Type    | Description                                                  |
|----------------------|---------|--------------------------------------------------------------|
| externalId           | string  | The external identifier for the receipt note.                  |
| receiptNoteNumber    | string  | The unique identifier for the receipt note.                   |
| deliveryDate         | string  | The date of receipt delivery.                                  |
| attachments          | array   | An array containing details of attachments for the receipt note.|
| items                | array   | An array containing details of items in the receipt note.       |
| purchaseOrder        | string  | The associated purchase order id.                          |
| vendorId             | string  | The ID of the vendor associated with the receipt note.         |
| receiptNoteAmount    | number  | The total amount of the receipt note.                          |
| totalAmount          | number  | The total amount including taxes, discounts, etc.              |
| totalTax             | number  | The total tax amount applied in the receipt note.              |
| totalWHT             | number  | The total withholding tax amount applied in the receipt note.  |
| currency             | string  | The currency used for the receipt note.                        |
| status               | string  | The current status of the receipt note. [Possible Values](#possible-rn-statuses)     |
| notes                | string  | Additional notes or details about the receipt note.            |
| fxRate               | number  | The foreign exchange rate applied.                             |
| convertedAmount      | number  | The amount after currency conversion.                          |
| customFields         | array   | An array containing details of custom fields. [Custom Field Schema](./common-schema.md#custom-field)                 |


### Possible RN Statuses

```json
[
  "draft",
  "submitted",
  "approved",
  "billed",
  "deleted",
  "cancelled",
]
```