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

- [Bills](./bill.md)
    - [Status changed](./bill.md#bill-status-changed)
- [Credit Notes](./credit-note.md)
    - [Status changed](./credit-note.md#credit-note-status-changed)

## Webhook responses

For bill and credit-note webhooks, return `Content-Type: application/json` with a **JSON array of result objects** as the HTTP response body, including when the request contains only one item. Return one result for each item in the request's `data` array so Peakflo can record its sync outcome, external-system ID, and details.

### Response fields

| Field | Type | Required | Description |
|-------|------|----------|-------------|
| `externalId` | string | Yes | Non-blank identifier matching the request item. For bills, echo `data[].billExternalId`; for credit notes, echo `data[].externalId`. Copy the value exactly, including case. |
| `status` | string | Yes | `success` or `error` (case-insensitive, without surrounding whitespace). This field determines the item's sync outcome. |
| `sourceId` | string | On success | Non-blank ID of the record in your system, such as a document number. Numbers must be encoded as strings. For an error, this may be omitted, `null`, or a string. |
| `errorMessage` | string or null | No | Human-readable failure reason. Provide it for errors; omit it or use `null` for success. |
| `details` | string, object, array, or null | No | Additional processing details. Strings are preserved; objects and arrays are JSON-serialized for sync details. Omit or use `null` when unavailable. |

Additional fields, such as `statusCode` or `sapStatusCode`, may appear in the saved response but do not determine sync success. A `success` result still requires a non-blank string `sourceId`; a numeric `statusCode: 200` alone is not enough.

### Successful response

For a bill request with `billExternalId: "BILL-001"`, respond with HTTP `200` and this body:

```json
[
  {
    "externalId": "BILL-001",
    "status": "success",
    "sourceId": "DOC-1001",
    "errorMessage": null,
    "details": "Document DOC-1001 posted successfully."
  }
]
```

### Failed response

For a bill that your system could not process, return a matching error result, for example with HTTP `400`:

```json
[
  {
    "externalId": "BILL-001",
    "status": "error",
    "sourceId": null,
    "errorMessage": "The account is not configured for this company.",
    "details": {
      "accountId": "ACCOUNT-001",
      "companyCode": "COMPANY-001"
    }
  }
]
```

### Batches and matching

A batch can contain both successes and errors. For example, the following is a valid response body with HTTP `400` when one bill failed:

```json
[
  {
    "externalId": "BILL-001",
    "status": "success",
    "sourceId": "DOC-1001"
  },
  {
    "externalId": "BILL-002",
    "status": "error",
    "errorMessage": "The vendor is not configured."
  }
]
```

- For a valid structured response, Peakflo uses each matched result's `status` regardless of the HTTP status: `success` completes that item's sync, and `error` fails it. In the example above, `BILL-001` succeeds despite HTTP `400`.
- Results are matched by identifier, not array position. Echo the request's ID rather than substituting a bill number or a newly generated ID. Send each requested item exactly once.
- For compatibility, bill matching also supports a legacy request `externalId`. Credit-note matching falls back from `externalId` to an exact `creditNoteNumber`. Both can fall back to a response `sourceId` matching the request's existing `sourceId`. Echoing the primary external ID is the recommended contract.
- A requested item with no matching result is marked failed without automatic retry, even if other results succeed. An empty array therefore fails all requested items; unrelated response rows are ignored.

### Invalid bodies and HTTP fallback

Every result must satisfy the response-field rules. If any result is invalid, the **entire body** falls back to legacy HTTP handling: HTTP `200` completes all items without extracting per-item source IDs or details, while any other HTTP status fails all items. This also applies to non-array bodies such as `{ "data": [...] }` or `{ "status": "success" }`. Use the structured array to communicate per-item outcomes reliably.

### Saved audit response versus HTTP body

Peakflo adds an audit wrapper when saving the response. For the successful example above, the saved `response` field looks like this:

```json
{
  "status": 200,
  "data": [
    {
      "externalId": "BILL-001",
      "status": "success",
      "sourceId": "DOC-1001",
      "errorMessage": null,
      "details": "Document DOC-1001 posted successfully."
    }
  ]
}
```

Here, `status` is the numeric HTTP status code and `data` is the body returned by your endpoint. **Return only the array as your HTTP body**, without the audit wrapper or an outer `response` property.
