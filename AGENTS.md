# Repository Guidelines

## Project Structure & Module Organization
- `peakflo-v1.0.yaml` and `peakflo-v2.yaml` are the OpenAPI specs for v1 and v2.
- `docs/Introduction.md` contains general API usage notes (auth, limits, formats).
- `docs/webhooks/v1/` holds webhook docs (e.g., `about.md`, `bill.md`).
- There is no application runtime here; this folder is documentation and API contracts only.

## Build, Test, and Development Commands
- No build or test scripts are defined in this directory.
- Typical workflow: edit the relevant YAML/Markdown file and verify changes with your OpenAPI tooling or parent-repo CI.
- Handy navigation examples: `rg "BillPayment" peakflo-v2.yaml` or `rg "webhooks" docs/`.

## Coding Style & Naming Conventions
- YAML uses 2-space indentation; keep structure consistent with existing OpenAPI 3.0.1 patterns.
- Keep schema/component names in PascalCase (e.g., `BillPayment`) and paths in kebab-case (e.g., `/bill-payment`).
- Date-time examples should remain ISO 8601 UTC strings (e.g., `2024-07-01T13:40:01Z`).
- Currency examples should follow ISO 4217 (e.g., `USD`, `SGD`, `INR`).

## Testing Guidelines
- No automated test framework is present.
- Validate that `$ref` links resolve and example payloads are valid JSON.
- If you add or modify endpoints, ensure both v1/v2 specs and related docs stay in sync.

## Commit & Pull Request Guidelines
- Commit messages often include a task key (e.g., `[TSK-15480]`) and a concise description in present tense.
- PRs commonly include a ticket reference and a brief summary of API changes.
- In PR descriptions, list modified endpoints, schema changes, and any doc updates.

## Security & Configuration Notes
- Authentication is JWT via `Authorization: Bearer <token>` and all requests must use HTTPS.
- Rate limits are 100 requests per second per account.
- Do not commit private keys or access tokens; keep secrets out of docs and examples.
