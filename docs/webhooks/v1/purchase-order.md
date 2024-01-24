# Purchase Orders

## Purchase order updated

The PO_UPDATED event is triggered when an existing purchase order is updated. The request body looks like this


```json
{
  "totalAmount": 1500,
  "POAmount": 2000,
  "totalWHT": 100,
  "paidAmount": 1200,
  "balanceAmount": 300,
  "currency": "USD",
  "issueDate": "2023-10-15",
  "dueDate": "2023-11-30",
  "notes": "This is a sample note for the transaction.",
  "deliveryInstructions": "Deliver to address XYZ.",
  "status": "pending",
  "totalTax": 250,
  "fxRate": 1.2,
  "convertedAmount": 1800,
  "attachments": [
    {
      "id": "attachment_1",
      "name": "Invoice_001.pdf",
      "contentType": "application/pdf",
      "fileSize": 1024,
      "base64": "Base64EncodedContent1"
    },
    {
      "id": "attachment_2",
      "name": "Receipt_001.pdf",
      "contentType": "application/pdf",
      "fileSize": 2048,
      "base64": "Base64EncodedContent2"
    }
  ],
  "items": [
    {
      "itemId": "item_001",
      "name": "Product A",
      "unit": "unit",
      "description": "Description for Product A",
      "quantity": 5,
      "unitPrice": 300,
      "accountId": "ACC001",
      "wht": {
        "id": "WHT001",
        "referenceId": "REF001",
        "code": "WHT_CODE",
        "displayName": "Withholding Tax",
        "amount": 50
      },
      "taxes": [
        {
          "externalId": "TAX001",
          "name": "Sales Tax",
          "amount": 200,
          "priceIncludesTax": true,
          "amountType": "percentage",
          "perc": 10
        }
      ],
      "discounts": [
        {
          "externalId": "Discount001",
          "name": "Volume Discount",
          "amount": 50,
          "amountType": "percentage"
        }
      ]
    },
    {
      "itemId": "item_002",
      "name": "Product B",
      "unit": "unit",
      "description": "Description for Product B",
      "quantity": 3,
      "unitPrice": 250,
      "accountId": "ACC002",
      "wht": {
        "id": "WHT002",
        "referenceId": "REF002",
        "code": "WHT_CODE",
        "displayName": "Withholding Tax",
        "amount": 30
      },
      "taxes": [
        {
          "externalId": "TAX002",
          "name": "VAT",
          "amount": 50,
          "priceIncludesTax": false,
          "amountType": "fixed",
          "perc": 0
        }
      ],
      "discounts": [
        {
          "externalId": "Discount002",
          "name": "New User Discount",
          "amount": 20,
          "amountType": "percentage"
        }
      ]
    }
  ],
  "PONumber": "PO123456",
  "PQNumber": "PQ789012",
  "vendorId": "VENDOR001",
  "receiptDate": "2023-11-05",
  "deliveryDate": "2023-11-20",
  "bills": ["BILL001", "BILL002"],
  "receiptNotes": ["Received partial payment.", "Customer requested additional items."],
  "balanceQuantity": 7
}
```

| Property             | Type    | Description                                                  |
|----------------------|---------|--------------------------------------------------------------|
| totalAmount          | number  | The total amount for the purchase order.                         |
| POAmount             | number  | The total purchase order amount.                              |
| totalWHT             | number  | The total withholding tax amount.                             |
| paidAmount           | number  | The amount already paid.                                      |
| balanceAmount        | number  | The remaining balance amount.                                 |
| currency             | string  | The currency used for the purchase order.                        |
| issueDate            | string  | The date when the purchase order was issued.                     |
| dueDate              | string  | The due date for the purchase order.                              |
| notes                | string  | Additional notes or details about the purchase order.             |
| deliveryInstructions | string  | Specific instructions for delivery.                            |
| status               | string  | The current status of the purchase order.                         |
| totalTax             | number  | The total tax amount applied.                                 |
| fxRate               | number  | The foreign exchange rate applied.                            |
| convertedAmount      | number  | The amount after currency conversion.                         |
| attachments          | array   | An array containing details of attachments for the purchase order.|
| items                | array   | An array containing details of line items in the purchase order|
| PONumber             | string  | The purchase order number.                                    |
| PQNumber             | string  | The purchase quote number.                                |
| vendorId             | string  | The ID of the vendor associated with the purchase order.          |
| receiptDate          | string  | The date when the receipt was generated.                      |
| deliveryDate         | string  | The expected delivery date.                                   |
| bills                | array   | An array containing IDs of bills.             |
| receiptNotes         | array   | An array containing receipt notes id.                  |
| balanceQuantity      | number  | The remaining quantity.                              |

