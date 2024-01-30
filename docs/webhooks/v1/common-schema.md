## Custom Field

```typescript
CustomField = {
  id?: string;
  customFieldNumber: string;
  name: string;
  type: string; //CustomFieldTypes
  sourceId?: string;
  sequence?: number;
  value: string | number | string[];
}

CustomFieldTypes = [
  "input",
  "list",
  "date",
  "number",
  "multiList",
  "multiFile",
]
```

