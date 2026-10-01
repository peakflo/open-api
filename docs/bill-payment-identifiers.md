# Bill payment identifiers and subsidiary scope

These rules apply to v1 and v2 bill payment APIs.

- Supply `subsidiaryReference` in create/update request bodies when your ERP reuses document or payment identifiers across subsidiaries.
- For a single-payment GET, supply it as a query parameter: `/v2/bill-payment/3980000002?subsidiaryReference=3130` (the same query parameter is supported in v1).
- Payment identity is the authenticated tenant, subsidiary, and payment `externalId`. The same external ID can exist in different subsidiaries; creating it again in the same subsidiary is rejected.
- Linked bills are matched within the requested subsidiary by Peakflo `externalId` or ERP `sourceId`. In v1 use `billId`; in v2 use `bills[].externalBillId`. SAP DocumentNo may be stored as `sourceId` despite the v2 field name.
- Without `subsidiaryReference`, an identifier must match exactly one active record. Ambiguous identifiers return HTTP 400; supply the subsidiary rather than relying on the first matching record. If multiple bills still match within that subsidiary, use a unique bill external ID.
- An unscoped update that uniquely identifies a payment uses its stored subsidiary to resolve linked bills and preserves that subsidiary.
- An unknown subsidiary returns HTTP 404. A payment update/read with no matching payment in that subsidiary also returns HTTP 404; it does not fall back to another subsidiary's payment.
- PUT updates an existing payment; it does not create or upsert one. Use POST when the payment does not exist in the intended subsidiary.
- Deleted bills and deleted/cancelled payments are excluded from matching. Existing vendor, currency, allocation, payable-amount and paid-payment validations still apply.

## Example

If payment `3980000002` exists only in subsidiary `3144`, a PUT specifying subsidiary `3130` returns not found, even if the external ID matches the `3144` payment. POST the `3130` payment first, with its own vendor, currency and linked bills.
