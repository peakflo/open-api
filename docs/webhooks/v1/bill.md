# Bills

## Bill Status Changed

The BILL_STATUS_CHANGED event is triggered when the status of a bill changes. The request body looks like this

```json
{
  "eventId" : "45645666aff54497ba804e6f1ea09929",
  "eventType" : "BILL_STATUS_CHANGED",
  "eventCreatedAt" : "2021-04-05T14:48:00.000Z",
  "bills": [{
    "billExternalId": "bill-external-id-1",
    "billNumber": "BILL12345",
    "status": "approved",
    "poExternalId": "po-external-id-1",
    "poNumber": "PO001",
    "receiptNotes": [
      {
        "rnNumber": "RN001",
        "rnExternalId": "rn-external-id-1",
      }
    ],
    "totalAmount": 550,
    "subTotal": 500,
    "totalTax": 50,
    "totalWHT": 20,
    "paymentAmount": 530,
    "date": "2023-11-27T12:00:00Z",
    "dueDate": "2023-12-15T23:59:59Z",
    "receiptDate": "2023-11-28T00:00:00Z",
    "scheduledDate": "2023-12-10T00:00:00Z",
    "vendorExternalId": "VENDOR001",
    "vendorName": "ABC Vendor",
    "currency": "USD",
    "currencyRate": 1,
    "notes": "This is a test bill",
    "attachments": [
      {
        "name": "Attachment 1",
        "contentType": "application/pdf",
      }
    ],
    "items": [
      {
        "itemId": "ITEM001",
        "name": "Product A",
        "unit": "unit",
        "description": "Description for Product A",
        "quantity": 2,
        "unitPrice": 150,
        "accountId": "ACC001",
        "wht": {
          "referenceId": "REF001",
          "code": "WHT_CODE",
          "displayName": "Withholding Tax",
          "amount": 10
        },
        "taxes": [
          {
            "externalId": "TAX001",
            "name": "Sales Tax",
            "amount": 20,
            "priceIncludesTax": true,
            "amountType": "percentage",
            "perc": 5
          }
        ],
        "discounts": [
          {
            "externalId": "Discount101",
            "name": "New user discount",
            "amount": 20,
            "amountType": "percentage"
          }
        ],
        "totalTax": 20,
        "totalDiscount": 0,
        "total": 320
      }
    ],
    "customFields": [
      {
        "customFieldNumber": "customfield2",
        "name": "Test field name",
        "type": "string",
        "value": "Test Value",
      }
    ]
  }]
}
```

| Property       | Type    | Description                                                  |
|----------------|---------|--------------------------------------------------------------|
| billExternalId | string  | An external ID associated with the bill.                       |
| billNumber     | string  | The unique identifier for the bill.                           |
| status         | string  | The status of the bill. [Possible Values](#possible-bill-status-values)      |
| vendorExternalId | string  | The external ID of the vendor associated with the bill.                 |
| vendorName     | string  | The name of the vendor.                                       |
| date           | string  | The date the bill was generated.                              |
| dueDate        | string  | The due date for payment of the bill.                          |
| scheduledDate  | string  | The scheduled payment date.                                   |
| attachments    | array   | An array containing details of attachments related to the bill.|
| currency       | string  | The currency used for the bill.                                |
| subTotal       | number  | The subtotal amount of the bill.                              |
| totalTax       | number  | The total tax amount applied to the bill.                      |
| totalAmount    | number  | The total amount including tax and other charges.              |
| notes          | string  | Additional notes or description about the bill.                |
| totalWHT       | number  | The total amount of withholding tax for the bill.              |
| items          | array   | An array containing details of items listed on the bill.       |
| receiptDate    | string  | The date when the bill receipt was generated.                  |
| updatedAt      | string  | The date when the bill was update.
| customFields   | array   | An array containing details of custom fields.                 |


### Possible Bill Status Values

```json
[
 "draft",
 "processing",
 "submitted",
 "approved",
 "scheduled",
 "failed",
 "paid",
 "deleted",
 "cancelled",
]
```