# Bills

## Bill updated

The BILL_UPDATED event is triggered when an existing bill is updated. The request body looks like this


```json
{
  "billNumber": "BILL12345",
  "status": "paid",
  "billExternalId": "123456789",
  "paymentId": "PAY789",
  "vendorId": "VENDOR001",
  "vendorName": "ABC Vendor",
  "date": "2023-11-27T12:00:00Z",
  "dueDate": "2023-12-15T23:59:59Z",
  "scheduledDate": "2023-12-10T00:00:00Z",
  "attachments": [
    {
      "id": "attachment_id_1",
      "name": "Attachment 1",
      "contentType": "application/pdf",
      "fileSize": 1024,
      "base64": "Base64EncodedContent1"
    }
  ],
  "currency": "USD",
  "subTotal": 500,
  "totalTax": 50,
  "paymentAmount": 450,
  "totalAmount": 550,
  "notes": "This is a test bill",
  "billPaymentId": "BP789",
  "totalWHT": 20,
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
        "id": "WHT001",
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
  "receiptDate": "2023-11-28T00:00:00Z",
  "paymentMadeDate": "2023-12-05T12:30:00Z"
}
```

| Property       | Type    | Description                                                  |
|----------------|---------|--------------------------------------------------------------|
| billNumber     | string  | The unique identifier for the bill.                           |
| status         | string  | The status of the bill (e.g., paid, pending, overdue).        |
| billExternalId | string  | An external ID associated with the bill.                       |
| paymentId      | string  | The unique identifier for the payment related to the bill.     |
| vendorId       | string  | The ID of the vendor associated with the bill.                 |
| vendorName     | string  | The name of the vendor.                                       |
| date           | string  | The date the bill was generated.                              |
| dueDate        | string  | The due date for payment of the bill.                          |
| scheduledDate  | string  | The scheduled payment date.                                   |
| attachments    | array   | An array containing details of attachments related to the bill.|
| currency       | string  | The currency used for the bill.                                |
| subTotal       | number  | The subtotal amount of the bill.                              |
| totalTax       | number  | The total tax amount applied to the bill.                      |
| paymentAmount  | number  | The amount paid for the bill.                                  |
| totalAmount    | number  | The total amount including tax and other charges.              |
| notes          | string  | Additional notes or description about the bill.                |
| billPaymentId  | string  | The ID associated with the bill payment.                       |
| totalWHT       | number  | The total amount of withholding tax for the bill.              |
| items          | array   | An array containing details of items listed on the bill.       |
| receiptDate    | string  | The date when the bill receipt was generated.                  |
| paymentMadeDate| string  | The date when the payment for the bill was made.               |
| updatedAt      | string  | The date when the bill was update.                             |


## Bill Status Changed

The BILL_STATUS_CHANGED event is triggered when the status of a bill changes. The request body looks like this

```json
{
  "billNumber": "BILL12345",
  "status": "approved",
  "previousStatus": "submitted",
  "billExternalId": "123456789",
  "vendorId": "VENDOR001",
  "vendorName": "ABC Vendor",
  "date": "2023-11-27T12:00:00Z",
  "dueDate": "2023-12-15T23:59:59Z",
  "scheduledDate": "2023-12-10T00:00:00Z",
  "attachments": [
    {
      "id": "attachment_id_1",
      "name": "Attachment 1",
      "contentType": "application/pdf",
      "fileSize": 1024,
      "base64": "Base64EncodedContent1"
    }
  ],
  "currency": "USD",
  "subTotal": 500,
  "totalTax": 50,
  "totalAmount": 550,
  "notes": "This is a test bill",
  "totalWHT": 20,
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
        "id": "WHT001",
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
  "receiptDate": "2023-11-28T00:00:00Z"
}
```

| Property       | Type    | Description                                                  |
|----------------|---------|--------------------------------------------------------------|
| billNumber     | string  | The unique identifier for the bill.                           |
| status         | string  | The status of the bill.        |
| previousStatus         | string  | The previous status of the bill.        |
| billExternalId | string  | An external ID associated with the bill.                       |
| vendorId       | string  | The ID of the vendor associated with the bill.                 |
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