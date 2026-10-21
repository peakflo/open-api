# Employee API

Use `POST /v1/employees` to push employee master data from your system, including
Oracle Fusion. Authenticate using the methods in [Getting started](Introduction.md).
This endpoint is available in API v1.

## Create or update an employee

The authenticated tenant and `sourceId` identify the employee. A new employee
returns `201`; sending the same `sourceId` again updates that employee and returns
`200`. Send all required fields on every request, including updates.

| Field | Required | Meaning |
| --- | --- | --- |
| `companyName` | Yes | Employee display name. |
| `sourceId` | Yes | Stable employee identity from your system, unique within the tenant. |
| `employeeId` / `employeeIds` | At least one | External employee aliases. Both may be sent. `employeeIds` must contain 1–9 unique strings; at most 10 distinct incoming references, including `sourceId`, are allowed. |
| `entityType` | Yes | Must be `individual`. |
| `vendorFirstName` | Yes | Employee first name. |
| `vendorLastName` | No | Employee last name. Omission or null saves an empty last name. |
| `subsidiaries` | Yes | Existing subsidiary references in this tenant. Send `[]` to remove subsidiary restrictions. |
| `contacts` | Yes | At least one contact with a valid `email`. Emails must be unique within the array. Replaces the contact list. |
| `directManagerId` | No | Manager's external `sourceId` in the same company group. See manager handling below. |
| `customField` | No | Values for existing custom-field definitions, identified by `customFieldNumber`. |
| `defaultCurrency` | No | ISO 4217 code; defaults to saved employee currency, then tenant currency, then `SGD`. |
| `beneficiaryCountry` | No | ISO 3166-1 alpha-2 code; defaults to saved employee country or tenant country. |

Identifiers must be nonempty strings without surrounding whitespace. Use
`employeeId` and `employeeIds` for employee aliases; `companyId`, `companyIds` and
tenant override fields are not accepted in the payload. Conflicting references return `409`. Consumers must serialize requests for the
same `sourceId` within a tenant: wait for the response before sending another
update or retry. Existing aliases are retained when new aliases are supplied.

## Example request

Send the manager first with `sourceId: "1000"`, and configure the subsidiary
reference `SG` and custom-field definitions before sending this request.

```http
POST /v1/employees
Content-Type: application/json
x-client-id: <tenant-id>
x-api-key: <api-key>
```

```json
{
  "companyName": "Jane Smith",
  "employeeId": "EMP-001",
  "employeeIds": ["EMP-001", "HR-001"],
  "sourceId": "1001",
  "entityType": "individual",
  "vendorFirstName": "Jane",
  "vendorLastName": "Smith",
  "subsidiaries": ["SG"],
  "directManagerId": "1000",
  "contacts": [{ "email": "jane@example.com" }],
  "customField": [
    { "customFieldNumber": "jobLevel", "value": "Manager" },
    { "customFieldNumber": "empCostCentre", "value": "Finance" },
    { "customFieldNumber": "empDepartment", "value": "Accounts" }
  ]
}
```

## Manager handling

`directManagerId` is resolved using the existing accounting incoming-sync helpers.
The external source reference is matched against `externalRefNumber` for employees
across tenants sharing `groupEntity`; without a group, lookup uses the authenticated
tenant. The matching manager's record ID and owning tenant are passed to shared
employee persistence. The helpers retain their existing selection rules.

Send managers first. An unresolved dependency returns `404`. Omit `directManagerId`
to preserve the saved manager, or send `""` to clear it.

## Contacts and custom fields

Contact names and `externalId` are optional. Missing names inherit employee
names; missing `externalId` uses the contact email. At most one contact may set
`isMainContact: true`; if none does, the first contact is saved as the main contact.
Optional phone numbers must include a country code when populated.

The integration uses `jobLevel`, `empCostCentre` and `empDepartment` as
`customFieldNumber` values. These definitions must already exist for the tenant.
Each number may appear once, and its value must match the configured type and
options. Omitted custom fields are retained. Numeric values must be nonnegative;
multi-select values use arrays of strings. Custom date fields use `DD/MM/YYYY`,
which is an exception to the general API date guidance.

## Responses

Successful responses echo the validated request with normalized `employeeId`
and `employeeIds`. If only `employeeIds` is sent, its first item becomes
`employeeId`; if `employeeId` is sent, it is included in `employeeIds` without
duplicates. The response does not contain internal record IDs, resolved internal
manager IDs or all saved defaults.

| Status | Meaning |
| --- | --- |
| `200` | Existing employee updated. |
| `201` | Employee created. |
| `400` | Invalid request, unknown custom-field number, invalid custom-field value or employee validation failure. |
| `401` | Missing or invalid authentication. |
| `404` | Unknown subsidiary reference or unresolved direct manager dependency. |
| `409` | Employee references already belong to another record. |
| `500` | Unexpected persistence failure. |

Successful saves include nonempty `validationWarnings` returned by the workflow.
Rejected saves also include `validationErrors` and any accompanying warnings.

Validation errors include `requestId`, `statusCode`, `service`, `message` and,
when available, field-level `details`. Use `requestId` when contacting support.

When employee-user sync is enabled for the tenant, employee saves also initiate
linked user creation or profile updates, including manager changes. User updates
complete asynchronously after the employee API response.
